---
layout: single
title: "Oracle DB 운영 환경에서 알아야 할 부하 지표"
toc: true
toc_sticky: true
toc_label: "목차"
categories: database
toc_icon: "bars"
tags: [database]
---

📘DB 부하

대용량 쿼리나 배치 작업을 운영 DB에 실행할 때, 단순히 "쿼리가 느리다"는 것 외에 어떤 자원이 얼마나 소비되는지 정확히 파악해야 합니다. 이 글에서는 Oracle DB에서 모니터링해야 할 핵심 지표들의 개념을 정리합니다.

---

## Oracle 메모리 구조 개요

Oracle의 메모리는 크게 두 가지로 나뉩니다.

- **SGA (System Global Area)** : 모든 세션이 공유하는 메모리
- **PGA (Program Global Area)** : 세션(접속) 하나하나가 독립적으로 가지는 메모리

이 둘의 차이를 이해하는 것이 DB 부하 분석의 출발점입니다.

---

## SGA (System Global Area) — 공유 메모리

Oracle 인스턴스가 시작될 때 OS로부터 할당받는 공유 메모리 영역입니다. DB에 접속한 모든 세션이 이 공간을 함께 사용합니다. SGA는 여러 하위 컴포넌트로 구성됩니다.

### Buffer Cache

디스크의 데이터 블록을 메모리에 캐싱하는 공간입니다. 쿼리 실행 시 먼저 Buffer Cache를 확인하고, 없으면 디스크에서 읽어옵니다.

> ⚠️ **운영 시 주의** : 수천만 건의 Full Table Scan은 Buffer Cache에 대량의 블록을 올리면서 기존에 캐싱된 다른 쿼리의 데이터를 밀어낼 수 있습니다. 이를 **Buffer Cache 오염**이라고 하며, 운영 시간대에 실행하면 다른 세션의 쿼리가 갑자기 느려지는 현상의 주요 원인이 됩니다.
> 

### Shared Pool

SQL 파싱 결과(실행 계획)와 데이터 딕셔너리 정보를 캐싱하는 공간입니다. 동일한 SQL이 재사용될 때 파싱 비용을 아끼는 역할을 합니다. Shared Pool이 부족하면 매번 SQL을 새로 파싱해야 해서 CPU 부하가 올라갑니다.

### Redo Log Buffer

데이터 변경사항을 디스크의 Redo Log 파일에 기록하기 전에 임시로 담아두는 버퍼입니다. SELECT만 하는 경우 거의 사용하지 않지만, 내부적으로 임시 테이블이나 정렬 결과를 기록하는 작업이 수반되면 소량 발생할 수 있습니다.

### Large Pool

병렬 쿼리, RMAN 백업, 공유 서버 모드 등에서 사용하는 메모리 영역입니다. 병렬 처리를 사용하는 대용량 쿼리라면 Large Pool 크기도 확인이 필요합니다.

---

## PGA (Program Global Area) — 세션 전용 메모리

각 세션(DB 접속)마다 독립적으로 할당되는 메모리입니다. SGA와 달리 다른 세션과 공유하지 않습니다. 주로 정렬(Sort), 해시 조인, 바인드 변수 처리 등에 사용됩니다.

- **BEFORE** : 쿼리 실행 전 해당 세션의 PGA 사용량
- **AFTER** : 쿼리 실행 후 PGA 사용량
- **USED** : AFTER - BEFORE, 쿼리가 실제로 추가 사용한 PGA 양

> ⚠️ **운영 시 주의** : 동시 접속 세션이 많을수록 PGA 총합이 커집니다. 단일 세션에서 6MB라도 100개 세션이 동시에 같은 쿼리를 실행하면 600MB가 됩니다. 멀티스레드 구조의 애플리케이션은 반드시 동시 세션 수를 함께 고려해야 합니다.
> 

---

## TEMP (Temporary Tablespace) — 디스크 임시 공간

PGA 메모리가 부족할 때 넘치는 데이터를 디스크에 임시로 저장하는 공간입니다. 주로 대용량 정렬(ORDER BY), 해시 조인, GROUP BY 처리 시 발생합니다.

TEMP를 쓴다는 것은 메모리가 부족해서 디스크 I/O가 발생한다는 의미이므로 성능에 직접적인 영향을 줍니다. TEMP 사용량이 0이면 인덱스를 활용하거나 PGA 안에서 정렬이 완료된 것입니다.

> ⚠️ **운영 시 주의** : TEMP Tablespace의 용량이 부족하면 `ORA-01652: unable to extend temp segment` 에러가 발생하며 쿼리가 실패합니다. 여러 세션이 동시에 TEMP를 사용하면 용량이 빠르게 소진될 수 있습니다.
> 

---

## Undo (Undo Tablespace) — 읽기 일관성 보장

데이터 변경 전 원본 이미지를 저장해두는 공간입니다. UPDATE나 DELETE가 롤백될 때도 사용하지만, **SELECT 쿼리도 읽기 일관성을 위해 Undo를 참조합니다.**

예를 들어 내가 1000만 건짜리 SELECT를 실행하는 도중 다른 세션이 해당 데이터를 변경하면, Oracle은 Undo를 통해 SELECT가 시작된 시점의 데이터를 일관되게 보여줍니다.

쿼리 실행 시간이 길어질수록 그 시간 동안의 Undo 데이터가 보존되어야 하는데, Undo가 너무 빨리 덮어쓰이면 `ORA-01555: snapshot too old` 에러가 발생합니다.

> ⚠️ **운영 시 주의** : 장시간 실행되는 대용량 쿼리는 Undo 보존 압박을 높입니다. `UNDO_RETENTION` 파라미터 설정과 Undo Tablespace 크기를 함께 검토해야 합니다.
> 

---

## CPU (CPU_SEC_USED / CPU_USAGE_PERCENT)

### CPU_SEC_USED

쿼리가 실행되는 동안 CPU를 실제로 점유한 시간(초)입니다. 전체 쿼리 실행 시간(Elapsed Time)과는 다릅니다. Elapsed Time에는 I/O 대기, 네트워크 대기 등 CPU가 쉬는 시간도 포함되지만, CPU_SEC_USED는 CPU가 실제로 연산한 순수 시간만 측정합니다.

### CPU_USAGE_PERCENT

전체 CPU 자원 중 해당 쿼리가 차지한 비율입니다. 멀티코어 환경에서는 단일 쿼리가 한 코어만 사용하면 전체 사용률은 낮게 나올 수 있습니다.

> ⚠️ **운영 시 주의** : 동시에 여러 세션이 같은 쿼리를 실행하면 CPU 사용률이 곱으로 올라갑니다. 단일 테스트 결과만 보고 괜찮다고 판단하면 안 됩니다.
> 

---

## I/O — 논리적 읽기 vs 물리적 읽기

| 구분 | 설명 | 발생 위치 |
| --- | --- | --- |
| 논리적 읽기 (Logical Read) | Buffer Cache에서 읽은 횟수 | 메모리 |
| 물리적 읽기 (Physical Read) | 디스크에서 직접 읽은 횟수 | 디스크 |

물리적 읽기가 많을수록 디스크 I/O 부하가 증가하고 성능이 느려집니다. 처음 실행(1차)에서 물리적 읽기가 많고 두 번째 실행(2차)에서 빨라지는 이유가 Buffer Cache에 데이터가 올라왔기 때문입니다.

Oracle의 `V$SESSTAT` 또는 실행 계획(Execution Plan)의 Statistics 항목에서 확인할 수 있습니다.

---

## Wait Event (대기 이벤트)

쿼리가 CPU 연산 외에 무언가를 기다리는 시간을 분류한 것입니다. CPU 사용량만 보면 쿼리가 어디서 시간을 쓰는지 알 수 없는데, Wait Event와 함께 보면 병목 지점을 정확히 파악할 수 있습니다.

| Wait Event | 의미 |
| --- | --- |
| `db file sequential read` | 인덱스를 통한 블록 읽기 |
| `db file scattered read` | Full Table Scan 시 다중 블록 읽기 |
| `direct path read` | 대용량 병렬 읽기 |
| `log file sync` | Commit 후 Redo Log 기록 대기 |
| `enq: TX - row lock contention` | 다른 세션의 락 대기 |

---

## Lock & Latch — 동시 접근 제어

대용량 쿼리가 실행 중일 때 다른 세션이 같은 테이블에 DML(INSERT/UPDATE/DELETE)을 시도하면 락 경합이 발생할 수 있습니다.

- **Lock** : 테이블이나 행 수준의 접근 제어. SELECT는 기본적으로 락을 걸지 않지만, 상대방 DML이 커밋되지 않은 상태에서 Undo를 참조하는 상황이 생깁니다.
- **Latch** : SGA 내부 메모리 구조를 보호하는 경량 잠금. 동시 세션이 많아지면 Latch 경합이 CPU 스파이크를 유발할 수 있습니다.

---

## 종합 요약

| 지표 | 영향 범위 | 부족/과다 시 증상 |
| --- | --- | --- |
| Buffer Cache (SGA) | DB 전체 세션 | 다른 쿼리 캐시 오염, 성능 저하 |
| Shared Pool (SGA) | DB 전체 세션 | 반복 파싱으로 CPU 상승 |
| PGA | 해당 세션 | TEMP 사용 증가 → 디스크 I/O |
| TEMP | 디스크 | 쿼리 성능 급락, 공간 부족 에러 |
| Undo | 읽기 일관성 | ORA-01555 에러 |
| CPU | 서버 전체 | 다른 프로세스 응답 지연 |
| Physical I/O | 디스크 | 전체 DB 응답 저하 |
| Wait Event | 병목 위치 | 원인 미파악 시 튜닝 불가 |
| Lock / Latch | 동시성 | 세션 대기, CPU 스파이크 |

---

> 💡 **핵심 포인트** : 단일 세션 테스트 결과가 양호해도 운영 환경에서는 동시 세션 수, 운영 시간대 다른 워크로드와의 자원 경합, Buffer Cache 오염을 반드시 함께 고려해야 합니다. 특히 대용량 Full Scan은 운영 피크 시간대를 피해 실행하는 것이 기본 원칙입니다.
>
