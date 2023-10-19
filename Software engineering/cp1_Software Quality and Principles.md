# cp1_Software Quality and Principles

---
1. 소프트웨어란?
2. 소프트웨어공학이란?
3. 개발소프트웨어의 특징
4. 소프트에어공학의 상세적인내용
5. Divergence of software
6. 소프트웨어공학윤리

---

## 1. 소프트웨어란?

### software in nowadays
- 선진국(developed nations)일수록 SW에 의존적이다.( dependent on SW)
- 소프트웨어로 대부분 통제함
- 소프트웨어공학은 이론, 방법, 툴을 다룸. 프로페셔널한 소웨 개발을 위해서.
- 소프트웨어에 대한 지출은 상당한 부분을 차지함(Expenditure on software represents a significant fraction 
of GNP(: Gross National Product) in all developed countries)


### 소프트웨어정의
프로그램과 소프트웨어의 차이

프로그램:  명령어 집합
소프트웨어 : 프로그램뿐만 아니라, 소프트웨어 개발동안 모든 산출물들을 포함함. (데이터구조나 db, 유저메뉴얼, 테스트결과 등)

### Characteristics of Software
- Individual abilities (developer's ability) can affect 
productivity of software development. 
- 개개인의(각 개발자의 능력) 능력이 소프트웨어개발 생산성에 영향을 미칠수도 있다.

- 개발과 생산의 차이점? 개발은 새로운 걸 만들어가는 프로세스(절차)임. 생산은 무언가를 만들고, 큰 규모의 물건을(goods)를 생산하고, 보통 공장에서 주로 쓰임.

- 하드웨어는초기 실패비율이 높지만, 오류수정이후에 길게 사용할 수 있음. 하드웨어의 실패(failure)는 환경요인(dust,heat..)때문에 급격히 오른다.
- 하드웨어와 달리, 소프트웨어는 파트별로 데미지를 받지 않음(즉, 환경이 소프트웨어에 영향을 받아도 작음)
- 이상적인 소프트웨어 커브(idealized softwar curve)를 보면, 실폐확률(failure rate)은 에러 수정이후에 떨어지고 있음 - 즉, 하드웨어와는 다름
- 소웨는 단계별로 요구사항을 반영9reflect)할 수 있음.
- 변화들은 패일레이트를 상승시킬 수도 있음.

  => 그치만 이상적으로는 소프ㅡ웨어가 시간들이고 고치면 더 완벽한 소프트웨어가 나온다곤 하지만, 실제 끝지점에 가면 소프트웨어자체를 폐기하거나, 아예 새로 만드는 경우가 많다고 함.

### Software problems to solve

1. 소프트웨어 발전 느림.- 970년도부터 하드웨어는 발전해왓는데, 그에 비해 하드웨어와 비교해서 개발속도가 느린편임(=발전속도), 물론 소프트웨어도 계속 진화하고 있지만 하드웨어에 비해 발전이 느린편임.

2. 새로운 소웨의 유저 수요 증가.(Increasing user demand for new software-demand for 수요) - 하드에어는 노은 생산성인데, 소웨는 낮은 생산성을 가지고 있음.

3. Partial use of management techniques(관리기술 부분사용) - 소프트웨어개발에는  관리기술이 필요함(requires), Exhaustive(철저한) management via 
Project Management Knowledge System (PMBOK).

### Software costs
- 소프트웨어 비용은 컴퓨터 시스템보다 넘어선다(dominate)
- 소프트웨어 비용은 개발하는것보다 보수하는데 더 많이 든다.
- 소프트웨어 공학은 소프트웨어 개발을 비용절감적(cost-effective)하게 관리해야한다. (concerned with)

### Software crisis?
Software crisis is a term used in the early days of computing science for the 
difficulty of writing useful and efficient computer programs in the required time.

소프트웨어 crisis..위기는 이 CS에서 사용하던 용어로, 유용하고 효과적인 컴ㅍ터프로그램을 요구된 시간내에 작성하는데 어려움이 있음.  

> 예, 증가하는 요구사항, 증가하는 복잡도, 증가하는 어려움, 같은 인적자원, 같은 개발 메소드, 같은 툴.

### 2 major reasons of SW project failure 소웨프로젝트 실패의 주된 이유 2가지

1. Increasing system complexity (시스템 복잡도의 증가)
- 새로운 소프트웨어공학 기술은 더 크고 더 복잡한 시스템을 만들 수 있도록 도와줌. 요구사항 변화에 맞게.
- 시스템은 복잡한 시스템을 요구했더라도, 빠르게 만들고 도달되어야함.
- 시스템은 이전에 불가하다고 했던 기능들이 이번 새 기능으로 갖고 있어야함.

2. Failure to use software engineering methods
- 소공 메소드나 기술 없이, 컴퓨트프로그램을 작성하는건 실패로 가는 지름길임.
- 많은 회사들은 포르덕트나 서비스가 진화함에 따라, 소프트웨어 개발이 쌓이고 있음(drifted)
- 매일 소웨엔지니어링 메소드를 사용안함

=> 결론, 그래서 (소웨엔지니어랑 메소드를 사용안한) 소프트웨어는 더 비싸고, 신뢰성도 안좋은 점을 갖게됨.


## 2. 소프트웨어공학이란?

### 엔지니어링이란
- 다리, 길 기계 같은거 포함해서, **과학적인 원리**(scientific principles)에 기반하여 설계하고 짓는걸 의미함. (design and build)

-  developing engineering은 엔지니어링 원리(engineering principles)를 개발하고, 문제를 해결하기 위한 스킬을 축적함.(accumulate)

- 엔지니어링 원리를 적용하는건 상세한 문제를 해결하기 위한 procedures와 standard 표준을 만듦

### 소프트엔지니어링(소프트웨어공학)
소웨+엔지니어링 = 소웨 개발 프로세스에 엔지니어링 원리를 적용시키는 것.(엔지니어링은 과학적이고mathematical한 원리)

=> 소프트웨어개발어려운거 해결, 개발 메소드를 통해 효율적이고 생산성 향상, 유저만족도 증가.

- software engineering :  engineering discipline(분야, 규)은 그게 우리가 사용한 이후(after it has gone into use) 시스템을 보수하는 것을 통해 시스템 초기 사양부터 소프트웨어 프로덕션의 측을 다루고 있다.
-  an engineering discipline that is concerned with all aspects of software production from the early stages of system specification through to maintaining the system after it has gone into use.
-  engineering discipline : Using appropriate theories and methods 
 to solve problems bearing in mind organizational and financial constraints(문제를 해결하기 위해 적절한 이론과 방법을 사용함-조직적, 재정적 제)
- 기술적인 개발과정 뿐만 아니라, 프로젝트 관리나 도구, 소프트웨어를 지원하는 방법도 포함한다.

### SW 엔지니어링의 중요성
- Dependency of SW : 소프트웨어 의존도. 개별적 그리고 사회적으로 소프트웨어 시스템에 의존하고 있다(더 많이), 빠르고 경제적으로 시스템을 신뢰적이고 믿을만한 가치가 있게 생산produce해야한다.
- Cost Saving : 비용절약. 개인 프로그래밍 프로젝트를 작성하는 것보다, 소프트웨어시스템으 ㄹ위해 메소드와 기술을 사용하는게 보통 더 저렴하고 더 길게 할 수 있다.  대부분의 시스템 유형에서 after it has gone into use(소프트웨어가 사용된 후), 대부분의 비용은 **시스템을 변경하는 비용**임

## 3. 개발소프트웨어의 특징
### Software Process Activities

**Software specification (명세화) - Software development (개발) - Software validation (검증) - Software evolution (진화)**

- 명세화 : where customers and engineers define the software that is to be produced and the constraints(제약) on its operation

specification -> design ->coding(implementation) -> Verification -> maintenance -> specification...  = > software development  


### General issues that affect SW 4가지
- eterogeneity : 이질성
  > 점진적으로, 시스템은 컴퓨터와 모바일 디바이스의 차이를 포함해 네트워크를 통해 분산된 시스템을 작동할 수 있는게 요구되고 있다.
- usiness and social change
  > 비즈니스와 사회는, 빠르게 변화하고 있다. 경제적인 성정과 새로운 기술의 결합때문에
  > 그래서 빠르게 새로운 소프트웨어를 개발하고 변화할 필요가 있다.
- Security and trust (보안과 신뢰)
- Scale 규모

## 4. Details of Software Engineering