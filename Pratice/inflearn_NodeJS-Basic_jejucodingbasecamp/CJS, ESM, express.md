cp7 ESM
---
내부외부모듈 + 내코드 = 하나의 프로젝트!

익스프레스!

```
npm init 
```

새로운 프로젝트를 선언하는 명령어.
여러가지 명령어가 나온다!. 
이 프로젝트의 설명, 기타 등등이 나오면서 프로젝트 기본 설정이 진행되고, package.json 라는 파일이 생성되면서 기본적인 내용이 여기에 적히게 된다.

```
npm install express
```

이렇게 명령어를 통해 익스프레스를 설치하게 되면, node_modules라는 폴더가 내 프로젝트안에 생기는 것을 확인할 수 있다. 익스프레스 자체도 누군가 만들어놓은 코드 덩어리여서 그 코드를 가져와서 사용할 수 있게 된다. 
package.json에 내용이 추가된것을 볼 수 있는데, 외부 라이브러리가 어떤 버전인지 어떤 종류가 설치되었는지 확인할 수 있다. 그래서 이를 통해 동일한 환경으로 설치할 수 있게 된다. 


```
{
  "name": "my_app",
  "version": "1.0.0",
  "description": "first project",
  "main": "index.js",
```
```
{
  "name": "my_app",
  "version": "1.0.0",
  "description": "first project",
  "main": "index.js",
  "type":"module",
```

package.json에 type:module를 입력하면, ESM 모드로 사용하겠다는것을 의미하게 된다. 


인덱스 js를 생성한다. 

cp8. ESM2
---
어떻게 ESM모드로 변경할 수 있는지. 


ESM은 require 대신에, import~from 구조를 사용한다.

```
//server.js - CJS 스타일 
const http = require('http'); // http 객체를 사용함.
const server = http.createServer((req, res) => {

```

```
//index.js - ESM 스타일	
import {createServer} from 'http';
const server = createServer((req, res) => {
```

이렇게 임포트를 하는경우 http. create~ 를 쓸 필요 없이 바로 create~ 라고 입력하면된다
(객체를 따로 생성하지 않아도 되니까 가능하다는 뜻 같음) 


*에러발생*
import { createServer } from 'http';
       ^

SyntaxError: Unexpected token {
    at Module._compile (internal/modules/cjs/loader.js:721:23)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:787:10)
    at Module.load (internal/modules/cjs/loader.js:653:32)
    at tryModuleLoad (internal/modules/cjs/loader.js:593:12)
    at Function.Module._load (internal/modules/cjs/loader.js:585:3)
    at Function.Module.runMain (internal/modules/cjs/loader.js:829:12)
    at startup (internal/bootstrap/node.js:283:19)
    at bootstrapNodeJSCore (internal/bootstrap/node.js:622:3)

ref : https://wotres.tistory.com/entry/node%EC%97%90%EC%84%9C-SyntaxError-Unexpected-token-import-%EC%98%A4%EB%A5%98-%EB%B0%9C%EC%83%9D%EC%8B%9C-%EC%A1%B0%EC%B9%98%EB%B0%A9%EB%B2%95



운영 체제 및 버전(OS): Windows, macOS, Linux
Node.js 버전: 18.16.0 (23년 5월 기준)
Express 버전: 4.16.1 (23년 5월 기준)
MongoDB 버전: 5.0.17 (23년 5월 기준)
- 인프런 강좌사이트 링크- 

현재 내 노드 버전이 10.x.x 인데 버전이 낮아서 오류가 생긴거 같다! 
(import 문법이 ES6이전에는 적용되지 않는다고 한다)

nvm list available, nvm list, nvm install vxx.xx.x, nvm use xx.xx.x 을 통해 버전을 변경했다 



cp9~10. express??
---
가장 많이 사용하는 웹 프레임워크 : 많은 기능을 미리 구현해놓은 도구다.   
익스프레스는 미들웨어 middleware의 연결로, 미들웨어는 요청과 응답사이 목적에 맞는 일을 수행하는 함수를 의미한다.   
request - middleware - middleware - middleware - response ..  

웹페이지 기획 전, 어떤 기능이 있는지 구성한다.   
무언갈 생성하고, 삭제, 수정 등등. 하고 하는걸 CRUD라고 한다. 


보통 html파일을 만들어서 전송해주는 식으로 작성하기도 한다. 웹프로젝트 안에서는 public이라는 걸 만들어저 정적 파일들을 관리한다. public안에 main.html 를 만들어주고. index.js res.sendfile(__dirname+'경로')를 통해 보내준다. __dirname 을 사용하기 위해서는 import path form 'path' 와  const__dirname = path.resolve();를 지명해줘야 오류가 생기지 않는다. 


```
import express from 'express';
import path from 'path';

const __dirname =  path.resolve;

const app = express();

//middle ware 부분
// main page GET
app.get('/', (req,res) => {
   // res.send('main page GET request');
   // 단순하게 한줄 보낼때는 send를 
   //res.send('<h1>hello main page</h1>')
   // 파일을 보낼때는 sendFile를 사용한다. 
   res.sendFile(__dirname+'/public/main.html')
});

app.listen(3000, () => {
    console.log('server is running');
});
```