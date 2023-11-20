# categorical features : 수치값으로 바꾸는 방법

1. one-hot encoding  : 서로 다른 값을 가질때, 차이도 모두 동일하길 원할 때 사용하는 방식 - 보통 nominal feature : 성별, 부서 등에 많이 사용  
2. ordinal encoding : 카테고리가 다르면 서로 정보 차이도 다르게 주고 싶은 경우에는 ordinal feature : 선호도,학력 를 사용함.

```
train.columns[train.isnull().any()]
```
결측치 없음 확인 

0하고 1밖에 없는 것들 binary features.

```
#one hot encoding
pd.get_dummies(data =data, columns = ['abc'])
```
만약 컬럼명이 너무 많은 경우, 나중에 문제가 생길 수 있다.  


**데이터를 줄이려면? : 차원감소기법**

1. 분석에 도움이 안되는 feature 제거하기
   결측치가 너무 많은 columns, 테스트 타임 예측과 상관없은 columns, 다중공선성이 너무 높은 columns.

   이 강의에서는 테스트 타임과 예측과 상관없는 컬럼제거를 목표로 함

   nuique() 값이 유니크한지... 2가 아닌 데이터를 제거시킴. 왜냐면 바이너리 피쳐여서, 값이 하나 있거나 아예 없는건 의미가 없기(관계성이없음) 때문임.

2. PCA principal component anlaysis 가장 대표적인 방법임
   2가지의 관점에서 사용함.
   - pca feature extracion - 정보를 잘 추출해서 좋은 feature로 새롭게 만들고 싶을 때
   -   추출할 feature개수를 정해줘야함
   -   비슷하게 생긴(one-hot, 바이너리 피쳐같은) 데이터에서 잘 적용한다.
    
   
```
from sklearn.decomposition import PCA 
pca = PCA(n_components=15)
newpca = pca.fit_transform(X_train)


newdf = pd.DAtaFrame(data=newpca,  columns=[f"PC{i}" for i in range(1, newpca.shape[1]+1)])

```
추출하고 뽑아야할 피처의 개수 설정 - n components, int또는 float으로 설정함. int는 지정된 개수 세팅, float 분산된 데이터를 얼마나 보존할지에 대해 정함.  
보통 df형태로 저장함. 
n_components에 0.9라고 입력할 경우,90%만큼 데이터를 가져온다는 것을 의미한다.  

보통 15, 0.9 같은 것들을 하이퍼파라미터 라고 부른다고 함  

3. feature importance f를 이용한 중요 변수 추출
- 전처리를 하면 머신러닝을 통해 예측 모델을 만들 수 있음.
- 트리모델

```
from sklearn.ensemble import RandomForestRegressor

model = RandomForestRegressor
model.fit(X_train, train.y) 
```

학습을 하기 시작함! 551개의 피쳐와 y사이의 관계를 모델링함. (4209개의 데이터를 기반으로)

model.feature_imoportances_

합치면 1이 됨! feautre_importance 를 정렬(sortd)를 한다음, 오름차순으로 정렬해서 일부값을 가져온다
=> 이때 어디에서 어떻게 값을 가져올까? 
sotring결과의 index를 가져오는 argsort. 사용할때 뒤에서부터 가져오면 된다.

```
top15 = model.feature_importance_.argsort()[-15:]
model.feature_names_in_[top15]
```

영향력이 높은 것들을 기준으로 뽑아서 예측모델을 만들수도 있다.
