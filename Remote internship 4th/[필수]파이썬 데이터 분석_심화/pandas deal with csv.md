# pandas 데이터 다루기

pandas 공식 홈페이지에서 참고할 것. 
csv, json, html, xml.. 등등 여러가지를 read할 수 있음.  

판다스는 정형데이터에 특화되어서, 대부분의 정형데이터에는 사용가능함.  

데이터 프레임이 2차원 테이블이고 테이터 한 줄을 시리즈라고 함.  

read_csv에서 parse_date를 통해서 데이트타임 형식으로 바꿀 수 있다(parse_dates=['바꾸고 싶은 열'])  

nrows= 숫자, 와 usecol=['사용하고 싶은 열']만 선택할 수 있다.  

# pandas 함수 - statistics 통계량 측정함수
correlation coefficiet 피어슨 상관계수 
두 개가 동시에 올라가면 +, 하나는 올라가고 하나는 내려가면 -  

```
df.corr()
```

# pandas 함수 - Pivot Table
피벗테이블이란 기존 테이블 구조를 특정 열을 기준으로 재구조화한 테이블임.  
주로 어떤 열을 기준으로 데이터를 해석하고 싶을 때 사용함.  

pd.pivot_table(data = df, index="",value="")  
인덱스를 기준으로 밸류의 평균 값을 가져옴. 

=> 일부 값에만 치중할 수도 있은 경우도 있음.

pd.pivot_table(data = titannic, index="Pclass",value="Survived", aggunc=['count','sum', 'mean'])  
aggunc를 이용해서 보고싶은 값을 설정할 수 있다.  

pd.pivot_table(data = titannic, index=["Pclass",'sex'],value="Survived", aggunc=['count','sum', 'mean'])   
두 가지 컬럼을 보고 싶을 경우 위처럼 처리할 수 있다.   

# pandas 함수 - fancy indexing
특정 조건에 부합하는 값을 찾음(search와 비슷함)

df.loc 특정 인덱스가 가지고있는 값을 가지고올수있음. 

df.loc['ROW에 대한 조건', 'COL'에대한조건'] 
df.loc[['1,2'],['co1,col3']] **대괄호유의**
df loc은 2차원 인덱싱도 가능하다!   
여러개를 작성할 수 있고,  
슬라이싱도 가능하다!  

df.loc[0:2, "col1":'col6']
인덱스 value의 시작: 끝 기준임 슬라이싱과 비슷하지만, 양끝데이터도 포함하고 있다.  


만약 co1에 해당하는 값 중 0보다 큰 값을 가지고 있는 데이터를 출력하고 싶다면, 다음과 한다.  
판다스은 넘파이를 기본적으로 탑재하고 있어서, 한번에 연산할 수 있게 표현된다. 

df['col1'] > 0  
- output : 0보다 큰 값을 가진 데이터만 T/F 라고 나옴.  
조건식에 따라 만들어진 마스크를 boolean mask라고 하며, 데이터 필터링에 사용한다.  


df.loc[df['col1']>0, "col2"]   
col1이 0이상인 col2만 출력도 가능하다.     

df.iloc은 인덱시만 가능한데, 조건은 불가하다!  

< 실습 >
1. 생존자만 추출
df[df["Survived"]==1]

2. 생존자들의 나이만 추출
df.loc[df["Survived"]==1, "Age"]

3.  요금을 100 이상 지불한 사람들의 Name, Pclass를 추출.
df.loc[df["Fare"] >= 100, ["Name","Pclass"]]

df[df['찾고싶은열']].str.contains("찾고자하는문자열")]

4. 결측치를 포함하는 모든 데이터를 추출
df.isnull().any()
any는 방향을 갖는다! 이 안에 속성에 axis=1, 0 을 설정해서 행이나 열의 기준을 설정할 수 있다.

