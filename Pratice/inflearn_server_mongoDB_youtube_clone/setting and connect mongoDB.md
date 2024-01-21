# ch. 2

1. 노드 설치되어있는지 확인하는 방법  
```
node -v  
```

2. package.json에 기재된 라이브러리를 다운로드 하는 방법 = dependencies  
```
npm install  
```

client도 다운받기 위해 cd client로 경로를 이동하고 npm install을 진행한다.   

3.로컬에서 할 수도 있지만 디플로이 이외에 작업을 하고 있는지 인식해야한다.   
server - config 폴더 안에 dev.js 파일을 생성한다.   


> 오류발생.
> npm ERR! code 1 ~ \bcrypt
> npm ERR! command failed   

ref : https://www.inflearn.com/questions/872982/npm-install-%EC%97%90%EB%9F%AC-%EC%A7%88%EB%AC%B8%EB%93%9C%EB%A6%BD%EB%8B%88%EB%8B%A4

package.json에 있는 bcrypt 삭제 후 npm install bcrypt --save 로 설치.
user.js에서 이름 변경하기 bcrypt -> bcyptjs

4. mongoDB를 이용하려면 cluster를 사용해야한다.   
회원가입하고 나서 cluster를 만들때 free trial이 가능한 나라로 선택한다.   

cluster tier를 보면 m0 sandbox를 사용해야 무료이다!(프로젝트 개수 제한이 있는듯)   
cluster name은 임의작성.   

5분정도 소요되는데 다 생성이 되면 보드가 생성되고,  
connect를 눌러서 connect your application를 클릭.   
server는 nodejs, version 3.0.0...(인데 기본설정인듯다)  

생성된 링크는 3번에 해당된 dev.js안에 링크에 붙여 넣어준다.   

database access가 있는데 username과 password를 입력하고 add user를 입력해서  
링크에 해당되는 <username>와 <password>에 해당 이름을 입력한다.  

> 구버전이라 그런지 직접 입력했는데 현재 확인시 알아서 입력된 상태로 링크를 복사할 수 있었다.   


*중요* 노드 버전 낮춰서 환경을 동일하게 만들어야한다. nvm 설치 후 강의에 표시된 버전으로 변경했다.   
ref: https://sanghee01.tistory.com/33
강의와 버전이 많이 낮아서 인지 계속 헤맸다...

mongo db와 연결은 된거 같은데... npm run dev 입력시
```
[1] npm ERR! code ELIFECYCLE
[1] npm ERR! errno 1
[1] npm ERR! client@0.1.0 start: `react-scripts start`
[1] npm ERR! Exit status 1
```

라는 에러 발생했다. 

cd client 하고 npm install 을 진행했다. 
이후 npm run dev

기다리다 보니 localhost 웹 페이지가 가동되었다. 
