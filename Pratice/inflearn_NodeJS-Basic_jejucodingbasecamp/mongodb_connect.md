cp16 mongoDB
---
json에 저장하는 방법이 있지만, DB를 사용하는 방법도 있다!

관계형 SQL과 비관계형데이터베이스 noSQL가 있다. 가벼운 프로젝트에서는 noSQL을 많이 사용하기도 한다!  
noSQL 데이터 분류 중 하나로 문서 지향 데이터베이스가 있다. 데이터 구조가 키:벨류 쌍으로 이루어져있고 모든 데이터가 json 형태로 저장된다. 

mongoDB 설치 -> nodejs와 mongoDB를 맵핑해주는 mongoose 모듈을 설치 -> mongoDB 실행 -> express 프로젝트와 연동.   

의 절차를 가진다. 

brew가 설치되어야 하고, 터미널환경에서 진행한다!    
강좌에넌 맥 환경이기 때문에 windows 환경으로 찾아서 진행했다.   

ref: https://thesse.tistory.com/308  
ref:https://thisismi.tistory.com/23 
ref:https://shanepark.tistory.com/103      
ref: https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-windows-unattended/

localhost:27017 입력했을때,   
It looks like you are trying to access MongoDB over HTTP on the native driver port.  
라고하면 된거라고 해서 우선 진행함 
(따로 맥환경처럼 커뮤니티 버전?을 터미널?을 통해 더 설치하진 않음.)  
cmd 
net start를 통해 현재 실행중인서비스를 알수 있음 (brew services list 와 비슷한 기능인거 같다)


cp17 mongoDB 셋팅
---
mongoose 
- 스키마 : node.js 에서 데이터 처리를 쉽게 해줄 수 있는 스키마 기능 제공
- 스키마종류 : string, number, date, boolean, buffer, mixed(모든 데이터 타입 가능), objectedid(객체아이디),array(배열)

npm i mongoose
mongoose 를 설치함.  

import mongoose from 'mongoose';   
추가하고 - index.js  

```
//mongoose set
const { Schema } = mongoose;

//새로운 몽구스 객체 생성. - 스키마 구조를 생성함 
const WritingSchema = new Schema({
    title: String,
    contents: String,
    date: {
        type: Date,
        default: Date.now,
    }
})

const Writing = mongoose.model('writing', WritingSchema);
```

npm run dev 대신 brew service start mongodb-community 해도 
각가의 포트에서 독립적으로 하는건데, 이걸 연결하기 위해 몽구스를 사용한다. 

```
// mongoose connect
mongoose.connect('mongodb://127.0.01:27017')
        .then(()=> console.log('연결성공'))
        .catch((e)=> console.error(e));
```

몽구스 연결여부 . 만약 성공하면 성공 log 가 오류나면 catch문으로 이동. 

그래서 서버를 실행 - npm run dev 했을때, 콘솔창을 확인하면 됨. 


**에러발생**
MongooseServerSelectionError: getaddrinfo ENOTFOUND 127.0.01

mongoose.connect('mongodb://127.0.01:27017')
mongoose.connect('mongodb://127.0.0.1:27017') 로 수정처리. 


ref: https://velog.io/@yu9562/MongoDB-mongoDB-Connection-Error-MongooseServerSelectionError-connect-ECONNREFUSED-127.0.0.127017-%EC%97%90%EB%9F%AC-%ED%95%B4%EA%B2%B0


작업관리자 - 서비스 확인시 상태가 중지되어 있어 사용으로 설정함. 

=>  진행완료. 


서버에서 데이터를 저장하기 위해서는 서버에서 추가적인 설텅을 해줘야한다.

mongodb > database > collection > document 
이런식으로 포함관계인데,
도큐멘트는 키와 밸류로 이루어져 있다. 

맥환경이여서 다른 블로그를 찾아봤다
ref: https://freekim.tistory.com/13  
ref: https://freekim.tistory.com/12 몽고디비 기본커맨드  


... 제대로 안되서 (mongo라는명령어를 쳐도 찾을 수없다는식으로 나온다)

몽고디비 버전이 현재 7?이였는데 5.0.24로 재설치.
