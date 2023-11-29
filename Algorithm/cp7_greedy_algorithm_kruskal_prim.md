# 그리디 알고리즘 : 탐욕알고리즘
optimization problem 최적화 문제에서 많이 사용하는 알고리즘임.  
매 알고리즘 **스텝마다 현재 상태에서 최적의 해**를 만드는 것을 선택함.  

MST

## kruskal's algorithm 크루스칼 알고리즘 
문제: connected graph G가 주어졌을 때, G의 MST G' 찾기  
즉, G의 MST를 이루는 edge set T를 찾기.  

각 단계마다 T에 추가해도 사이클이 생기지 않은 엣지들(가용해-feasible solution) 중  
cost가 가장 작은 edge를 T에 추가하고 이 과정을 반복함.  

위 알고리즘의 결과물은 무조건 G의 vertex를 포함하게 된다.  

### 정리1  
kruskal' algorithm의 결과물 G' = (V(G),T) 는 항상 connected 하다.   
그래서 크루스칼은 언제나 Spanning tree를 리턴한다. 

증명 : G'이 connected 가 아니라 가정한다.  
v1, v2, ... vr을 G'의 connectedc component들 이라고 하자.  
G는 connected 하므로, v1상의 vertex와 v(G)-v1상 의 vertex를 이어주는 edge E가 언제나 적어도 하나 존재한다. 
해당 E를 추가해도 그래프는 언제나 사이클 하지 않다.

따라서, 크루스칼 알고리즘은 엣지E를 추가하게 되고, 나머지 v2...vr에 대해서도 마찬가지이다.  

### 정리2 
크루스칼 알고리즘은 G의 엣지들의 cost가 모두 다를때 유일한 MST를 반환한다.   
(같은 cost를 갖고 있는 엣지가 있는 경우, MST는 만들어지지만 **유일함**은 성립안함.)  

증명: T와 T'을 각각 크루ㅅ칼과 최적해(optimal solution)을 포함하고 있는 엣지 세트라고 하자.  
만약 T와 T'이 != (같지않다)면, 어떤 엣지 E = (u,v)가 T'-T에 속해있어야 한다.  

이때, 크루스칼 알고리즘에 의해 T에서 u에서 v까지의 path들을 이루는 edge들의 cost는  
모두 E의 cost보다 작다. (아닌 경우, 크루스칼 알고리즘은 받드시 E를 포함)  

따라서, T'-{E}U{E'}(E'은 T에서 u에서 v까지의 path 들 아무 엣지)의 total cost는 t'의 total cost보다 작으며, 해당 엣지들은 여전히 spanning tree를 이룬다.  => T' 최적해라는 가정에 모순발생함.  

### 시간복잡도
엣지를 비교하는데 있어 O(m log m)  
G' = (V(G),T)에 대해 DFS를 수행하여 판단, 각 엣지를 추가할때마다 최대 O(n+m).  
=> O(m log n) + O(m(n+m)) = O(m^2)

=> 크루스칼을 더 최적화 하자!! union find data structure를 이해해야함.  
