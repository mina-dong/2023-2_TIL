# subroutine 부프로그램

## 1. Principle of the subroutine : 서브루틴 원칙(규칙)  

*process : 어떤 절차, 단위*  
*abstraction : 추상화*  

### process abstraction : 프로세스 추상화
어떤 task를 실행하는 명령어의 집합. 
(babbage's anlytical engine의 카드 뭉치)  

**프로세스 추상화의 필요성 : 작업단위를 추상화시켜 재사용**
-> 서브프로그램의 재사용
- 디테일을 감출수 있고, logical struture를 노출할 수 있음.

변수나 내용이 달라도 수행하는 명령어가 같음-> 서브프로그램화 , 즉 추상화를 하고 필요할 때마다 가져와서 사용한다.  

### data abstraction :  자료구조
ADT   
캡슐화  encapsulation  


### 서브루틴 원칙 principle of the subroutine 
- 각 서브루틴은 single entry point를 가짐 = 즉 항상 하나의진입점을 가짐
- 주어진 시간에, 단 하나의 서브루틴만 실행되어야함
- 서브루틴이 끝나면, 제어권은 콜러한데 돌아감(control always returns to the caller)

### 서브루틴의 구조 
definitaion, declaration, call.  
정의 예시)  
void sub(a,b) {...}  
선언 예시)  
void sub(a,b);  
호출 예시)  
void main(){ ... sub(x,y); .. }  

*정의와 선언의 차이는 무엇일까?*

서브루틴의 구성요소 1)header 2)body  
헤더에는 서브루틴의 정의, 서브루틴의 이름, optionally 파라미터 리스트가 명시되어 있어야한다. 
예) void adder(parameter)  
바디에는 code. 끝.  

### 서브루틴의 선언. 
static type checking  
파라미터 타입과 같은 인터페이스 정보를 우선적으로 제공해야함.
서브루틴 바디를 포함하지 않을 것.  
실제로 정의된 타입이 동일한지 아닌지를 확인함! 

### 서브루틴 접근하기 data access of the subroutine  
1) 비지역변수에 직접적으로 접근하기 direct avvess through non-local variables
2) 파라미터를 통해 접근하기 access through parameter passing - 복사가 된 데이터를 사용함.  즉, 매개변수 공간을 할당하고 값을 복사하는 형태임.

## 2. local variavles and parametres  
지역변수는 2가지가 있다. 1) 스택다이나믹 로컬 변수 2) 스태틱 로컬 변수  

1) stack dynamic local variable
   서브루틴을 실행할 때, 메모리가 바인딩 된다(it is bound to memory)
   서브루틴이 종료될때(terminates), 메모리로부터 바인딩해제된다(it is unbound from memory)

장점: 재귀적으로 호출할 수 있고, 유연성을 가지고 있음. (flextibility, recursively callable)  
로컬변수를 위한 메모리공간을 공유할 수 있음. (memory space for local variavles can be shared)  

단점: 활성화 비용(activation cost), 호출때문에 손실데이터가 있을 수있음. 

2) static local variable
   프로그램 실행전에 변수를 메모리할당시킬 수 있음.(실행전 컴파일 단계에서 할당)
   장점 : 빠르게 반환할 수 있고, no overhead for allocation.
   단점: 재귀호출을 지원하지 않음, 실행시간에 바꿀 수 없어서 유연하지 않음.

=> 그래서 대부분 스택다이나믹 형태를 사용하고 오버헤드가 있지만, 유연하기 때문임.  (오버헤드에 관한 내용은 다음 파트에서 설명) 

대부분의 언오는 스택 다이나믹 배리어블을 사용한다.  

### 파라미터 1) 포말 2)실
1) formal parameter: 형식매개변수
서브루틴 정의할때 헤더에 포함하는 리스트.
호출된 프로그램의 매개변수
서브루틴 정의에서 나타나는 매개변수

void (a,b) { ... }  

라고 있을때, a와 b가 형식 매개변수다. 
3) actual parameter : 실매개변수
   parameter in the subroutine call statement

void sub(int, int)  
void main {... sub(x,y);}   

라고할때 x,y가 실매개변수다. 메인에서 호출할때, 실제 전달되는 값.  

### parameter correspondence 파라미터 매칭 
총 3가지 방법이 있다.  1) 위치매개변수 2)키워드파라미터 3)포지션/키워크 keyword 파라미터(hybrid)  

1) positional parameter : 위치에 맞개 포말과 애추얼파라미터를 매칭해줌.
2) keyword parameter : 형식 매개변수에 실매개변수 값을 지칭해서넣어줌.
   sumer (len=> my_len, sum=>MySUM).
3) positon keyword parameter

키워드 매개변수는 하나이상 비어져있는 매개변수가 있으면 안됨.  


### parameter default value 
서브루틴 정의시 전달하지 않아도, 기본적으로 가지는 값을 정의함. 

포말변수와액추얼변수가 반드시 매치되면, 기본값 파라미터가 필요없음(in case of no parameter defaule value)

### 프로시저와 함수 procedure and function 
공통점: 프로그램을 모듈화(modularization - 작업단위로 나눔, 오류발생시 전체 바꾸는게 아니라 모듈별로 수정할 수 있다는 장점이 있음.), 호출프로그램에 결과를 산출하는 방법.  

프로시져 : 일련의 작업과정.  연산의 연속, 0또는 여러 반환값을 반환함.   
함수: 호출된 코드로 부터 함수를 통해 생성한 값을 반환함. user-defined operator 를 사용할 수 있음   

