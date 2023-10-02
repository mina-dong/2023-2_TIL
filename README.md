# 2023-2_TIL


* 소프트웨어공학 Software engineering
* 알고리즘 Algorithm
* 컴퓨터시스템개론 Computer System 
* 펌웨어프로그래밍 Firmware programming
* 프로그래밍언어론 Programming Language Theory
* 빅데이터분석시각화 Big Data Visualization and Analysis



## remote:permission to 사용자이름/git이름 denied to 사용자이름. fatal: unable to access 'git 주소' : the requested URL returned error: 403

 ### console 창에서 실행
 
1. replit 에서 import 를 해서 레포지토리(add readme.md c체크하긴 했는데 필수 사항인지는 모르겠음) 와 우선 연결함.
2. 보통의 git 연결과정과 비슷하게 진행.
3. git add.
4. git commit -m "커밋메시지"
5. git push origin main -> remote:permission to 사용자이름/git이름 denied to 사용자이름. fatal: unable to access 'git 주소' : the requested URL returned error: 403
   = > 관련으로 구글 검색시 token 발급, 제어판 - 일반자격 증명자 내용이 나오는데 나에게는 적용되는 게 없었음(해결안됌)

6. **중요** git push https://{token}@github.com/사용자이름/깃이름.git

contributions 및 git push(레포지스토리에 변동된 사항이 제대로 올라옴)이 정상적으로 됌.
이전에는 contributions만 반영되고 push는 제대로 안됐는데(=잔디밭만 채워지고 코드가 올라가지 않음)
저 방법으로 push하니 정상적으로 반영됨.


##  ! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs to 'https://github.com/mina-dong/2023-2_TIL.git'  
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. 
 Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.  
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

현재 브랜치의 긑이 리모트 브랜치보다 뒤에 있으므로 업데이트가 거부됨 
=> 원격저장소와 로컬저장소간 오류발생  
=> rebase로 잔디관련(푸시는되는데 기여란에 초록색으로 보여지지 않은 에러) 시도하다가 브랜치위치 바뀌면서 오류가 생긴듯함
=> git pull 오류생김
=> --force로 강제 푸시

1. git push https://{token}@github.com/사용자이름/깃이름.git **--force**

