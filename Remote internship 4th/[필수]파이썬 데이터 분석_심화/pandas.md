# pandas 대용량 데이터 불러오기

**EDA 고려해야 하는 것:결측치 처리**
- 데이터가 아예 없는 경우에는 분석자체가 진행될수 없음
- 지우거나 채우거나 숫자를 채워야함
- 어떻게 얼마나 처리하는지에 따라 분석 결과가 차이남 .

판다스에서는 NaN으로 Null를 처리함. 


1. Drop Missing Values
   - row나 columns 단위로 제거함.
   - 만약 어떤 컬럼이 70% 이상없은데 이 없는값으 row를 삭제하게 되면 전체 데이터의 70%가 사라지는거기때문에, 해당 컬럼만 삭제하는 경우도.
   - 보통 50% 70% 90% 으로 본다고 함.

2. Filing missing Values
   - 평균값 채워넣기 각 컬럼당
   - ground values를 넣음(아예 0이나 -1000처럼 해당 컬럼에 없는 값을 넣어줌.)
   - near value 앞 뒤에 있는 데이터로 넣어줌.
   - KKKImputer 결측치가 있는 데이터와, 비슷한 k개의 데이터를 찾아서 평균 계산함.

# pandas 대용량 데이터 처리
```
import numpy as np
import pandas as pd

train = pd.read_csv('../input/bosch-production-line-performance/test_numeric.csv.zip')
#zip파일들은 read_csv가 자동으로 읽음.

# chunksize, nrows, usecols ..
# isnull.sum()을 사용하면 결측치개수를 알수 있음.

train.head()
```
```
train = pd.read_csv('../input/bosch-production-line-performance/test_numeric.csv.zip',
                   nrows=100)

S0_columns = train.columns[train.columns.str.contains('S0')].tolist()
#tolist = 함수로 변환가능 

usecols = ['Id'] + S0_columns + ['Response']

usecols
```

```
train = pd.read_csv('../input/bosch-production-line-performance/train_numeric.csv.zip',
                   usecols=usecols)
train
```

```
train.fillna(0) #결측시를 모두 0으로 채움

```



```
#빠른 저장이 가능한 parquet-fanily

train.to_parquet('train.pqt', index=False)

train2 = pd.read_parquet('train.pqt')
train2
#cSV보다 속도가 더 빠름.
```

# cuPF : gpu ... cupf는 사용하면 원본데이터가 변환됨. 
setting - accelerator 에서 gpu p100으로 바꾸면, cpu사용을 줄이고 gpu사용을 함.   
 해당기능은 일주일에 33시간만 제공함.  