cp16 mongoDB
---
json에 저장하는 방법이 있지만, DB를 사용하는 방법도 있다!

관계형 SQL과 비관계형데이터베이스 noSQL가 있다. 가벼운 프로젝트에서는 noSQL을 많이 사용하기도 한다!  
noSQL 데이터 분류 중 하나로 문서 지향 데이터베이스가 있다. 데이터 구조가 키:벨류 쌍으로 이루어져있고 모든 데이터가 json 형태로 저장된다. 

mongoDB 설치 -> nodejs와 mongoDB를 맵핑해주는 mongoose 모듈을 설치 -> mongoDB 실행 -> express 프로젝트와 연동.   

의 절차를 가진다. 

brew가 설치되어야 하고, 터미널환경에서 진행한다!  
강좌에넌 맥 환경이기 때문에 windows 환경으로 찾아서 진행했다. 

ref: https://thisismi.tistory.com/23
