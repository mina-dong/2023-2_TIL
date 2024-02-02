cp11 서버 유지하기 
---
npm install nodemon -D

D 옵션에 따라 약간 차이가 나는데, 
패키지 제이슨 파일에 보면 기본적인 디펜더시에 생기는게 아니라 devDepencies에 있는걸 확인할 수 있다. 
두가지의 차이점은, 데비디펜더스는 필수적인 요소는 아니지만 따로 적어줄때 사용한다고

스크립트라는건 어떤 명령어를 저장했을 때 그 명령어를 미리 저장하는 것을 지정하는 것이다. 

```
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```

```

  "scripts": {
    "start":"node index.js",
    "dev": "nodemon index.js"
  },
```
이 스크립트를 사용할때는 npm run + "스크립트"를 사용하게 된다. 

nodemon의 장점은 서버를 껏다가 다시 키지 않아도, 안의 내용이 바뀌었을 때 저장하고 나서 리프레시만으로도 바로 확인할 수 있게 된다!

cp12~13 화면구성하기
---
파일 자체를 전송하는 형식으로 하면, 각 파일을 여러개 생성해줘야한다는 점이 있다.  
이걸 보완하기 위해 나온 방법이 templeate engine 이다.  여러가지 파일이 존재한다고 했을 때 공통적인 내용을 묶어주고, 다른 부분만 적절하게 렌더링해서 표현할 수 도 있다.  
EJS, pug, Nunjucks 넌적스 같은 방법이 있다.  

```
npm i numjucks
```
npm은 인스톨 대신 i로 생략할수 있다..

```
import express from 'express';
import path from 'path';
import nunjucks from 'nonjucks';

const __dirname =  path.resolve();

const app = express();
```

**에러발생**
Error [ERR_MODULE_NOT_FOUND]: Cannot find package 'nonjucks' imported from D:\study\node_study\my_app\index.js

오타나서 오류발생. 수정 후 서버 가동. 


```
import express from 'express';
import path from 'path';
import nunjucks from 'nonjucks';

const __dirname =  path.resolve();

const app = express();
//view engine set 
app.set('view engine', 'html'); // main.html -> main(.html)  그냥 main만 입력해도, html이 붙게해줌. 생략가능하게 작성해줌.

//numjucks
nunjucks.configure('views',{
    watach:true, //html 파일이 수정될 경우 다시 반영 후 렌더링
    express:app //어떤 객체를 나타내는지, 앞서 선언한 객체인 app을 입력. 
}); // 정적파일이 아니라, 화면을 구성하는 것들인 views를 여기에 모아둔다
```

그런 다음 views폴더를 생성하고 base.html을 생성한다. 

```
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- 공통된요소 -->
    <nav>
        <a href="">logo</a>
        <a href="">글작성</a>
    </nav>
    <!-- 바뀌는 요소 -->
    <!-- 항상 블록타입의 콘텐츠는 블록을 열어주고 닫아야한다! -->
    {% block content %} 
    {% end %}

    <!-- 공통된요소 -->
    <footer>
        <p>footer</p>
    </footer>
</body>
</html>
```

```
//write.html
<!-- 기본적인 템플릿 -->
{% extends 'base.html' %} 

{% block content %}
<h1>글작성페이지입니다</h1>
{% endblock %}
```

```
// write 
app.get('/write', (req,res) => {
    res.render('/write.html')
 });
```
index.js 에서 render를 사용해서 write.html를 가져온다.. 


**오류발생**
Error: template not found: /write.htm

```
// write
app.get('/write', (req,res) => {
    res.render('/write.html')
 });

```
수정전

```
// write
app.get('/write', (req,res) => {
    res.render('write.html')
 });
```

수정후 


**에러발생**
Template render error: (D:\study\node_study\my_app\views\write.html)

    {% block content %} 
    {% endblock %}

base.html 파일에서 이 부분이
    {% block content %} 
    {% end %}
로 되어 있음, 블록이 제대로 닫히지 않아서 오류 발생했다. 


cp14. 페이지구성하기
---
get과 post 구분하기.   
메인페이지는 글 목록을 보여주기 때문에 단숙하게 출력하기 위해 get을 사용  
글 작성하기 페이지 접속 - get , 그 글을 저장하기위해서는 post   
상세페이지를 보여주는 get   
글 수정 페이지 접속 - get, 수정한 내용이 반영되는 post   