---
layout: single
title: "Branch Prediction(분기예측)"
toc: true
toc_sticky: true
toc_label: "목차"
categories: backendstudy
toc_icon: "bars"
tags: [backendstudy]
---
📘 Branch Prediction(분기예측)

회사 기술면접 코딩테스트를 보았다.
내가 한 프로젝트들을 잘 설명하고 정렬 알고리즘 문제도 풀었다.

근데 그 이후 예전과는 다른 분류의 문제를 풀어야 했는데 이 문제를 풀지 못해 멘붕이 오고 면접을 망한거같다..
그 문제는 바로 분기예측이다.

집에 와서 찾아보니까 스택 오버 플로우에서 그 문제를 찾을수 있었다.
[링크](https://stackoverflow.com/questions/11227809/why-is-processing-a-sorted-array-faster-than-processing-an-unsorted-array)

질문은

``` 
#include <algorithm>
#include <ctime>
#include <iostream>

int main()
{
    // Generate data
    const unsigned arraySize = 32768;
    int data[arraySize];

    for (unsigned c = 0; c < arraySize; ++c)
        data[c] = std::rand() % 256;

    // !!! With this, the next loop runs faster.
    std::sort(data, data + arraySize);

    // Test
    clock_t start = clock();
    long long sum = 0;

    for (unsigned i = 0; i < 100000; ++i)
    {
        // Primary loop
        for (unsigned c = 0; c < arraySize; ++c)
        {
            if (data[c] >= 128)
                sum += data[c];
        }
    }

    double elapsedTime = static_cast<double>(clock() - start) / CLOCKS_PER_SEC;

    std::cout << elapsedTime << std::endl;
    std::cout << "sum = " << sum << std::endl;
}
``` 
위의 코드에서 
- std::sort(data, data + arraySize);
이렇게 정렬을 했을때 더 빠를지 안빠를지의 문제이다.
당연히 정렬을 하지 않은게 더 빠르다고 생각하기 마련인데 정렬한게 더 빠르다고 한다.
실제로 실행해보니 두배이상 더 빨랐다.

그 이유는 바로 cpu의 branch prediction때문이다.

# Branch predicion
분기 예측(영어: branch prediction)은 다음 실행될 조건문이 어떤 곳으로 분기할 것인지를 확실히 알게 되기 전에 
미리 추측하는 CPU 기술이다. (출저 위키피디아)

## Static Branch Prediction(정적분기예측)

정적 분기 예측은 컴파일러의 도움으로 분기 여부를 예측하는 기법으로 분기가 발생하지 않는다(분기가 실패한다)고 가정하는 발생 예측 기법과 분기가 발생한다(분기가 성공한다)고 가정한는 발생 얘측기법이 있다.
1. 분기가 실패할 것으로 예측 (predict the branch as not taken)
    - 분기가 일어나지 않을 것으로 예측하고 실행
    - 분기 주소는 “ID” 단계에서 미리 계산 -> ID : Instruction Decoding 단계
    - 만약 분기가 일어나면, 파이프라인을 멈춘 뒤 분기 주소로 이동
2. 분기가 성공할 것으로 예측 (predict the branch as taken)
    - 분기 주소는 “ID” 단계에서 미리 계산
    - 예상 페널티: 1 사이클 (실제로 분기 안 함), 1 사이클 (실제로 분기) -> 장점이자 단점임. 무조건 1사이클

## Dynamic Branch Prediction(동적분기예측)
conditional branch의 과거를 기반으로 예측을 수행한다.
하드웨어에서 각 branch마다 과거를 기억하고 있어서, 해당 branch의 트렌드로 예측을 한다.
두가지 종류가 있는데, 1-bit predictior와 2-bit predictor가 있다.
1-bit predictor는 branch가 Taken이 된다면 bit를 0으로 바꿈으로써 다음 branch도 taken 될 것이라 판단하고, branch가 not taken이 된다면 bit를 1로 바꾸고, 다음 branch는 taken 되지 않을 것이라 판단한다.
default는 1이다.

2-bit predictor은 대략 두번의 예측이 틀렸을때, 비로소 예측이 바뀐다
strongly taken, weakly taken,strongly not taken, weakly not taken이 있다.
default는 weakly not taken이다.


# 이유
CPU가 연산을 수행하면서 분기를 만나게 된다면 조건 값의 계산이 끝날때 까지 기다려야한다. 그만큼의 지연이 발생한다.
그렇기 때문에 cpu는 미리 조건의 값을 추론하여 미리 명령을 실행시켜놓고 기다린다.
만약 분기 얘측이 맞으면 지연없이 바로 수행이 가능하고 분기얘측이 틀린 경우 다시 올바른 명령이 수행된다.

정렬된 경우 앞에 부분은 포함이 안될거고 뒤에 부분이 계속 포함이 될거니까 계속 적중하여 지연이 없이 수행될거고
정렬되지 않을 경우 분기예측이 틀려 다시 처음부터 연산이 수행되어 시간이 지연될 것이다. 


- 저 상황에서 소트를 하는것은 두배이상의 빠른 효과를 가지고 옵니다. 왜냐하면 cpu상 dynamic Branch Prediction을 사용하게 되면 128이전에는 F였다 그 이후 전부 T라는 결과가 일어나 miss가 고작 한번만 일어나기 때문에 파이프라이닝을 ....

# 확장
이 문제를 찾아보다 확장된 이론을 적용한 블로그를 보았다.
[링크](https://jissi.tistory.com/20)
정렬되지 않은 데이터를 사용하면서 속도를 빠르게 내는 방법을 정리한 글이다.

방법은 분기되지 않게 하면 된다.

if (data[c] >= 128)
    sum += data[c];
위의 코드를
int t = (data[c] - 128) >> 31;
sum += ~t & data[c];
아래 코드로 변경 할 수 있다.

int t = (data[c] - 128) >> 31;: 이 줄은 data[c]에서 128을 뺀 다음 결과를 31비트만큼 오른쪽으로 이동하여 t 값을 계산한다. 31비트만큼 오른쪽으로 시프트하면 결과의 부호 비트가 효과적으로 추출된다. 원래 data[c]가 128보다 크거나 같으면 부호 비트는 0(양수의 경우)이 되고, 128보다 작으면 부호 비트는 1(음수의 경우)이 된다.
sum += ~t & data[c];: 이 줄은 t 값을 기반으로 조건부 추가를 수행한다. 여기서 ~t는 t의 비트 보수이므로 t가 0이면 ~t는 모두 1이 되고, t가 1이면 ~t는 모두 0이 된다. data[c]와 비트별 AND(&)는 조건에 따라 data[c]의 비트를 효과적으로 마스크한다. t가 0인 경우(data[c]가 128보다 크거나 같음을 의미) data[c]의 전체 값이 sum에 추가된다. t가 1이면(data[c]가 128보다 작다는 의미) 추가가 생략된다(~t로 마스크됨).