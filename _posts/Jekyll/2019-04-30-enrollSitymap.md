---
layout: post
title: "[Jekyll]검색엔진 블로그 등록하기_Google 편"
date: 2019-04-30
excerpt: "Jekyll 블로그를 Google 검색엔진에 노출하기"
tag:
- jekyll
category: [ Jekyll 블로그 ]
feature: ../assets/img/title/basic.jpg
comments: false
---

## 구글 웹마스터 도구(Search Console)에 속성 추가(블로그 등록)

1. [구글 웹마스터 도구](https://search.google.com/search-console/about)에 접속합니다. Google 계정으로 로그인합니다.
2. [속성추가] 버튼을 선택합니다.
3. 자신의 jekyll 블로그 주소를 입력하여 블로그 등록합니다. (ex.http://[github 사용자명].github.io/)

## 블로그 소유권 등록

1. 소유권 확인 HTML 메타 태그를 복사하여 블로그 가장 첫 페이지 head파트에 붙여넣기합니다.
2. 확인 클릭 후 소유권 확인합니다.
3. 안될시 HTMl파일 다운받아 블로그 가장 상위 디렉토리에 업로드하고 다시 확인uv클릭합니다.

## sitemap.xml 파일 생성하기

#### sitemap?
- 웹 크롤링 봇이 이용하는 웹사이트 접근가능한 페이지 목록입니다.
- 이 파일을 사용하면 구글 또는 다른 검색엔진에 쉽게 등록할 수 있습니다.
- 검색엔진에 크롤링 할 url을 알려줌으로 색인 생성을 제어합니다.

#### 생성방법
1. 플러그인 사용
만든 GitHub Jekyll 블로그의 *_config.yml* 에 아래 내용을 추가합니다.
```
plugins : 
  - jekyll-sitemap
```
2. sitemap 생성확인
```
http://[github 사용자명].github.io/sitemap.xml
```
위 url에 접속하여 파일 생성됬는지 확인합니다.

3. sitemap 설정하기
- 우선순위 변경하고 싶을때 아래와 같이 각자의 posts파일에 태그정보를 추가합니다.
- changefreq를 빈도를 짧게 하면 빈번한 sitemap에 접속함으로 안좋은 영향을 미치니 중요한 변동이 없는 포스팅의 경우 일주일로 설정합니다.
```
---
layout: post
title: '제목'
date: 2017-10-20
lastmod : 2017-10-20 12:00:00
sitemap :
changefreq : daily
priority : 1.0
---
```

4. _config.yml 파일 설정 확인

본인 블로그의 _config.yml에 url이 본인의 설정에 맞게 바꾸었는지 확인합니다.

```
url  :  https://[github 사용자명].github.io/
```

## robots.txt 파일 생성하기

#### robots.txt?
- 검색엔진의 웹 크롤러가 방문할 때 참고하는 정책
- robots.txt 파일에 sitemap.xml 위치를 등록하면 크롤러들이 블로그를 크롤링하는데 도움을 줍니다.

#### robots.txt 생성하기
1. robots.txt 파일을 자신의 GitHub Jekyll 블로그의 가장 상위 디렉터리에 생성합니다.(theme 복사 하신분들은 대부분 만들어져 있을 거에요)
2. 아래 코드를 복사 붙여넣기합니다.
```
ser-agent: *
Allow: /
Sitemap: http://[자신의 github 사용자명].github.io/sitemap.xml
```

## 구글 웹마스터 도구(Search Console)에 만든 sitemap.xml 제출하기
1. [구글 웹마스터 도구](https://search.google.com/search-console/about)에 접속합니다.
2. 자신이 추가한 블로그(속성)을 선택합니다.
3. 왼쪽 대시보드 부분에 위치한 색인 - sitemap을 클릭합니다.
4. 새 sitemap 추가에 sitemap.xml 입력하고 제출 클릭합니다.
5. 끝!!!!!

## References
- https://gmlwjd9405.github.io/2017/10/20/include-blog-in-a-GoogleSearchEngine.html
- https://nesoy.github.io/articles/2017-01/blog-search
- https://imweb.me/faq?mode=view&category=29&category2=35&idx=15573

