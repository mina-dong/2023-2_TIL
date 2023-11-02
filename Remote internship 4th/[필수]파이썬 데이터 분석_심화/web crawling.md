데이터 수집에는 다양한 목적이 존재함.  

# 웹크롤러 : html소스에 숨겨진 tag내용의 데이터를 추출하기


page_n = 1
page_url = f"link{page_n}"
print(pag_url)

프린트문으로 출력하면 링크가 연결이 됨.  

### HTML 소스에서 필요한 내용 추출하기 : beautifulsoup4, Requests 

import requests
requests.get(page_url) #output : 200일때 정상, 404 페이지 not pound.  

마우스 오른쪽 버튼 - inspect 클릭.

- 조건을 만족하는 모든 tag를 가져오는 함수임.    
datas = source.find_all('div', class_="quest_dn")

- .text를 사용하면 안에 있는 데이터만 추출할 수 있음.
datas[0].text
반복문 ->  data.text for data in datas 


### selenium : 동적 페이지의 웹페이지를 크롤릴ㅇ할 때 사용함.  (예- opinet)  + 크롬 드라이버

동적페이지 - 페이지가 바뀌지 않는데도, 데이터가 다르게 표현됨. 


크롬 버전(setting에서 확인가능)에 맞는 크롬 드라이버를 설치.  

from selenium import webdriver  

driver =webdriver.Chrome('./chromedriver')   
driver.get('동적페이지링크')  

어떤 경우에는 접속하지 못하게 막아놓는 경우가 있음.
타 사이트에서 inspect 을 키고, 주소를 복사하면 접속할 수 있음.  

xpath : 어떤 웹페이지에서 위치를 나타내는 함수.

driver.find_element_by_xpath('xpath복사붙여넣기').click  

너무 빨리 뜨면 클릭하지 못하기 때문에 time 라이브러리를 입력.

from time import time
from selenium import webdriver  

driver =webdriver.Chrome('./chromedriver')   
driver.get('동적페이지링크')  
time.sleep(2)
driver.find_element_by_xpath('xpath복사붙여넣기').click  

E또는 xpath 대신에 
.execute_script('javascirpt')  를 사용할 수도 있음  


# pdf 데이터의 텍스트 파일전환 : pdfminer.six

pip install pdfminer.six

from pdfminer.high_leve import extract_text

text = extract_text('피디에프링크')
test = text.replace("바꿔야하는문자열" , "바꾸고싶은문자열") 

### 많이 나오는 단어 찾기  conter, nltk
from collections import Counter
import nltk (pip install nltk)

word_list = text.split()
Counter(word_list)
우선 단어를 나누고, counter를 사용한다. 

Counter().most_common(개수)
를 이용해서 개수만큼의 단어가 나오다(50을 입력하면, 50개의 상위단어빈도수를 나타냄)

nltk.Text(world_list).vocab().most_common() 도 동일하게 표현된다. 

### 정규표현식 re를 사용해서 필요하지 않은 글자 제외하기 


# 엑셀 데이터 병합하기 : 다량의 엑셀파일을 하나로 통합  

from glob import glob

file_names = glob ('link/*.xls')  
total = pd.DataFrame()

for file_name in file_name:
  temp = pd.read_excel(flie_name, header=2)
  total = pd.concat([total,temp])



