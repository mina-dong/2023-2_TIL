cp15 crud 구현하기
---
data 폴더생성 후 writing.json 생성.  
데이터를 생성하면 writing.json에 저장할 수 있게 한다!  

```
import express from 'express';
import path from 'path';
import nunjucks from 'nunjucks';
import bodyParser from 'body-parser';
import fs from 'fs';

const __dirname =  path.resolve();

const app = express();

//file paht
// 이 파일 패스를 통해서 myapp/data/writing.json 으로 이동하게 된다.
const filePath = path.join(__dirname, 'data','writing.json');

// body parser set
app.use(bodyParser.urlencoded({ extended: false })); // express 기본 모듈 사용
app.use(bodyParser.json());

//view engine set 
app.set('view engine', 'html'); // main.html -> main(.html)  그냥 main만 입력해도, html이 붙게해줌. 생략가능하게 작성해줌.

//numjucks
nunjucks.configure('views',{
    watach:true, //html 파일이 수정될 경우 다시 반영 후 렌더링
    express:app //어떤 객체를 나타내는지, 앞서 선언한 객체인 app을 입력. 
}); // 정적파일이 아니라, 화면을 구성하는 것들인 views를 여기에 모아둔다

// middleware
// main page GET
app.get('/', async (req, res) => {
    res.render('main');
});

app.get('/write', (req, res) => {
    res.render('write');
});

app.post('/write', async (req, res) => {
    const title = req.body.title;
    const contents = req.body.contents;
    const date = req.body.date;

    // 데이터 저장
    // data/writing.json 안에 글 내용 저장.
    //readfilesync를 이용함. 노드제이에스는 비동기적인데, 다음 메시지를 실행할 수 있게끔.
    const fileData = fs.readFileSync(filePath);
    console.log(fileData);

    res.render('detail', { 'detail': { title: title, contents: contents, date: date } });
});

app.get('/detail', async (req, res) => {
    res.render('detail');
})

app.listen(3000, () => {
    console.log('Server is running');
});
```

글을 작성하게 되면, 버퍼데이터가 생기는데 이 데이터를 json으로 패싱하기 위해서 변수를선언한다. 
(터미널에보면 buffer ~~~ 라고 나옴) - consolelog를 통해  


```
app.post('/write', async (req, res) => {
    const title = req.body.title;
    const contents = req.body.contents;
    const date = req.body.date;

    // 데이터 저장
    // data/writing.json 안에 글 내용 저장.
    //readfilesync를 이용함. 노드제이에스는 비동기적인데, 다음 메시지를 실행할 수 있게끔.
    const fileData = fs.readFileSync(filePath);
    console.log(fileData);

    const writing = JSON.parse(fileData)
    console.log(writing)
    res.render('detail', { 'detail': { title: title, contents: contents, date: date } });
});
```

이렇게 하면 터미널에 [] 이런식으로 출력이 되는걸 알 수 있다. 


```
app.post('/write', async (req, res) => {
    const title = req.body.title;
    const contents = req.body.contents;
    const date = req.body.date;

    // 데이터 저장
    // data/writing.json 안에 글 내용 저장.
    //readfilesync를 이용함. 노드제이에스는 비동기적인데, 다음 메시지를 실행할 수 있게끔.
    const fileData = fs.readFileSync(filePath);
    //console.log(fileData);

    const writings = JSON.parse(fileData)
    // console.log(writing);

    //request 데이터 저장
    writings.path({
        'title':title,
        'content':contents,
        'date':date
    })
    res.render('detail', { 'detail': { title: title, contents: contents, date: date } });
});
```

이걸 다시 외부에 저장을 해줘야하는데 

```
app.post('/write', async (req, res) => {
    const title = req.body.title;
    const contents = req.body.contents;
    const date = req.body.date;

    // 데이터 저장
    // data/writing.json 안에 글 내용 저장.
    //readfilesync를 이용함. 노드제이에스는 비동기적인데, 다음 메시지를 실행할 수 있게끔.
    const fileData = fs.readFileSync(filePath);
    //console.log(fileData);

    const writings = JSON.parse(fileData)
    // console.log(writing);

    //request 데이터 저장
    writings.push({
        'title':title,
        'content':contents,
        'date':date
    });

    //data/writing.json에 저장하기
    fs.writeFileSync(filePath, JSON.stringify(writings));

    res.render('detail', { 'detail': { title: title, contents: contents, date: date } });
});
```
이렇게 하고 글을 작성하보면 writing.json에 데이터가 저장이 된것을 알 수 있다. 

```
    <nav class="navbar bg-body-tertiary">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">Logo</a>
            <a href="/write">글 작성</a>
        </div>
    </nav>
```
base.html에서 a태그 내용을 바꿔주고 .write로 -> write.html로 변경하는 것을 알 수있다.

```
{% extends 'base.html' %}

{% block content %}
    <h1>메인 페이지</h1>
    {% if list %}
        {{ list }}
    {% else %}
        <p> 작성된 글이 없습니다.</p>
    {% endif %}
{% endblock %}
```
이 부분을 글 목록이 있게 보여주도록 수정한다 . - main.html임. 

```
{% extends 'base.html' %}

{% block content %}
    <h1>메인 페이지</h1>
    {% if list %}
        {% for writing in list %}
            <p>{{writing.title}}</p>
        <!-- for문도 블럭처럼 꼭 닫아줘야한다. -->
        {%endfor%}
    {% else %}
        <p> 작성된 글이 없습니다.</p>
    {% endif %}
{% endblock %}	
```


```
{% extends 'base.html' %}

{% block content %}
    <h1>메인 페이지</h1>
    {% if list %}
        <table class = "table">
            <tr>
                <th>글제목</th>
                <th>글 내용</th>
                <th>글 날짜</th>
            </tr>
                {% for writing in list %}
                    <tr>
                        <td>{{writing.title}}</td>
                        <td>{{writing.contents}}</td>
                        <td>{{writing.date}}</td>
                    </tr>   
                <!-- for문도 블럭처럼 꼭 닫아줘야한다. -->
                {%endfor%}
        </table>
    {% else %}
        <p> 작성된 글이 없습니다.</p>
    {% endif %}
{% endblock %}
```


```
import express from 'express';
import path from 'path';
import nunjucks from 'nunjucks';
import bodyParser from 'body-parser';
import fs, { readFile, readFileSync } from 'fs';

const __dirname =  path.resolve();

const app = express();

//file paht
// 이 파일 패스를 통해서 myapp/data/writing.json 으로 이동하게 된다.
const filePath = path.join(__dirname, 'data','writing.json');

// body parser set
app.use(bodyParser.urlencoded({ extended: false })); // express 기본 모듈 사용
app.use(bodyParser.json());

//view engine set 
app.set('view engine', 'html'); // main.html -> main(.html)  그냥 main만 입력해도, html이 붙게해줌. 생략가능하게 작성해줌.

//numjucks
nunjucks.configure('views',{
    watach:true, //html 파일이 수정될 경우 다시 반영 후 렌더링
    express:app //어떤 객체를 나타내는지, 앞서 선언한 객체인 app을 입력. 
}); // 정적파일이 아니라, 화면을 구성하는 것들인 views를 여기에 모아둔다

// middleware
// main page GET
app.get('/', async (req, res) => {
    const fileData = readFileSync(filePath);
    const writings = JSON.parse(fileData);


    res.render('main', {list:writings});
});

app.get('/write', (req, res) => {
    res.render('write');
});

app.post('/write', async (req, res) => {
    const title = req.body.title;
    const contents = req.body.contents;
    const date = req.body.date;

    // 데이터 저장
    // data/writing.json 안에 글 내용 저장.
    //readfilesync를 이용함. 노드제이에스는 비동기적인데, 다음 메시지를 실행할 수 있게끔.
    const fileData = fs.readFileSync(filePath);
    //console.log(fileData);

    const writings = JSON.parse(fileData)
    // console.log(writing);

    //request 데이터 저장
    writings.push({
        'title':title,
        'content':contents,
        'date':date
    });

    //data/writing.json에 저장하기
    fs.writeFileSync(filePath, JSON.stringify(writings));

    res.render('detail', { 'detail': { title: title, contents: contents, date: date } });
});

app.get('/detail', async (req, res) => {
    res.render('detail');
})

app.listen(3000, () => {
    console.log('Server is running');
});
```
index.js 전체코드 