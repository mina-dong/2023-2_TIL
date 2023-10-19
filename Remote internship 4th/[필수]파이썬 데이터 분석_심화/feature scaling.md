# 데이터 가공 방법 ㅣ feature Scaling
서로 다른 feature들이 값을 가지는 범위가 달라 모델링에서 문제가 발생할 수 있음.
피쳐끼리 비교 가능하려면, 동일한 범위내에 존재해야함  

서로 feacture scale이 안되어있다면 각각 다른 단위이기 때문에 비교할 수가 없음.  
만약 클러스터링 한다면 피처스케일(비슷하게 스케일을 맞춰주는 일)해야함.   
```
import pandas as pd

train = pd.read_csv("../input/dacon-elec-usage-prediction/train.csv", encoding = 'cp949')
```

**에러 발생**
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xc0 in position 14: invalid start byte  

한글데이터가 존재하는 경우, 캐글노트북에서 돌아가는 환경이 아닐때 발생함.   
이때 encoding = 'cp949'를 입력하자.  


거리 기반의 모델들은 클러스터링 영향을 많이 끼침.  
두 가지 방법의 스케일링이 있음.   1. minmax scaling 2. standard scaling  


```
# 1. minmax scaling 
from sklearn.preprocessing import MinMaxScaler

# minmaxscaler를 사용하겠다는 선언하기
scaler = MinMaxScaler()

# scaler.fit_transform : 데이터를 넣으면 지정된 데이터를 찾아줌.
#인덱싱을 해와라...할데 괄호 [[ 잊지말기 ]]
X =scaler.fit_transform(train[['기온(°C)','풍속(m/s)','습도(%)','강수량(mm)','일조(hr)']])
X # 0부터 1사이의 값으로 나타내줌.

X = pd.DataFrame(data=X, columns =['기온(°C)','풍속(m/s)','습도(%)','강수량(mm)','일조(hr)'] )
X
```


```
#2. standard scaling
from sklearn.preprocessing import StandardScaler
# 평균과 분산으로 처리해주는 StandardScaler
scaler = StandardScaler()

X2 =scaler.fit_transform(train[['기온(°C)','풍속(m/s)','습도(%)','강수량(mm)','일조(hr)']]) 

X2 = pd.DataFrame(data=X2, columns =['기온(°C)','풍속(m/s)','습도(%)','강수량(mm)','일조(hr)'] )
X2
```


```
#StandardScalerd 가 잘 되었는지 확인하는 방법? -> 평균값 거의 0 이어야함 
# std는 1. 정확히는 1이 맞긴한데, 컴퓨터가 1을 표현못해서 가까운값이 나옴.

X2.mean()
X2.std()
```