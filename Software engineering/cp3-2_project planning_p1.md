# project planning

1. what is project planning
2. software pricing
3. plan driven development
4. project scheduling
5. agile plannng
6. estinamation technique
7. cocomo cost modeling(중요하지는않음)

## project planning? 
프로젝트 관리는 breaking down the work  하는일을 쪼개고, 팀 멤버를 배정하고 assgin, 문제를 예측하고, 불확실한 솔루션을 준비한다. tentative solutions  

프로젝트가 시작되고 프로젝트플랜이 생성되었을때, 프로젝트 팀에에 **어떻게 일을 끝낼건지** 소통하는데 사용되고, 사용자가 프로젝트의 진행사항을 평가하는 걸 도운다. 

### planning stages 
프로젝트 라이프 사이클에서..  
proposal stage에서, 개발 계약 또는 소프트웨어시스템 제공을 위해 입찰한다. 
project starup pahase 동안, 프로젝트가 어떻게 점진적으로 세분화 할것인지, 자원은 어떻게 할당할건지를 정해야한다.  
프로젝트 중간에, 계획을 수정할 때 진행 상황을 모니터링함으로써 얻은 것으로 부터 

[proposal planning  제안 단계 ]  
계획은 소프트웨어 요구사항의 개요가 필수적이다.  
고객이 시스템의 비용을 산정하는 데 사용할 수 있게 정보를 제공하는 목적이 있다. 
개발이나 임금, 하드웨어 비용 등 프로젝트 예산을 산정한다.  

[project startup planning 프로젝트 시작 단계]  
이 단계에서 시스템 요구사항에 관해 더 알게되지만, 설계나 구현 정보는 아니다.  
프로젝트 예산이나 인력에 관해 충분히 상세하게 계획을 만든다.  
이 단계에서 매커니즘을 모니터링을 정의해야한다.  
스타트업 플랜은 프로젝트에 자원을 할당하기 위해 애자일 개발론이 필요하다.  

[development planning 개발단계]
프로젝트 플랜 중간중간 고치며(amended)  
프로젝트 스케듈, 비용 산정과 리스크는 정기적으로 바꾼다 revised

## software pricing 
### softwar pricing? 소프트웨어 가격을 어떻게 결정하는지 
출장이나 하드웨어 같은 비용을 모두 포함해야함. 트레이닝도 물론 포함.   
비용을 산정하는건 쉽지 않다. not a simple!  
경제적, 정치적, 같은게 영향을 준다.

### 소프트웨어 가격선정에 영향을 미치는 요인 factors 
계약조건 : sw만 주는거랑 코드포함에서 주는거랑 다르다.  
비용추정의 불확실성 : 비용에 대해 불확실하게 산정하는 경우에는 추후에 비용이 더 올라갈 수 있다. 앞으로 돈이 더 들어갈 걸 생각해서 예산을 잡아야한다. 
재정건전성: 재정건정성에 문제가 있는 경우에, 다른 회사에 비해 낮게 입찰해야한다. 현금의 유동성을 유지하기 위해서, 낮게 입찰할 수 있다. cash flow 
시장기회: 새로운 시장으로 진출하기 위해 타 회사보다 더 낮게 책정할 수 있다.  
요구사항 변동성 : 요구사항이 변동될거 같으면 낮게 책정해도 된다. 나중에 요구사항이 변경하면 추가적으로 비용을 지불할 수 있게 한다. 

### pricing strategies 
가격을 책정할때 크게 두가지 전략이 있다. 
1) under pricing 개발비용보다 낮게 책정 : 우선 계약을 수주하고 개발해서, 새로운 가능성을 엿보기 위해서 개발 비용을 낮게 책정할 수 있다.
2) increased pricing 개발비용보다 높게 책정: 추가적인 리스크를 비용에 포함시켜서 높게 측정할 수 있다.

### pricing to win 가격합의를 잘 하는 법
- 고객이 내고싶은 만큼의 가격을 책정해야함.
- 개발에 대한 cost가 낮으면 퀄리티가 낮을 수 있기 때문에 나중 릴리즈를 추가할 걸 생각해서 책정할 수 있다.
- 계약서를 쓸때 요구사항이 변경되면, 추가적인 비용이 들 수 있다는걸 산정해 놓아야 한다. 

## plan-driven development 
전통적인 소프트웨어 개발론의 하나임.  
전통적인 공학 - 건축공학 - 전형적인 공학에서는 설계 그대로 건축을 하는데 정석적인데, 소프트웨어의 경우 하면서 요구사항이 바뀌는 경우가 많음. 그래서 전통적인 공학과 다른 방면이 있다.  

### 플랜드라이븐개발론.  
- 프로젝트 계획은 소프트웨어가 시작될때 생성이 되고 계속 관리가 된다.
- 프로젝트 관리하는 사람은 계획을 사용해서 프로젝트에서 없던 사항이 있을 경우 수립을 하고, 계획을 통해 진행 상태를 확인한다.
즉, 계획이 완벽하게 짜여져 있는 경우에 해당하다.

[장점]  
- a개발자는 이 프로젝트만 6개월 동안 할거야, 같은 내용이나 비용 고정 등. 조직적으로 발생할 수 있는 이슈에 독립적으로 개발할 수 있다.
- 계획을 상세하게 설정하기 때문에 상세하게 기술해놓아서 문제가 생겼을때 대처할 수 있음. 

[단점]  
- 요구사항이 발생했을 때, 반영하기 어렵다.

### project plan 프로젝트 계획
소프트웨어 프로젝트를 개발하는 데 있어 필요한 자원을 미리 정하는 것을 의미함. 
introduciton, project organization, risk anaysis, hardware and software resource requirement, work brakdown, project schedule, monitroing and reporting mechanisms

위 내용들이 문서화되어야함. (당연히 들어가야하는 내용)
### project plan supplements 부가적으로 필요한 것
형상관리 계획: 버전관리.  소스관리를 어떻게 관리할 건지.
배치계획: 특정 소프트웨어가 특정 하드웨어에서 실행되는 경우.  소프트웨어 분포가 어디어디 분포해야하는 경우, 그런 배치를 어떻게 할건지  
유지보수 계획:  
품질 계획:  
검증 계획: 소프트웨어가 잘 만들었는지 어떻게 검증할건지. 

### project planning process 프로젝트 계획 수립 프로세스. 
스타트업 단계에서 결정이 도지만, 프로젝트 계획 변경은 일어날 수 밖에 없다! 중간중간에...  
계획 기반에 개발론일지라도, 중간에 프로젝트 계획을 재정하고 새롭게 바뀐 요구사항을 추가하고 지속적으로 수행해야한다.  
비즈니스 목표가 바뀐 경우,프로젝트 내용도 바뀔 수있다.  

[planning assumptions(반드시 계획시 고려해야할 점)]
- 낙천적으로 생각하지 말고,현실적으로 생각해야한다.
- 문제는 언제든지 생길 수 있기 때문에, 프로젝트가 지연될 수 있다는 점을 인지하고 있어야한다.
- 예상못한 문제가 발생할걸 생각하고, 일정을 조율해야한다.

[risk mitigation 위험을 줄이는 요소]
- 일정이 심각하게 늘릴거 같다면,리스크를 줄이는위험완화를 해야한다.
- 최악의 경우, 재계획을 수립할 수 도 있다.
- 고객에게 다시 협상할 수도 있다.(미래 피해를 방지하기 위해서)
- 사전에 발견하고, 조치를 한다고 했을 때, 고객과의 계약조건 등을 통해서 위험을 타개할수 있다.

**즉 프로젝트계획은 현실적으로 해야한다**