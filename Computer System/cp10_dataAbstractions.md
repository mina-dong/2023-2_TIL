## 1. 기본 데이터 구조1
### 데이터 구조 - 컴퓨터에서 처리할 자료를 효율적으로 관리하고 구조화시키기 위한 학문
배열, 집합체, 포인터, 정적구조와 동적구조.  

### 정적 자료구조 static data strucutres
자료구조의 크기와 형태가 변하지 않음

### 동적 자료구조 dynamic data structures 
자료구조의 크기와 형태가 변할 수 있음
linked list

### 포인터 pointer 
데이터의 위치를 가리키기 위해 사용됨  

### 2. 기본 데이터 구조2 
### 리스트 
- 연속형 리스트 : 정적인 리스트를 구현하기 편리한 저장구조. 삭제나 삽입으로 인해 여러 항목들이 이동해야 하는 동적 리스트의 경우에는 불리함.
- 연결리스트 : 연결 리스트의 시작위치,  리스트 헤드의 주소는 별도로 저장함. 연결 리스트의 끝은 null포인터를 사용하여 표시한다.

### 스택 
항목들의 대한 제거와 삽입이 헤드에서만 일어나는 리스트, 후입선출.  
스택 포인터 : 항목 위치를 나타냄
pop 상단에서 항목을 제거, push 상단에서 항목을 삽입  

### 큐 
항목들의 삽입은 한 쪽 끝에서만 일어나고, 삭제는 반대쪽 끝에서만 일어나는 리스트임. 선입선출.  

- 헤드테일포인터를 사용한 큐의 문제점.
  항목들을 삽입하고 삭제하다보면, 큐가 메모리에서 빙하처럼 움직임. 큐가 정해진 메모리 블록을 벗어나지 않게끔 만드는 매커니즘이 필요.  
  => 순환형 큐

### 트리
항목들이 계층적 구성을 갖는 데이터 집합.  
노드 : 트리안의 항목  
루트 노드: 최상단의 노드  
단말노드 : 하단노드
깊이 : 가장 긴 경로의 길이
레벨: 루트로부터의 거리 
서브트리 : 트리의 일부.  

부모 : 현재 노드의 바로 상위 노드  
자식 : 현재 노드의 바로 하위 노드 
조상: 현재 노드 기준으로 모든 상위 노드들  
후손:  현재 노드를 기준으로 모든 하위 노드들  
형제 : 공통의 부모를 갖는 노드들.   

### 이진트리 바이너리 트리 
각 노드가 2개 이하의 자식을 갖는 트리.  
연결 리스트와 유사한 연결 구조를 사용하여 메모리에 저장, 노드는 데이터와 두개의 자식 포인터를 갖는다.  

이진트리가 거의 균형을 갖고 있고 거의 가득 차있을 때 연속형 리스트를 사용하면 효율적이다. (예시는 배열느낌임.)

## 3. 맞춤형 데이터 타입 
### 데이터 구조의 조작. 
컴퓨터 메모리에 데이터 구조를 저장하는 방식  
사용자가 생각하는 개념적 구조와 일치하지 않음!!!  

**추상화도구** 주기억장치는 리스트, 스택 등 으로 구성되어 있지 않고 주소를 지정할 수 있는 메모리 셀의 열로 구성되어 있음..즉, 이런 리스트,스택 등의 구조들은 추상적 도구임!  

### 추상 데이터 타입
데이터와 함수를 모두 포함할 수 있는 사용자 정의 자료형  

클래스 형으로 만들어진 생성되는 변수역할: 객체  

