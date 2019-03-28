---
layout: post
title: 인터파크 공연 리뷰(관람후기) 크롤링 시도: 파이썬(beautiful soup) + 셀레니움
excerpt: "최근 연구실 프로젝트를 진행하면서 인터파크에 있는 공연 리뷰를 크롤링해야하는 일이 있었다. 검색을 잘못한건지, 내가 필요로 했던 솔루션을 찾지 못해서 헤매다가 직접 코딩한 부분을 정리해보고자 한다. 여러 공연 리뷰 데이터를 긁는데는 성공했으나 케바케로 완벽히(?) 안되는 경향이 있다. 크롤링이 완벽하게 되지는 않지만, 일단 첫번째 버전을 공유하는 차원에서 포스트를 작성한다"
categories: [code, crawling]
comments: true
---

최근 연구실 프로젝트를 진행하면서 인터파크에 있는 공연 리뷰를 크롤링해야하는 일이 있었다. 검색을 잘못한건지, 내가 필요로 했던 솔루션을 찾지 못해서 헤매다가 직접 코딩한 부분을 정리해보고자 한다. 여러 공연 리뷰 데이터를 긁는데는 성공했으나 케바케로 완벽히(?) 안되는 경향이 있다. 크롤링이 완벽하게 되지는 않지만, 일단 첫번째 버전을 공유하는 차원에서 포스트를 작성한다.



## 0. 개발 환경 및 필요 라이브러리

필자는 맥, 그리고 파이썬3 에서 코딩하는지라 맥 기준으로 작성

1. Python 3
  1. beautiful soup: `pip3 install bs4`
  2. pandas: `pip3 install pandas`
2. Selenium: `pip3 install -U selenium`
3. Pandas: `pip3 install pandas`
4. [Chrome Driver](http://chromedriver.chromium.org): 링크를 방문해서 알맞은 드라이버 다운로드. 같은 폴더에 넣거나 `/usr/local/bin` 에 넣거나 편하신대로 하면 될듯 합니다.



## 1. Selenium을 이용한 웹사이트 브라우징

필자는 크롬을 사용하여 크롤링을 해보고자 한다. (위에 크롬드라이버 설치하세요)  
그리고 `selenium`이라는 툴을 사용해서 웹사이트를 열어 제어하고, `beautiful soup` 으로 크롤링을 한다.

```python
from bs4 import BeautifulSoup

from selenium import webdriver
from selenium.webdriver.common.desired_capabilities import DesiredCapabilities

import time

### Crawling Setup
browser = webdriver.Chrome('/usr/local/bin/chromedriver')
browser.implicitly_wait(3)
```

`browser.implicitly_wait(3)` 이 부분은 웹사이트를 열고 로딩을 위해 3초만 기다려달라 하는 부분이다

이제 '지킬앤하이드' 모바일 웹페이지에 접속한다

```python
url = 'http://mticket.interpark.com/Goods/GoodsInfo/info?GoodsCode=18011275&app_tapbar_state=fix#GoodsTabArea'
browser.get(url)
```

여기까지 코드를 실행하면, 새로운 크롬 창에 '지킬앤하이드' 모바일 사이트가 열릴 것이다.



## 2. 인터파크 관람평 보기

결론부터 말하자면 인터파크 데스크탑 웹사이트보다는 모바일 웹사이트을 이용하는 방식을 택했다. 이번 글에서 예시로 크롤링을 할 ['지킬앤하이드'](http://ticket.interpark.com/Ticket/Goods/GoodsInfo.asp?GoodsCode=18011275) 페이지로 들어간다. 일단 데스트탑 페이지의 리뷰 부분을 보면, pagination이 들어간 부분을 볼 수 있다:

![데스크탑 웹페이지 댓글](https://d.pr/i/RPxQw1+)

이러면 크롤링이 조금 짜증나는… 경우가 될 수 있을것 같다.  
(특히 나는 코딩 고수가 아니니까… 쉬운길로 가는걸로 한다)

하지만 모바일 페이지는 다르다. [모바일 페이지](http://mticket.interpark.com/Goods/GoodsInfo/info?GoodsCode=18011275&app_tapbar_state=fix#GoodsTabArea')는 infinite scroll 방식으로 리뷰가 늘어난다. (스크롤을 페이지 끝까지 진행하면 다음 리뷰들이 로딩되어 나온다). 

우리는 여기서 `selenium` 을 이용하여 '관람후기' 부분을 클릭해야한다. 그래야 웹페이지에 공연 리뷰들이 열리기 때문이다.  
`selenium` 을 이용하여 클릭을 시뮬레이션을 해야하기에, 개발자툴을 열고  `Inspect Element` 를 한다.

![리뷰를 보기위한 버튼 클릭](https://d.pr/i/0bjAY6+)

'관람후기'의 `id = "tabPostInfo"` , `onclick = tabControl03()` 부분을 주목하자.  
여기서 우리는 `selenium`을 통해 `tabPostInfo`를 찾고, 클릭을 시뮬레이션 한다:

```
element = browser.find_element_by_id("tabPostInfo")
browser.execute_script("tabControl03()", element) 
```



## 3. 스크롤 시뮬레이션 하기

우리는 페이지를 열고, 클릭해야할 버튼을 찾았고, 클릭까지해서 리뷰들이 나오게 만들었다. 이제 모든 리뷰들이 나올수 있도록 스크롤을 해야한다: 

```python
# Get scroll height
last_height = browser.execute_script("return document.body.scrollHeight")

while True:
    # Scroll down to bottom
    browser.execute_script("window.scrollTo(0, document.body.scrollHeight);")

    # Wait to load page
    time.sleep(0.5)

    # Calculate new scroll height and compare with last scroll height
    new_height = browser.execute_script("return document.body.scrollHeight")
    if new_height == last_height:
        break
    last_height = new_height
```

중간에 확실한 페이지 로딩을 위한 시간 0.5초가 있는걸 주목.  
필자의 경험으로 너무 작은 로딩 시간을 주면 모든 리뷰가 나오기 전에 페이지 스크롤이 끝나는 경우가 잦았다. 시간은 알아서 적당히 조절하자.



## 4. Beautiful Soup을 이용하여 리뷰 크롤링하기

이제 스크롤까지 시뮬레이션을 하고, 모든 리뷰의 로딩을 마쳤다. 다음 스텝은 리뷰들의 제목과 텍스트를 뽑는 일이다.  
리뷰를 하나 열어보면, 리뷰 제목, 그리고 리뷰 텍스트의 구조를 갖고 있는것을 확인 할 수 있다. 우리는 제목과 리뷰 텍스트의 `class` 이름을 알아야한다.

![리뷰를 펼쳐보자](https://d.pr/i/N5mkoO+)

제목의 `class` 이름은 `userBoardTitle`, 실제 텍스트의 `class` 이름은 `boardContentTxt` 인걸 볼 수 있다. 이제 우리는 `beautiful soup` 을 이용해서 이 부분을 크롤링한다:

```python
html = browser.page_source
soup = BeautifulSoup(html, 'html.parser')

review_title = soup.find_all("div", {"class": "userBoardTitle"})
review = soup.find_all("div", {"class": "boardContentTxt"})

total = len(review_title)
print(total)
```

아래 `print` 는 웹사이트에 표시된 후기 갯수와 우리가 뽑은게 일치하는지 확인하는 용도로 넣었다.

리뷰는 다 긁은것이 확인 된다면 (혹시 일치하지 않다면 위에 `time.sleep(0.5)` 부분의 시간을 조정해보도록 하자.) pandas 를 이용해 데이터를 간단히 정리하여 csv 파일로 출력한다.



## 5. pandas로 데이터 정리하기 및 csv 파일 만들기

파일 상단에 꼭 `import pandas as pd` 를 잊지말고 넣어두자

```python
import pandas as pd

# pandas dataframe setup
titles = []
reviews = []

for i in range(len(review_title)):
    titles.append(review_title[i].get_text())
    reviews.append(review[i].get_text())

df = pd.DataFrame({'Title': titles, 'Text': reviews})

# clean DataFrame
df = df.replace('\n', ' ', regex=True)

# export to excel
df.to_csv('jekyll.csv')
```

긁은 데이터를 `pandas dataframe` 으로 넣는 작업이다.  

1. 크롤링한 제목은 `titles` 에, 실제 리뷰 텍스트는 `reviews `에 넣는 작업을 거치고, 
2. `Title` 이라는 column에 제목을, `Text `라는 column에 리뷰를 넣는다.
3. 데이터 클렌징 작업. 줄바꿈 되어있는 부분을 한 줄로 정리해준다.
4. `jekyll.csv` 이라는 이름의 csv 파일로 저장한다.



## 6. 마무리

필자는 일단 이 방식으로 '지킬앤하이드' 공연의 리뷰를 2019년 3월 26일 기준 7,653개의 리뷰를 성공적으로 크롤링하였다. 다음 작업은 한번 TF-IDF 를 돌려보는 것이다. 이 뮤지컬을 본 사람들이 공연의 어떤 부분에 가장 큰 만족도를 느끼는지, 어떤 요소를 집중적으로 평가하는지 볼 수 있으면 한다.



---

### References

1. <https://beomi.github.io/2017/02/27/HowToMakeWebCrawler-With-Selenium/>
2. <https://stackoverflow.com/questions/20986631/how-can-i-scroll-a-web-page-using-selenium-webdriver-in-python>
3. <https://medium.com/@whj2013123218/%ED%8C%8C%EC%9D%B4%EC%8D%AC%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-twitter-%ED%81%AC%EB%A1%A4%EB%A7%81-576f7b098daf>





