# 1. set node.js
npm init : 라이브러리 설치를 도와주는 도구

어떤 라이브러리를 사용했는지 기록하는 것 -> package.json에 저장하게 되는데
해당 파일을 직접 만드는게 아니라 npm init을 통해 자동으로 생성된다. 

엔터를 통해 나머지 부분 생략하고, 터미널 entry point: (index.js) 가 나올때
server.js를 입력한다. 나머지는 생략(엔터입력)

엔트리포인트만 원하는 파일명으로 입력한다. 

Sorry, name can only contain URL-friendly characters. 라는 오류발생.
폴더명이 이상해서 오류가 난듯하여 재수정 후 다시 킴. 

package.json이 생성되고
터미널에 npm install express를 설치한다. 

node_modules 파일은 라이브러리에 필요한 내용이 저장되어 있다. 

# 2. get request

server.js (저번에 init 설정할때 입력한 이름)으로 파일을 생성한다. 


```
const express = require('express');
const app = express();

app.listen()
```

서버를 띄우기 위한 기본 세팅. 

```
app.listen(8080, function(){
    console.log('listening on 8080')
});
```

listen(서버를 띄울 포트 번호, 띄운 후 실행할 코드); 
8080를 통해 들어올 사용자에게 띄울 코드를 의미한다.
포트번호는 임의적으로 적어도 된다. 

터미널에 
node server.js 
를 입력하면 정상반영이 된걸 확인할 수 있다. = 서버를 열었다. 

웹사이트에 localhost:8080 를 입력하면
서버가 열려있음을 확인할 수있다. 


get 요청을 하면 서버에서 수신해서, 요청한 페이지를 보여줌. 

```
app.get('/pet', function(요청, 응답){
    응답.send('get페이지입니다.')
});
```
요청은 req, 응답은 res로 자주 사용한다.  터미널 사용시 컨트롤 C를 이용한다. 
localhost:8080에 경로를 입력하면,  해당 페이지로 get요청을 처리한다. 

수정하고 나면 바로바로 반영이 안되고, 서버를 껐다가 다시 켜야하는 불편함이 있다. 
>> npm install -g nodemon

nodemon server.js
보안 오류가 발생한다 - 윈도우10에서 주로 발생함.
>> 해결방법
 1.windows powershell 관리자권한으로 실행
 2. executionploicy 입력
  결과가 Restricted로 나옴
  왜냐면 윈10에서 nodemon을 막는다고..
 3. set-executionpolicy unrestricted 입력
그럼 실행 규칙을 변경할 수 있는데, Y를 입력한다.
그럼 간단한 스크립트를 실행할 수 있다. 


nodemon server.js 가 작동이 되는걸 확인 할 수 있다. 

app.get('/', function(요청, 응답){
    응답.sendFile(__dirname+'/index.html');
});

/만 입력하면 홈을 의미한다. 
홈에 접속했을 때 sendfile를 이용해서 index.html를 파일을 보내준다. 