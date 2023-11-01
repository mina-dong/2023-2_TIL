
# Numpy 넘파이를 이용해서 산술계산하는 방법. 


이진법으로는 0.1도 제대로 나오지 않음
-> 부동 소수점 산술

그러면 최대한 근사값을 표시하자!
float를 사용할 때 넘파이에서는 두가지 형태
single percsion(32비트) 과 double perision(64) 을 제공함.  


```
import numpy as np


# 1. python
3.14 - 4 #output : 0.85999...

# 2. numpy
np.array([3.14]) - np.array([4])  #output: array([-0.86])
```

numpy내부에 이런 불안정인 것들을 처리하는게 있어서 이런 오차가 더 적어지게 표현함. 

머신러닝이나 딥러닝 같은 계산이 많이 있는 분야에서는 파이썬과 넘파이를 비교했을 때 그 오차범위가 크게 차이나는 편임.  


# Numpy 벡터연산 : 원소들끼리 더해지는 것.

vector.shape 의 결과가
(3, ) 이 나온다면 한줄짜리 벡터임.  3개가 들어있는.


벡터에는 원래 곲하는 연산이 없지만
numpy에서는 지원한다 elementwise division


# indexing 벡터에서 특정 위치의 원소를 가져오기

리스트에서 제공하는 slicing 등을 지원함.


```
#arr 의 2row, 3columns

arr[1][2] #python list indexing
arr[1, 2] #numpt array indexing
arr[:,2] # 모든 인덱스를 다 가져옴

# 두번째 row
arr[1, :] # 첫번째 행에 있는 모든 컬럼들
```

# Aggregation : 집계함수

np.random.seed(42) : 랜덤함수를 고정함 : 기본 seed값이 clock기준이기 때문에 이런식으로 (필요하다면) 고정할 수 있음. 

최소값이 있는 index  vec.argmin(axis=0) , 최대값이 있는 index vex.argmax(axis=1)

오름차순 정렬만 지원하는 vec.sort()

인덱스를 정렬 .argsort() 

# mathematics

np.random.randn(5,3)
파라미터에 따라서 해당 행렬을 만든다. 5*3의 행렬 생성.  


abs
sqrt
만약 runtimewarning , nan 이 보인다면 원소에 복소수가 있어서임. 

np.linalg.norm(vec)
np.linalg.eig()


# universal function
넘파이가 기본적으로 어떤 연산을 할때, 더 확장해서 연산을 처리할 때... 사용.
행렬곱 연산을 할 때 편리함!

arr = [1,2,3,4]

2행 4열의 행렬

arr2 = [0,1,0,-1]

(4,) 의 행렬

개의 배열을 더해보면? 서로 차원이 다르면 맞는 부분을 이어서 자동으로 계산함
예) arr + arr2 = [[1,3,3,3],[1,1,-1,-1]]



(arr * arr2).sum(axis=1) 

(2,4) * (4,1) = (2,1)


만약 확장하게 된다면? 
f = lambda x : 1/x 일때,

1/arr2

universal funcion : 어떤 연산을 어떤 넘파이 어레이에 제공해주면, 자동으로 모든 원소에 자동으로 적용해주는 것. 직접 뒤집어 assgin하는 것보다 해당 연산 기능을 이용해 하는 것이 더 빠름. 

# numpy로 논문 수식 구현하기 
cosine similarity 벡터 2개 사이의 유사도를 측정하는 방법임.  

arr = np.array([1,2,3,4])
arr2 = np.array([0,1,0,-1])

cosine similarity

def cosine_sim(v1,v2):
	*v1_norm = np.sqrt(np.square(v1).sum())*
	a = np.linlg.norm(v1) * np.linalg.norm(v2)
	b = v1 @ v2
	return b / a

cosine_sim(arr, arr2)
	
*output : -0.255829889...*


# neural 네트워크 구현에 사용되는 ReL U

RelU : 인공 신경망의 관점에서 들어온 값ㄷㄹ의 양의 파트만 남겨주는 함수. 

음수를 0, 양수를 x값 그 자체로 나오게 해야함.  

x = np.array([0.7,0,-0.5,0.3])
def relu(x):  
	if x >= 0:  
		return x  
	else:  
		return 0  

 넘파이 어레이에 조건식을 넣어 수행하면, 해당 인덱스만 뽑혀서 나옴

x[x>=0]  
또는,
x[x<0] 이라고 사용할 수도 있다. 

x[x>=0]=0 이렇게 사용하면 벡터의 원소중에 음수인 숫자를 0으로 만들수 있따.


