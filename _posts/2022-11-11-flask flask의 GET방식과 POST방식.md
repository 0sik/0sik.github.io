---
layout: single
title: "GET방식과 POST방식"
toc: true
toc_sticky: true
toc_label: "목차"
categories: flask
toc_icon: "bars"
tags: [flask]
---


📘 Flask



# CRUD란?

정보기술의 본질은
<li>Create</li>
<li>Read</li>
<li>Update</li>
<li>Delete</li>


## Create

a태그를 이용하여 /create/라는 사이트 접속하는법

```  
<a href="/create/">create</a>
```

create를 누르면 /create/로 접속가능

```<p>태그란 한줄에 하나씩 쓸수 있는 태그 방식 이다```

```<input type ="text" name="title" placeholder="title">```
<p>여기서 사용자에게 값을 입력받는데 type이 text인 값을 받고 title이라는 변수에 저장된다 코틀린기준 hint가 placeholder이다</p>

```<textarea name="body",placeholder="body"</textarea>```
<p>textarea란 문장들을 입력 받는것이고 body라는 변수에 저장된다</p>

```<input type ="submit" vlaue="create">```
<p>type이 submit은 코틀린기준 button이다</p>

## UPDATE


```
@app.route('/update/<int:id>/',methods=['GET','POST'])
def update(id):
    if request.method=='GET' :
        title = ''
        body = ''
        for topic in topics:
            if id == topic['id']:
                title = topic['title']
                body = topic['body']
                break
        content = f'''
            <form action="/update/{id}/" method="POST">
                <p><input type="text" name="title" placeholder="title" value="{title}"></p>
                <p><textarea name="body" placeholder ="body">{body}</textarea></p>
                <p><input type = "submit" value="update"></p>
            </form>
        '''
        return template(getContents(),content)
    elif request.method=='POST':
        global nextId #전역변수를 사용하기 전에 전역변수라고 선언해줘야됨
        title = request.form['title']
        body = request.form['body']
        for topic in  topics:
            if id == topic['id']:
                topic['title'] = title
                topic['body'] = body
                break
        url='/read/'+str(id)+'/'
        return redirect(url)


```


## Delete
```
def template(contents,content,id=None):
contextUI =''
if(id != None):
contextUI =f'''
<li><a href="/update/{id}/">update</a></li>
<li><form action="/delete/{id}/" method ="POST"><input type="submit" value ="delete"></form></li>
```

<p>Delete일때는 method가 무조건 POST방식이어야 한다. GET방식으로 url을 치고 들어가면 삭제가 되니까 POST방식이어야한다</p>

```
@app.route('/delete/<int:id>/',methods=['POST'])
def delete(id):
    for topic in topics:
        if id == topic['id']:
            topics.remove(topic)
            break
    return redirect('/')
    
```

# GET방식
url을 통해서 서버로 데이터를 전송하는 방식은 GET방식이다.
<p>create/title=f&body=f+is+</p>
처럼 주소뒤에 title과 body의 데이터를 전송하는 방식이다
어떤 웹 페이지에 데이터를 사용자가 가져올때는 get방식을 쓴다

# POST방식
값을 변경할때는 POST방식을 이용한다.
주소 뒤에 title과 body의 데이터가 들어가있지않고 웹 브라우저가 서버한테 전송한 데이터는
payload라는 곳에 은밀하게 전송된다, <p>훨씬 더 큰 데이터를 안전하게 전송할수있다는 장점이있다.
사용자가 값을 변경할때는 POST방식을 사용한다.</p>
```<form action="/create/" method="POST">```
<p>여기서 method가 POST로 변경 되었기 때문에 위에 @app.route에서도 설정해줘야한다</p>
설정 방법은 @app.route('/create/',methods=['GET','POST']이다

>redirect
> <p>redirct이란 사용자에게 어디로 이동하라고 명렁할수있다.</p>
> <p>url = '/read/'+str(nextId)+'/'</p>
> <p>return redirect(url)</p>