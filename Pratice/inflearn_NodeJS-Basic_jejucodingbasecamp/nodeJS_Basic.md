제주코딩베이스캠프 nodejs 노드 강의 

cp1~cp4. node js 이해

---
chorme 엔진...   

html css -> 브라우저 내에 있는 엔진을 통해 해석  
js - >자바스크립트 엔진을 통해 해석  

크롬에서 만들 v8엔진이 생기면서 자바스크립트 엔진이 빨라지고, 독립적 인 실행이 가능해짐.  
node.js 자바스크림트 런타임이다.  
js는 html 요소를 조작하기 위한 언어인데, 브라우저는 자바스크림의 런타임이라고 표현하기도 한다.   
런타임? 동작할 수 있는 환경.   

1) 심플스레드 simple thread 작업을 처리하는 곳이 하나 (자바스크립트 특징 중 하나임)  
2) non blocking I/O 앞선 작업이 오래걸리는 경우 후반 작업을 먼저함.  

npm node package manger 
node.js를 패키지를 관리할 수 있는 도구로, 필요한 기능들이 미리 구현되어 있는 경우가 많다.!  

LTS long term support 장기 지원 버전이라고 불리며 오랜 기간에 걸쳐짐을 의미한다.   

node.js REPL  -> read evaluatio print loop 를 의미하며 코드를 즉석에서 바로 실행하고 그 결과를 확인할 수 있는 환경  

터미널을 켜서 node라고 입력하면 >(꺽쇄)가 나오는데, 이게 바로 REPL (레펠) 환경이 시작됨을 알 수 있다. 
console.log("hello,wolrd")

.editor를 입력하면 여기서 부터 여러줄의 코드를 입력할 수 있다.
console.time('시작');
for(let i=0; i<10; i++) {console.log(i);}
console.timeEnd('시작');

결과
0
1
2
3
4
5
6
7
8
9
시작: 6.705ms

이런식으로 time을 이용하면 걸리는 시간을 알 수 있다.


repl -> 코드를 바로 실행할 수 있다.  js 파일 -> 특정 기능을 담은 하나의 파일 실행


임의의 js파일을 생성하고, 단순 출력- console.log("first")  을 입력한다.
터미널에서 node 파일명 을 입력하면 해당 파일을 출력한다. 
node 001_nodejs.js
> first


cp.5 server ?
---
클라이언트가 요청하면 서버에서는 응답 response함.


HTTP : 인터넷상에서 데이터를 주고받고할때 사용하는 프로토콜 - 통신마다 독립적으로 관리한다. 
HTTP request와 HTTP response
HTTP request -> 어디에 보낼지: url + 어떻게?: 요청 메서드 get, post, put, delete 
HTTP response -> 어디에 보낼지: 요청을 한곳 + 어떻게?: 응답코드 2xx 3xx 

get : url 에 요청하는 정보가 포함된다. 단순 열람이 이에 해당한다. 
post : url에 요청하는 정보가 포함되어 있지 않고, body부분에 요청 정보를 포함한다. 요청내용이 길거나 보안이 필요한 경우에 이에 해당한다. = url에 포함(공개)할 수 없기 때문에. 


url을 주소창에 입력 -> 브라우저 : 이 도메인 주소(url)의 ip? <- ip 주소 제공 : domain server

브라우저: ip 주소를 통해 실제 주소를 찾아감 -> 해당 서버를 찾음 -> 브라우저에 제공 -> 사용자에게 제공 



const http = require('http'); 객체를 생성함


cp6. node server cls
---

```
const http = require('http'); // http 객체를 사용함.

const server = http.createServer((req, res) => {
    res.writeHead(200, {'content-Type':'text/plain'});  // 응답 헤드부분 작성
    res.write('helloJS'); //응답 내용 - 응답 body
    res.end(); // 항상 요청이 있을 때 다 처리했다는 코드로 마무리해야한다. 
});

// 어떤 포트를 사용할 건지, 서버가 동작하게 됏을 때 터미널에 있는 콘솔을 통해 작동여부를 확인한다.
server.listen(3000, ()=> {
    console.log('server is running');
});
```

터미널에 node server.js 를 입력하면 터미널에 server is running' 해당 내용이 출력된다. 콘솔에 입력한 데이터는 터미널에 뜨기 때문이다. 평소에 사용하는 브라우저를 사용해서 localhost:3000를 이용하거나 127.0.0.1:3000(포트)를 입력하면 es.write('helloJS'); 즉, helloJS가 브라우저에 출력되고 있음을 알 수 있다. 

노드를 종료하게 되면 = 컨트롤  c 브라우저에서도 종료됨을 알 수 있다. 