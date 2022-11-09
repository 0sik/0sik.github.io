# flask 설정 방법
vscode 기준 flask를 다운 받기 위해서는 터미널에 
> pip3 install flask
를 입력하여 다운 받아야 한다
# 라우팅
어떤 네트워크 안에서 통신 데이터를 보낼 때 최적의 경로를 선택하는 과정
플라스크의 라우팅 과정은 다음과 같다
```
@app.route('/')
def index():
    return 'hi'
 
@app.route('/main')
def main():
    return 'flask'
    
@app.route('/main/1')
def main2():
    return 'flask2'    
    
```
/main/1  에서 1이 만약 가변적으로 변하면 어떻게 받아야 될까?
<변수> <>자리 안에 들어오는 값으로 변한다
```
@app.route('/main/<id>/')
def read (id):
  print(id)
  return 'Read'+id
```
## fstirng
파이썬에서 문자열을 변수와 같이 쓸때 쓰는것이 fstring이다
```
s = 'coffee'
n = 5
result1 = f'저는 {s}를 좋아합니다. 하루 {n}잔 마셔요.'
print(result1)
```

## html연결하는법
```
from flask import Flask
import random

app = Flask(__name__)

#나중에 여기 데이터베이스를 가져오는 코드를 넣으면 데이터 베이스랑도 연결 가능
topics = [
    {'id': 1,'title':'html','body':'html is ...'},
    {'id': 2,'title':'css','body':'css is ...'},
    {'id': 3,'title':'js','body':'js is ...'}
]

@app.route('/')
def index():
    liTags = ''
    for topic in topics:
        liTags = liTags + f'<li><a href="/read/{topic["id"]}"/>{topic["title"]}</a></li>'
    return f'''<!doctype html>
    <html>
        <body>
            <h1><a href="/"/>WEB</a><h1>
            <ol>
                {liTags}
            </ol>
            <h2>Welcome</h2>
            Hello,Web
        </body>
    </html>
    '''
 
@app.route('/main')
def index2():
    return 'flask'

@app.route('/read/<id>/')
def read(id):
    return 'READ'+id

app.run(port=5001,debug=True)
```
