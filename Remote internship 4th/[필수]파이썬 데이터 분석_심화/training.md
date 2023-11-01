# cafe
kaggle에 csv 업로드할 때,  duplication data라고 나오는 경우가 있다. 이때 skip 말고 included duplicate files을 선택한다.   

##  csv 불러오기

## 데이터 추출
데이터가 많은 거에 비해 실제 사용할 데이터가 많지 않기 때문에 일부 데이터만 추출하는 작업을 함.

.value_count() 를 통해서 해당 하는 값이 얼마나 있는지 확인한다.  

usecols = ['사용할열']  속성을 부여해서 필요한 데이터만 추출한다.  

## 여러개의 csv 불러오기
glob을 이용해 사용한다! 

from glob import glob  
file_names = glob('../input/*.csv')  

total = pd.DataFrame()

for file_name in file_names:
  temp = pd.read_csv(file_name, usecols = [['col1','col2']])  
  total = pd.concat([total,tmp])

## 시간이 오래 걸리는 작업을 할때 프로그래스 바를 사용할 수도 있다.  

## import gc
메모리 낭비를 막기 위해 gc를 한다.  

# manufacturing : 대용량 데이터 처리

## 데이터 일부만 불러오기
어떻게 데이터를 줄일까?(데이터 일부만 쓰는 방법)
1.  read_csv 에서 chunksize=10000을 부여한다.

2. nrows =1000 속성 부여하기 

언더샘플링, 오버샘플링, 하이브리드 어프로치의 방법이 있다.   

샘플링을 하기 위해서는 전처리가 필요함!  => 결측치 처리 우선!  

filna(0) 을 이용하여 값이 없는 곳은 0으로 채워진다.  

1. 언더샘플링 : 메이저리티 클래스(데이터가많은) 수를 마이너리티클래스(데이터가적은)에 개수를 맞춤

if samplig == 'under': (세가지 방법을 사용하기 위해 samplig에 대한 값을 수정할 수 있음.)
  sample_nomal= nomal.sample(n=len(abnormal), random_state = 42)


2. 오버샘플링
if samplig == 'over':
  from imblearn.over_sampling import SMOTE
  X = train_numeric.drop(['ID', "res"]) # feature vecotr
  Y = train_numeric["res"] #target value

  X_over, Y_over = SMOTE().fit_resample(X,Y)
  
3. 하이브리드 어프로치
if samplig == 'hybrid':
  N =1000 ... 생략. 