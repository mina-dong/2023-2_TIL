```
import numpy as np

arr1= np.array([1,2,3])
arr2= np.array([4,5,6])

#vector addition - 리스트끼리 더할때는 결합형식인데, numpy는 적용되지 않음.
print(arr1+arr2)
```

```
arr1= np.array([1,2,3])
arr2= np.array([1,2,3,4])

print(arr1+arr2)
# output : ValueError가 발생함. 즉, 연산이 불가. 
```

```
#절대값 abs
arr = np.array([-1,2,-3])
np.abs(arr) 

#제곱근 
np.sqrt(arr)

#마이너스는 허수이기때문에, 오류발생! 
```

```
#shape 알아보기
arr1= np.array([1,2,3])

arr2= np.array([[1,2,3],
              [1,2,3]])

#2by 3by 4 ; 4차원 벡터가 3개 있는것이 2개 잇음.
arr3= np.array([
    [[1,2,3],
    [1,2,3],
    [1,2,3]],

      [[1,2,3],
      [1,2,3],
      [1,2,3]]])

print(arr1.shape,arr2.shape,arr3.shape)

#output : (3,) (2, 3) (2, 3, 3)
# 원소가 3개 / 원소가 3개인 리스트가 2개 /  원소가 3개인 2차원 리스트개가 2개
#1d vetcor 2d matrix 3d tensor
```

(3,) != (3,1)  
서로 같은게 아님을 확실하게 알자!
