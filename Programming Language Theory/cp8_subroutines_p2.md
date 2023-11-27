# subroutine 부프로그램

## 2. local variavles and parametres(이어서)
### parameter passing - semantic model 매개변수 전달
1. In-mode 인모드 : 실매개변수로부터 형식 매개변수를 받음. recive  
2. out-mode 아웃모드 : 형식매개변수가 실 매개변수에게 전달함. pass  
3. Inout-mode 인아웃모드 : 완성될때까지 실매개변수한테 형식매개변수를 받고, 실매개변수든 다시 데이터를 돌려줌.(pass data back to actual parameters)  

**two conceptual models of data passing**
1. 물리적으로 실제 값을 전달함(직접적) - physically pasing the actual value  
2. 포인터를 통해 전달함(간접적) - passing and access path

### five methods of parameter passing :다섯가지 방법
인, 아웃, 인아웃 * 밸류, 포인터의 조합임  
1. pass by value  
2. pass by result  
3. pass by value-result  
4. pass by reference  
5. pass by name

### pass by value (인모드*값)
- 실제 값을 전달해서 형식 매개변수에 사용한다.  
- 서브루틴이 끝났을때, 형식 매개변수의 값은 실 매개변수에 **반환하지 않는다** 
- 추가적인 메모리 공간과 pass operations이 요구됨.
예)
 ```
 void swap1(int a, int b){
 int tmp;
 tmp = a;
 a = b;
 b = tmp;
 }

 void main(){
  c= 10;
  d = 20;
  swap1(c,d)
 }
 ```

 위치매개변수 방식으로 매칭됨( 형식 a -> 실 c, 형식b -> 실d)  
 위 예시에서 swap1이 실행되도, c=10, d=20으로 실제로는 swap되지 않는다. 
 
 ### pass by result
 - 아웃모드*값
 - 서브루틴이 다 실행된 다음에, 실매개변수로 전달된다.
 - 메모리 공간과 copy operation이 요구됨.
```
void sub(int x){
x = 30;
}

void mian(){
int a = 20;
sub(a);
print("%d", a);
}
```
a는 30으로 출력됨(outmode지원) - 직접적으로 return을 명시하지 않음에도.  
c언어로 실행시 a는 20으로 출력됨. outmode를 지원하지 않기 때문에!  

**일관성이 없다는 문제점이 발생함!**
아래 예시를 살펴보자 
```
void sub(int a, int b){
a = 30;
b = 40;
}

void mian(){
int x = 20;
sub(x,x);
print("%d", x);
}
```
이럴 경우 x는 무슨 값이 발생할까? 위치매개변수 방법으로 매칭되면, 첫번째 x는 a가, 두번째 x는 b가 매칭될 것이다. 따라서 x는 30과 40이라는 값을 갖게 되는데...  
이때 모호성이 발생한다!!!  

 ### pass by value-result
 - 인아웃 * 값  
 - 실매개변수 - > 형식매개변수  
 - 서브루틴이 끝날때, 형식매개변수 -> 실매개변수

```
main(){
 c= 10;
 d = 20;
 swap2(c,d);
}

procedure swap2(a:in out integer, b: in out integer) is
temp : integer;
begin
temp := a;
a:= b;
b:= temp;
end swap;

// c, d remain unchanged until return. : 반환하기전까지 c와 d는 바뀌지 않음
```
서브루틴이 끝나야, c와 d가 바뀜( c= 20, d=10)  
패스바이밸류는 인모드고, 패브바이밸류리절트는 인아웃모드임.  
**문제점! assignment order - outmode의 고질적인 문제점**

```
main(){
x=10;
y=20;
sub(x,y,y);
}

proceduer sub(a:in out integer, b:in out integer, c:in out interger) : is
begin
a:=1;
b:=2;
c:=3;
end sub;
```
x = a, y=b, y=c 인데 이때 y의 값은?! 

 ### pass by reference
 - 인아웃모드 * 간접접근_포인터
 - acces path를 통해서 실매개변수에 접근을 함.
 - 공간 및 시간이 효율적
 - 그치만, **access speed is relatively slow**
 - Aliases can be generated.

### pass by name 
- 인아웃모드
- 서브루틴내 모든 형식 매개변수가 실매개변수로 대치됨 replace
- 사용하기도 어렵고 가독성이 안좋음.


### binding
- shallow binding
- deep binding
- ad hoc binding

## 3. overloaded / generic subroutines
오버로드 서브루틴 : 서브루틴은 같은 이름일 수는 있으나, 다른 기능을 가지고 있어야함.  
실 매개변수에 기반해서, 오버로드 서부루틴을 결정함.  
= 즉, 파라미터로 구분한다.  


generic subroutine : 범용 부프로그램(ploymorphic 다형성, 여러 형태로 바꿀 수 있다.)  
다양한 데이터 타입의 파라미터를 사용할 수 있음.  

## 4. operatior overloading and coroutine
연산자도 오버로딩 할 수 있다.  

### coroutine 
- 서브루틴의 한 종류.
- caller 코루틴과 callee코루틴이 같은 레벨에 있음 . locateed
- 코루틴들은 코루틴에 제어에 의해 여러 entry point를 가지고 있음
- 주어진 시간에, 오직 하나의 코루틴만 실행됨.
- history sensitive
- 스태틱 로컬 변수임 !

동시에 영향을 주면서 병행적으로 실행됨(=동시에 실행되는 것이 아님)   
즉, 제어권이 왔다갔다하면서 비동기적으로 실행된다.  
a 서브루틴을 실행한다고 b 서브루틴이 멈추는 것은 아님.  

