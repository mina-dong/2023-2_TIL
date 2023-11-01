# seaborn
matplot 라이브러리를 쉽게 쓸 수 있게 만들어진 라이브러리.
데이터프레임과 호환이 잘된다. 

### histoplot : 연속적인 데이터를 확인할 때 사용함
sns.histplot(data=df, x="x", bins=30) 

bins속성을 통해 구간을 조절할 수 있다.(더 늘리는 방식)  
### barplot : 어떤 데이터의 값의 크기를 막대로 보여주는 plot 

### countplot 
hue라는 파라미터를 넣으면 정보차이를 색상으로 표현함. 

### boxplot : e데이터의 각 종류별로 사분위 quantile 를 표현한다.  
박스플롯 안의 선은 중앙값에 해당함.    
iqr 기준1.5배를 표시한 것.   

### lineplot : 특정 데이터를 x,y로 표시하고, x의 변화의 y의 변화(관계)를 확인할 수 있는 plot  

ci=none 속성을 추가해 필요없다면 추세를 삭제할 수 있음.  


### scatterplot : line과 비슷하지만, line은 경향성을, scatter는 데이터의 분포를 확인할 수 있다. 

### pairplt : 주어진 데이터의 각 feature 들 사이의 관계를 표시하는 plot임. 모든 수식값의 pair에 대해 한번에 계산하는 plot임.  

각 피쳐에 대한 계산된 모든 결과가 나오기 때문에, 피쳐가 많은 경우 적합하지는 않다.  

### 상관관계 heatmap 
corr()를 이용해 우선 처리한다. 밝을 수록 1, 어두울수록 -임. 
anoot=True 부여하면,  숫자를 표현한다.  


df.columns = ["col1", "col2"]  
한글 컬럼 명은 오류가 나기 때문에 이 방법처럼 바꿀 수 있다. 단, 순서를 잘 지켜야 한다.  