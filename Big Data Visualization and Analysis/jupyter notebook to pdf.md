# jupyter notebook to pdf

주피터 노트북을 이용해 pdf로 변환하는 방법.  

아래와 같이 있다.  
1. 구글에서 검색해서 나온 .ipynb to pdf 변환 사이트를 이용한다.  
2. 복잡한 설치방법을 거쳐서 직접 주피터 노트북을 이용헤 변환한다.   

1번 같은 경우 편리하긴 하지만, 한글로 마크다운을 작성했을 때 글자 자체가 출력이 안되는(한글깨짐) 현상이 발생함.  
영어만 이루어져있다면 상관없을텐데, 한글이 들어가야해서 2시간 정도 걸렸다.. 
따라서 2번의 방법을 사용했으며, 상세한 내용은 구글링해서 참고할 것.  

2. 복잡한 설치과정을 통해 주피터노트북에서 pdf 변환하기 (LaTex)  
   2.1 Miktex 설치(설치시에 계속 패키지 설치하라는 창이 여러개 뜸.)    
   2.2 주피터 노트북에서 "Latex"로 export하기  
   2.3 oblivoir.tex 저장(파이썬이 저장되어있는 경로)  
   2.4 export한 .tex 열기 (압축파일 풀고 실행할 것.)  
   2.5 Teworks를 통해 어떤 콘솔창 같은게 나옴. 맨 위로 올려서 \usepackage{kotex} 입력  

   ```
   \documentclass[11pt]{article}
    
    \usepackage{breakable}...
   ...
   ```

   전

    ```
    \documentclass[11pt]{article}
     \usepackage{kotex}
     \usepackage{breakable}...
    ...
    ```

   후

   2.5 초록색버튼(재생모양)클릭

   한글 글자가 깨지지 않은 pdf 변환 완료!


   **참고로 \usepackage{kotex} 은 변환할때마다 입력해야함**
   