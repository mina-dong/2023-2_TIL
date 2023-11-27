# subroutine 부프로그램

## 1. macro funcion and inline function 
### inefficient subroutine 
짧은 길이의 명령어.  
오버헤드 : call and return 할때까지 메모리가 할당됨, context switching  
실행하는게 번거로움 . annoying  

### macro funcion 
not call, replacement.  
```
#define subtracion (x,y) x-y  
result = subtraction (a+1, b+10)

//결과
result = a+1-b+10: 
```

이런식으로 replace 된다. 만약 원하는 결과가 (a+1)-(b+10)인 경우, 아래와 같이 괄호를 사용한다 use bracket 
```
#define subtracion (x,y) (x)-(y)  
```


### inline function 
전형적인 서브루틴으로써, 정직한 실행을 함.  implementation as straightforward as a typical subroutine  
프로세스는 매크로 펑션과 비슷하다.

```
inline int subtracion(int x, int y) {
 return x-y
}
```
## 2. subprogram linkage 서브프로그램 연결 
### 프로그램 (서브프로그램포함) 구조
- code segment + activation record
- AR? activation record로, 활성화 레코드라고도 부름 : 런타임동한 바뀔수 있는 지역변수와 데이터를 의미함.

### 서프브로그램 linkage : 서브프로그램 호출과 반환 call and return

### call operation 
- save exectuion state
- allocation of activaion record(in case of dynamic local variavles)
- parameter passing
- sending return address to callee
- transferring control to the callee

### return operation
- passing the foraml parameter value as an actual parameter아웃모드일때만 해당.
- restoring the callers execution state
- deallocation of the mory space and activation record
- switch control to the caller

## 3. subroutine implementation  
### static subprogram - 중첩과 재귀가 안됨. 
얼리버전의 포트란에서 사용했고, loading 타임에 메모리 할당함. 그리고 모든 변수들이 고정됨.  
|static subprogram  |
|-----|
|return value|
|local variable|
|formal parameter|
|return address|

### non-nested subroutine with stack-dynamic local variables - 중첩없는 서브루틴 + 스택다이나믹 로컬 배리어블 
- 복잡한 AR (활성화 레코드)
- 서브프로그램 연결 - 스태틱 서브프로그램 보다 더 복잡함.
- 동적 변수
- concurrent activation 동시발생의 활동
- 비지역변수 접근 제공
   
|non-nested -- |
|-----|
|local variable|
|formal parameter|
|dynamic link // callers top(pointer)| 
|return address// callers code segment address|
|return value|

다이나믹 링크는 caller's top, AR을 지우기 위해서 사용함.  
재귀호출 가능!  

### nested sub프로그램. 
비지역 변수에 접근하기 위해서 1) 변수가 배정된 활성화레코드를 찾음 2)로컬오프세을 사용해서 목표 변수에 접근함.  

- static link : static paren의 AR의 base의 포인터.
- static chain : 스택에서 활성화 레코드를 연결하는 스태틱 링크의 체인.
- static depth : 깊은지..
- nesting depth = chain offset : 비지역변수를 참조할대, 활성화 레코드를 넘어야할 링크 수
- access variable using offsets

## 4. block program 
블록 = 참조영역 

### block-structured language 

## 5. static scope 정적 범위
1) 중앙에서 관리 central stack apporach

chain offset을 찾기 위해... 1. 지역변수 확인 2. 없으면 비지역변수 확인. 3. 찾을때까지 해서, 시간이 조금 걸림   
즉, 시간을 예측하기 어렵다는 단점이 있다. 
2) diplay approach
현재 서브 프로그램의 스태틱 체인을 maintain 하고 있음. 
바로 찾을 수 있다!

## 6. dynamic scope 동적 범위
### 심층접근방식deep access 
central stack approach. 

비지역 참조가 필요하고, identifier를 사용해 local table을 찾음.  

**스태틱 체인과 다른점 : 컴파일 시간에 실행되서 체인으 ㅣ길이를 결정할 수 없다 = > 느린 퍼모먼스**
또한, 활성화 레코드를 안내하기 위해 반드시 변수 이름을 저장store해야한다. 
(스태틱 범위는 오진 체인과 로컬 오프셋만 요구됨)  

### shallow access 피상접근방법
1) central reference environment table : 중앙 참조 환경 테이블
비지역 참조를 찾지 않아도 됨. 중앙 테이블은 모든 활성화관계를 포함하고 있음(로컬이든 로컬이 아니든.)
다이나믹 체인을 따라가지 않아도 이 테이블만 있으면 확인 가능하다.

문제점: 다이나믹하다보니, 실행시간이 바뀌면 테이블도 바뀌어서 계속 갱신할 필요가 있다.  

2) variable stack
모든 변수에 대해 stack구조르 부여함. 주어진 포인트에, 명확한 이름을 가지고 있는 하나의 visible 변수만 있음. 
