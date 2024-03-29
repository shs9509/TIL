# 검색엔진 최적화, SEO

> Search Engine Optimization

## WHY

구글에서 당신의 사이트를 찾아서 색인을 생성하고 순위를 지정합니다. 

그리고 가이드에 잘맞게 되있다면? 더 높은 순위를 가져서 사람들이 자주 방문하게 되는거죠!

광고검색클릭은 2% 근데 자연검색콘텐츠는 한 40% -> "광고대비 전환률 8~10배, 비용도 9~10배 차이남''



### 구글 검색 접근

- 크롤링 : 크롤러가 좋아할만한 글작성 ->수집이 잘됨

- 인덱싱 : 크롤러가 모은 데이터를 저장함

- 랭킹 : 콘텐츠 랭킹을 올리자



### SEO 결정 요소들

- 사이트 보안
- 모바일 친화적인가
- 페이지 스피드



### SEO 관련 키워드를 얻기 위한 사이트

- 구글 키워드 플래너
- 네이버 광고센터
- 실제키워드가 갖고있는 경쟁력 - keyword tool.io 
  - 관련있는 키워드 의도키워드를 사용해야됨
- 유입하는 고객들의 키워드 -구글 서치콘솔
- ahrefs



## HOW

### 1. 문법에 맞는 HTML 작성하기

- 적절한 HTML 소스로 홈페이지를 구성하는 것은 결과적으로 검색엔진에게도 이해하기 쉬운 웹 문서가 되고, 유사한 내용의 웹 문서가 있을 경우 상대적으로 이러한 문서의 순위가 높아집니다.
  - `<title>`태그에는 사이트 제목을 기재
  - ` <div>` 태그를 사용해 줄을 바꾸기
  - `<strong>`과 `<em>` 태그를 활용해 강조하고 싶은 키워드에 붙이는 등 



### 2. 구체적인 페이지 제목 만들기

HTML 문서의 헤더에 들어가는 페이지 제목(title)은 구체적이고 간결하게 구성해, 검색 결과 화면에서 텍스트가 잘리지 않도록 합니다.

- 유인 키워드 반복 삼가 (예) café, ca fe, 카페, 카 페
- 반복적이고 틀에 박힌 제목 삼가
- 제목의 시작이나 끝에 사이트 이름을 포함하고 나머지 제목은 하이픈( – ), 콜론( : ), 막대(ㅣ)



### 3. 메타 태그 활용하기

Google 등 메타 태그 `<meta>` 정보를 검색 알고리즘 평가 대상에서 제외하는 검색엔진이 증가한다지만, 검색엔진의 검색 결과에도 표시되기 때문에 포함하는 것이 좋습니다.

```html
<meta name=”keywords” content = “키워드 1, 키워드 2″>
<meta name = “description” content = “페이지 내용을 정리한 소개 글(검색 결과 프리뷰로 나타나는 영역)”>
```

**[구글에서 추천하는 디스크립션(description) 작성법]**

- 웹사이트 내 모든 페이지에 동일한 디스크립션(description)을 적용할 경우 효과적이지 않음
- 각 페이지의 내용을 전체적으로 요약해 서술한 내용을 넣는 것이 좋음
- 해당 페이지의 제목(title)과 중복되는 정보는 제외하는 것이 좋음
- 페이지가 많은 홈페이지의 경우, 최대한 잘 읽히고 스팸으로 구분되지 않게 구성해야 함
- 모든 페이지를 작성할 수 없는 상황이라면, 홈페이지 내 각 페이지에 우선순위를 두어 주요 페이지들만 작성하는 것을 추천



### 4. 이미지에 alt 속성 기재

alt 속성이란, alternative의 의미로 이미지가 로딩되지 못했을 때 대신 표시되는 텍스트입니다.

`<img>` 태그에 alt 속성을 넣어 적절한 대체 텍스트를 기재해야 합니다. 검색엔진이 이미지를 발견하면 alt 속성 안의 텍스트를 통해 인덱싱 작업을 하기 때문에 SEO에 좋습니다.

alt 속성을 붙이면 시각장애인용 스크린리더가 사용될 때 이미지 대신 alt 속성 값을 읽어 대략 어떤 이미지인지 파악할 수 있도록 도움을 줍니다.



### 5. 이미지 맵에 중요한 링크 사용 피하기

이미지 맵은 `<map>` 태그와 `<area>` 태그를 이용해 한 장의 사진에 여러 개의 링크를 설치하는 것입니다. 

이미지 맵은 검색엔진이 링크를 따라 이동할 때 방해가 될 수 있으므로, 중요한 링크 설치는 피합니다.

(예) 여러 카테고리나 메뉴를 하나의 큰 이미지에 들어가게 만들어 놓고, 각 부분을 클릭하면 해당 페이지로 이동하도록 만든 사이트



### 6. 플래시 전용 페이지 피하기

현재, 대부분의 검색엔진은 Flash 애니메이션의 텍스트를 수집할 수 없으며, 그 링크 또한 사용할 수 없습니다.

예를 들어, 홈페이지에 Flash만 놓고 HTML 소스에 `<a>` 태그를 코딩해 작성하지 않는 경우, 검색 로봇은 앞 뒤 페이지로 이동할 수 없어 검색엔진 데이터베이스에 수집되지 않습니다.
결과적으로 해당 홈페이지는 검색 결과에 잘 나타나지 않게 됩니다.



### 7. anchor 태그를 활용한 적절한 키워드 배치

키워드가 본문에 기술되어 있지 않은 홈페이지는 검색 결과에 랭크되기 어렵습니다.
구글의 경우, ‘앵커 텍스트’ 링크로 해당 페이지에 키워드가 포함되어 있는지 체크하기도 합니다.

앵커 텍스트: 홈페이지에 삽입되는 링크 위에 있는 설명 문구(text)를 의미합니다.
앵커 태그: 서로 다른 페이지 사이를 이동하거나 페이지 내부에서 특정한 위치로 이동할 때 사용합니다.

-> a태그 쓰자



### 8. 여러 개의 페이지로 나누어진 콘텐츠 검색 최적화 – 시리즈/연재

시리즈 및 연재 등과 같이 한 주제로 글이 길어질 경우, 동일 제목을 가진 콘텐츠를 여러 페이지로 나누어 만들게 됩니다. 

- 캐노니컬 태그 (Canonical tag)

  - 캐노니컬 태그란 사이트 내 URL 주소는 다르지만 동일한 내용의 중복된 페이지가 있을 때 페이지에 코드를 삽입하여 검색엔진에 대표가 되는 URL 주소를 알려주는 역할을 하는 태그

  - 페이지가 다른 페이지의 중복 페이지임을 나타내려면 HTML의 `head` 섹션에 `<link>` 태그를 사용하면 됩니다.

    ```html
    <link rel="canonical" href="https://example.com/dresses/green-dresses" />
    ```

1) 전체보기 페이지를 만들어 제공
   : 각각의 나누어진 페이지에 rel=”canonical” 링크를 삽입해 전체보기 페이지를 표시합니다.

2. rel=”next”및rel=”prev” 링크로 연재글 사이의 순서를 알림
   - Google에서는 해당 페이지를 논리적 순서로 처리하여 페이지의 링크 속성을 통합하고 검색자에게 주로 첫 번째 페이지를 표시해 줍니다.



### 9. 모든 페이지가 유입 페이지가 되도록 사이트 구성

사용자가 꼭 홈페이지의 메인 페이지만 방문하는 것은 아닙니다. 가령, Google에서 키워드나 내용으로 검색하면, 검색 결과에는 원하는 정보가 있는 콘텐츠 페이지가 나타나고, 클릭하면 해당 페이지로 유입됩니다.

홈페이지 내 어떤 페이지로 방문이 유입될지 모르기 때문에 모든 페이지에는 메인 페이지로 이동할 수 있는 링크를 설치해 전체 사이트의 ‘동선’을 개선하는 것이 무엇보다 중요합니다. 이것이 곧 사용자 편의성과도 연결되는 것입니다.



### 10. HTTPS 사용 권장

동일사이트라면 http로 서비스 하는 것보다, https로 서비스 할 경우 구글 검색엔진에서 전체 점수의 약 1% 정도에 해당하는 랭킹 가산점을 부여합니다.







----

#### 참조

- [초급 검색엔진 최적화][https://developers.google.com/search/docs/beginner/seo-starter-guide?hl=ko]

- [가이드 라인][https://developers.google.com/search/docs/advanced/guidelines/webmaster-guidelines?hl=ko]

- [구글 검색엔진 최적화 가이드][http://static.googleusercontent.com/media/www.google.com/ko//intl/ko/webmasters/docs/search-engine-optimization-starter-guide-ko.pdf]
- [가비아 효율적인 검색엔진 최적화][https://library.gabia.com/contents/domain/4359/]

- [SEO가이드 총정리][https://www.hedleyonline.com/ko/blog/seo-guide-2021/]

[https://www.hedleyonline.com/ko/blog/seo-guide-2021/]: 