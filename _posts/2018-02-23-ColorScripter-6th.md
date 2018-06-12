---
title:  Color Scripter - 운영한지 6년 된 개인 프로젝트
date:   2018-02-23
description: '나는 혼자 만들고, 디자인하고, 운영한 프로젝트를 6년 동안 어떻게 이끌어 나갔는가'
category: dev
image: colorscripter-6th/cover.png
---

<p class="center margined">
	<img src="/attachs/colorscripter-6th/logo.png" width="445">
</p>

내가 운영하고 있는 서비스 중에 "Color Scripter" 라는 것이 있다. Syntax Highlighter (웹 상에서 코드를 볼 때 코드의 가독성을 높이기 위해 색을 바꿔주는 것)의 일종이고, 만들어진지 만 6년이 되어가고 있으며 현재는 **일 평균 400명** 정도가 찾는다. 

한국에서는 꽤 많이 쓰이는 프로그램인데, 내가 정보를 찾기 위해 구글링을 하다 보면 이 프로그램을 써서 코드를 올린 블로그를 종종 발견하곤 한다. 그렇기 때문에 쉽게 서비스를 중단할 수 없고, 또 애정을 가질 수밖에 없기도 하다.

내가 지금 만 22세이니 만 6세를 먹은 이 프로젝트는 내 인생의 1/4 이상을 함께한, 나의 개발자 인생에 상당히 비중이 있는 프로젝트다. 생일을 챙길 정도로 사용자가 많은 서비스까지는 아니라서 "6주년 이벤트!!!" 같은 걸 하기는 좀 그렇지만, **나에게만큼은 중요한 의미**가 있는 프로젝트이기에 6주년을 맞아 한 번쯤 글로 정리하는 시간을 갖고자 한다.

![screenshot](/attachs/colorscripter-6th/screenshot.png)



## 왜 만들게 되었나

Color Scripter를 처음 만들게 된 시기는 중학교 3학년 때다. 당시 한창 플래시라는 플랫폼과 Action Script 라는 언어를 이용해서 프로그램을 만드는데 흥미를 붙이고 있었다. 그리고 별거 없는 실력이지만 알고 있는 내용을 최대한 공유하려고 블로그에 강의를 코드와 함께 올리곤 했었다. 당시 나는 네이버 블로그를 이용하고 있었는데, 문제는 **네이버 블로그에 적합한 Syntax Highlighter가 없었다**는 것이다.

네이버 블로그는 강력한 보안 정책으로 `script` 태그를 일절 사용할 수 없었고, 그렇다고 **사진**으로 코드를 올리면 읽는 사람이 **복붙**을 할 수 없을뿐더러 크롤러도 코드를 읽어가지 않아 검색엔진 노출도 상대적으로 덜 되었다. 그래서 처음에는 손으로 주요 키워드마다 색깔을 입히다가 해외 서비스도 알아봤는데 디자인이 전부 맘에 들지 않았다. Action Script를 지원하는 서비스도 거의 없었던 것 같다.

<p class="center">
	<img src="/attachs/colorscripter-6th/manual-highlight.png" width="412" style="border: 1px solid #ccc"><br>
	<span class="caption">이런 허접한 강좌를 썼는데, 직접 에디터에서 '$' 드래그해서 파란색 입히고,<br>
	'a' 드래그해서 초록색 입히고, '1' 드래그해서 분홍색 입히고.. 이런 식으로 하이라이팅을 했다.</span>
</p>


그래서 불편함 끝에 직접 만들기로 결정했다. 언어도 내가 쓰는 언어만. 스타일도 내가 원하는 것만 추가해서 만들면 됐다. 그렇게 최초의 프로그램은 단순히 내가 사용하기 위해 만들게 되었다.



## 탄생 - 버전 1.0

*2012.2.29 ~ 2012.4.28*

처음에는 자신만만했다. 그냥 정규식을 이용하면 간단하게 제작할 수 있을 것이라 생각했다. 하지만 주석 속의 문자열, 문자열 속의 주석, 각종 키워드, 작은따옴표의 문자열과 큰따옴표의 문자열 등을 처리하기 위해선 정규식으로 힘들었다.

For문을 중첩하고 각종 `flag`를 이용하여 프로그램을 만들었던 기억이 난다. 이 때는 거의 Flash만 사용했으므로 Flash를 이용하여 프로그램을 만들었었고, 문법도 플래시에서 사용하는 언어인 `Action Script`만 지원했다.

<p class="center">
	<img src="/attachs/colorscripter-6th/screenshot-1.0.png" alt="v1.0 스크린샷"><br>
	<span class="caption">최초의 프로그램은 이렇게 못생겼다. 나만 쓰려고 만들었기 때문.</span>
</p>


**개인적인 용도**로 사용하기 위해서 간단히 만들었었던 프로그램이었는데, 그냥 "이런 걸 만들어 봤다" 라는 의미로 블로그에 프로그램을 올리기도 했었다. 그러다 주변 사람들(다른 플래시를 공부하는 학생들)이 신기해하길래 버전 업데이트를 계속하며 남들도 쓸 수 있도록 개선해 나가기도 했다.


블로그나 카페에 이 프로그램을 올리고, 이 프로그램을 이용하여 하이라이트 한 코드를 보며 **남들도 하나둘씩 내 프로그램을 이용**하기 시작했다. 남들이 이용하기 시작하니까 디자인에도 신경을 썼다. 설정을 누르면 사용자의 입맛 대로 스타일을 바꾸거나 옵션 등을 줄 수 있으며 이렇게 변경한 옵션은 실시간으로 미리 보기 화면에서도 반영되게끔 개선해 나갔다. 나중에는 `Action Script` 뿐만 아니라 내가 백엔드에서 주로 사용했던 언어인  `PHP`도 지원했다.

<p class="center">
	<img src="/attachs/colorscripter-6th/screenshot-1.1-settings.png" alt="v1.1 설정 화면 스크린샷"><br>
	<span class="caption">이후에는 디자인도 개선되고, 설정을 통해 사용자 입맛에 따라 변경할 수 있게끔 개선했다.</span>
</p>




## 6개월 - 버전 2.0

*2012.7.30 ~ 2012.10.27*

그러다가 재미를 붙였나 보다. 버전에 대한 판올림도 진행했다. 기존 버전에서는 `Action Script`와 `PHP`만 지웠했지만 2.0으로 판올림을 하며 `C#`, `Java`, `HaXe`, `JavaScript`, `HTML/XML`, `SQL`도 지원하기 시작했다. 언어만 추가한 건 아니다. 기존 코드는 개판이었기에 하이라이팅 엔진을 처음부터 다시 짜며 성능 개선을 꽤 했다. 

꽤 많은 언어를 지원하기는 했으나, 이게 크게 대단한 건 아니었다. 이때 나는 고등학생이었고, BNF나 LR Parser 같은 걸 전혀 몰랐다. 언어 지원이라 해봤자 **자주 사용되는 예약어들을 등록**해서 예쁘게 색깔만 입혀주면 되는 것이었다. 다만 `HTML`은 일반적인 언어와 상당히 차이가 있기 때문에 이에 맞춰서 새로운 엔진을 만들기는 했다. 꺾쇠 (`<`)가 열고 닫히는 걸 잘 보며 색깔을 입혀주고, 또 꺾쇠 안에서 attribute 표현식 (ex. `target="_blank"`)을 다른 색으로 칠해주는 방식 등 `if`문 무더기를 통해서 하이라이팅 엔진을 만들었다.

![v2.1 스크린샷](/attachs/colorscripter-6th/screenshot-2.1.png)

한가지 새로운 시도가 있었다면 **쓰레드**를 사용해서 하이라이팅을 진행하는 시도를 했다는 점이다. 원래 플래시는 쓰레드가 없다. 웹브라우저에서 임베딩되어 사용되는 플러그인 같은 존재였기에 보안상 때문인지 아님 성능상의 이유인지 관련 라이브러리를 제공하지 않았다. 대신 `Adobe AIR`라고, <u>플래시를 데스크탑 앱으로 빌드</u> 할 수 있게끔 하는 플랫폼이 있었는데, `Air `용으로 Color Scripter를 만들고, 여기서 쓰레드를 사용하여 실시간 하이라이팅을 하게 했다.

비동기 처리에 대한 문제도 있었다. 열심히 코드를 치는데 1초 뒤에 하이라이팅이 되면 그 1초 동안 새로 친 코드는 사라지고 이전의 코드가 다시 나타나게 되는 것이다. 이를 해결하고자 **비동기 처리**에 대한 나름의 공부와 머리를 좀 썼던 것 같다. 5년 전 이야기라 사실 자세한 기억이 나지는 않는다 (..)



## 3년 - 버전 3.0

*2014.12.14 ~*

2.1.1 버전을 공개하고 한동안 업데이트를 진행하지 않았다. 고등학교 내에서 동아리 활동하랴, 홈페이지 개편 프로젝트 하랴 정신이 없었기 때문에 개인 프로젝트까지 할 여유가 없었다. 그러는 와중에 고3이 되고 이때는 수능 공부 때문에 마찬가지로 신경을 쓸 수가 없었다.

그런데 종종 코딩을 하다 무언가를 찾아보려 구글링을 하면 **이 프로그램을 사용해서 하이라이팅 한 코드**를 볼 수 있었다. 어쩌다 한 번 보는 게 아니라 진짜 자주 보였다. 어떤 검색어는 상위 5개 중 2~3개 블로그가 내 프로그램을 쓰고 있기도 했다.

이때까지만 해도 네이버 블로그는 코드를 임베딩하는 기능을 제공하지 않았었고, 티스토리 사용자들도 귀찮은 Google Syntax Highlighter 대신에 그냥 "코드 복사 - Color Scripter에 붙여넣기 - 복사 - 블로그에 붙여넣기"만 하면 끝나는 내 프로그램을 많이 사용하는 것 같았다.

그래서 나중에 한번 날 잡고 개편을 해야겠다는 생각을 했다. 이번에는 나를 위해서가 아니라, 내 프로그램을 애용하는 **사용자들을 위해서**. 그렇게 수능을 보고 노는게 약간 지겨워 질 때쯤 개편 작업을 시작했다. 그리고 14년 12월 중순쯤 버전 3.0을 오픈했다. 물론 이때는 **망해가는 플래시**로 개발하지 않았다. `JavaScript`를 이용하여 **홈페이지** 형태로 만들었다.


<p class="center">
	<img src="/attachs/colorscripter-6th/screenshot-3.0.png" alt="v3 스크린샷"><br>
	<span class="caption">현재 버전과 거의 유사하다. UI에도 상당한 노고를 들여서 만들었다.</span>
</p>


개발 언어도 갈아탔고, 플랫폼도 갈아탔지만 **내부 엔진**도 완전히 갈아엎었다. 더 많은 언어를 언어를 제공함과 동시에 확장성을 보장하고자 꽤 많은 고민을 했던 것 같다. 대표적인 게 언어마다 `type`이라는 속성을 주었는데, **비슷한 언어**들은 하나의 type으로 묶어 모든 언어마다 따로 알고리즘을 사용하는 것이 아니라, **공유**하게끔 개발했던 것이다.

```json
"html" : {
	"types" : ["markup", "html"],
	"keywords" : []
},
"markdown" : {
	"types" : ["markup", "markdown"],
	"keywords" : []
},
"php" : {
	"types" : ["markup", "html", "php"],
	"keywords" : []
},
"php-inner-code" : {
	"types" : ["common", "sigil"],
	"comment_types" : ["//", "/*", "#"],
	"keywords" : [
		["array","object","StdClass","count",...],
		["as","new","self","include","require",...]
	]
},
"xml" : {
	"types" : ["markup"],
	"keywords" : []
},

```

위 설정 파일을 보면 `xml`은  markup 만의 속성을 따르지만 `html`은 markup 과 html 의 속성을, `markdown`은 markup과 markdown의 속성을, `php`는 markup과 html, php의 속성을 모두 따르게 했다. `type:php`는 `<?php`와 `?>` 키워드 사이에 위치한 코드의 경우 `php-inner-code` 로 하이라이트 하게끔 하는 속성이다.

<br>

```python
if (lang == 'xml' || lang == 'html' || lang == 'markdown' || lang == 'php'):
    # Highlight Markup Lanauge
```

이런 방법을 쓰면 위와 같은 더러운 코드가 들어가지 않아도 된다. 속성을 바탕으로 **언어의 특징들을 그룹화하고 언어를 <u>특징의 합</u> 형태로 표현**하여 확장성과 함께 나름 깔끔하게 언어들을 관리할 수 있었다.

하지만 이도 완벽한 방법은 아니었고, 결과적으로 `type`마다 손수 알고리즘을 짜야 하며, <u>새로운 유형</u>의 언어를 추가하려면 또다시 엔진을 수정해야 한다. 그래도 개발자 한 명이 계속 업데이트 하기에는 나름 괜찮은 구조로 개발했던 것 같다. 3.0 버전으로 업데이트하며 `c++`,  `python`, `ruby`, `perl`, `visual basic`, `objective-c`, `swift` 를 지원했으며, 3.1 버전에서는 `ASP`와 `JSP`가 추가되었다.

<br>

**사용자 편의성**도 많이 고려했다. 웹으로 만들어진 다른 서비스들을 많이 참고하면서 디자인을 했고, 스타일패키지(테마)의 경우 선택 전에 미리 볼 수 있게끔 간이 화면도 제공한다. 

<p class="center">
	<img src="/attachs/colorscripter-6th/toolbar.png" alt="툴바" width="664">
</p>


이렇게 서비스를 개편하고 공개했을 때의 반응은 **성공적**이었다. URL를 새로운 주소로 리디렉션하고 개편 사실을 알려주는 팝업을 띄워서 새로운 버전으로 유도시켰고, 상당 수의 사용자는 자연스럽게 새로운 버전으로 넘어오게 되었다. 이후 구글과 네이버에 `Color Scripter` 라는 키워드로 검색을 해보니 "업데이트 되어 기쁘다", "더 예뻐졌다"라는 반응도 종종 보였다.

무엇보다 홈페이지 내에 "기부" 탭이 있는데, 여기에 있는 `Paypal Donation`을 통해서 몇 명의 사람들이 진짜 **후원**을 해주기도 했다. 물론 커피값~점심값 정도의 적은 금액이기는 했지만 상당히 뿌듯한 경험이었다.



## 4년 - 확장 스토어

*2016.1.23 ~*

확장 스토어는 사실 **귀찮음** 때문에 만들었다. 홈페이지에 문의는 여기로 해달라고 내 메일을 적어뒀었는데, 그 메일로 자꾸 "이 언어 추가해달라", "저 언어 추가해달라"라고 메일이 온 거다. 자주 사용되는 언어면 기꺼이 해줄텐데, 들어보지도 못한 **마이너** 한 언어의 요청이 많았다. 귀찮음 이외에도 요청 온 언어들을 전부 추가한다면, 오히려 주요 언어만 사용하는 <u>대다수의 사용자</u>가 마이너한 언어 때문에 프로그램 사용 시간이 길어져 <u>편의성을 해쳐질 수 있다</u>는 문제도 있었다.

이러한 문제점 때문에 차라리 **확장 스토어**를 만들자고 결정했다. 사용자들이 스스로 언어를 만들어서 사용하고, 또 공유해서 내가 가만히 있어도 알아서 돌아가는 생태계를 구축해보기로 했다.

<p class="center">
	<img src="/attachs/colorscripter-6th/extend-store.png"><br>
	<span class="caption">현재 Color Scripter 확장스토어의 모습</span>
</p>


원래 하이라이팅 엔진 자체가 `json` 형태로 언어와 테마를 지정하는 형식이었기에 일반 사용자도 언어나 테마를 만들기는 쉬운 구조였다. 내가 할 일은 이 json을 손으로 치는 방법 대신 조금 예쁘고 편하게 할 수 있도록 **제작 페이지를 개발**하는 것과, 이렇게 만들어진 설정들을 공개해서 크롬 확장스토어 처럼 일종의 "**설치**"를 할 수 있도록 하는 일이었다. 

그 결과 300개 이상의 플러그인이 등록되었고, 무엇보다 언어를 추가해달라는 메일이! 더 이상 오지 않는다! 낮은 퀄리티의 플러그인도 많지만 꽤 **괜찮은 퀄리티**의 플러그인들도 있다. `ES6`나 `Go`, `Delphi`, `Docker` 같은 언어는 모두 사용자들이 직접 만든 언어이다. 내가 개발할 당시에는 그렇게 핫하지 않았지만 요즘 핫한 언어들이 이렇게 **사용자를 통해서 자연스럽게 관리되는 환경**이 어느 정도는 조성되었다고 말할 수 있는 것이다.


<p class="center">
	<img src="/attachs/colorscripter-6th/extend-store-2.png"><br>
	<span class="caption">확장 스토어의 플러그인 제작 페이지 또한 최대한 이쁘게 만들어<br>사용자들이 높은 퀄리티의 플러그인을 자연스럽게 만들어낼 수 있게끔 의도했다.</span>
</p>



## 4년 반 - 머신러닝과 언어 자동선택 기능

*2016.7.12 ~*

사실 그전까지 이 서비스를 운영하며 할 수 있는 것이라고는 더 편리한 기능, 더 예쁜 UI/UX를 통해 사용자를 더 만족시키는 것 밖에는 없었다. 그러다 '알파고'가 떴고, 나도 **인공지능**을 통해 무언가를 해보고 싶은 생각이 들었는데, 사용자가 코드를 입력하면 **자동으로 코드를 분석하여 언어를 추천해주는 기능**을 만들면 어떨까 하는 아이디어가 떠올랐다.

프로그래밍 언어를 유추하는 가장 쉬운 방법은 "키워드"다. 언어별로 사용하는 고유의 함수들이나 예약어들이 있는데, 이를 많이 사용하면 사용 할수록 그 언어일 확률이 높아지는 거다. 예를 들면 `public void static main` 이라는 키워드를 사용하면 이 언어는 `Java`일 확률이 굉장히 높을 것이다. 마찬가지로 `#include, prinft, scanf`를 많이 사용한다면 `C언어`일 확률이 높을 것이다.

이와 같은 상황을 처리하기 좋은 정리가 있었고, 실제 머신러닝에서도 "스팸 분류" 등에 사용되고 있었다. [나이브 베이즈 정리](https://ko.wikipedia.org/wiki/%EB%82%98%EC%9D%B4%EB%B8%8C_%EB%B2%A0%EC%9D%B4%EC%A6%88_%EB%B6%84%EB%A5%98)라고 하며, 확률 및 통계에 기반을 두고 있다.


<p class="center">
	<img src="/attachs/colorscripter-6th/keyword_prob.png"><br>
	<span class="caption">실제로 학습을 돌려보면 자주 사용되는 키워드가 높은 확률을 가지고 있다</span>
</p>


이를 구현하기 위해 가장 중요한 것은 "코드-언어"에 대한 **정답 셋**이다. 실제 사용되는 코드와, 그 코드가 어떤 언어인지에 대한 정보가 필요한 것인데, 이를 얻기 위해선 Github 등을 크롤링 하면 된다. 하지만 나는 굳이 차단을 우회하고 힘들여가며 크롤링을 할 필요가 없었다. Color Scripter는 정답 셋을 만들기에 상당히 유용한 서비스였다.

바로 약관에 코드를 수집한다는 점을 추가하고 안내 후 **코드를 수집**하기 시작했다. 코드가 일정 수준 이상 모인 후 `Python`을 통해서 학습기 및 분류기를 만들게 되었다. 처음에는 2만 개의 코드로 학습을 돌렸고, 최근에는 10만 개 이상의 코드로 학습을 돌려 둔 상태이다.

꽤 많은 데이터로 학습을 돌렸음에도 높은 정확도가 나오지는 않았다. 특히 `HTML`과 `JavaScript`는 서로 섞어서 사용하는 경우가 많았는데, 이 둘의 정확도는 50% 정도로 굉장히 낮은 수치가 나왔다. 일부 데이터의 경우 **사용자**가 `JavaScript` 코드를 붙여놓고 `HTML`으로 설정을 해두어 **학습 셋 자체가 잘못된 경우**도 있었다.

이후에는 키워드뿐만 아니라 언어별 문법을 기준으로 한 **주요 패턴**이 얼마나 매칭 되느냐에 대한 기준도 추가하며 코드를 **몇 차례 개선**을 거친 후, 현재는 약 80%의 정확도가 나오는 상태이다. 이에 대한 보다 자세한 내용은 별도의 [블로그 글](https://prev.kr/posts/머신러닝을-맛보다/)로도 정리해 뒀었다. (저 글도 2년이 다되가서 지금 쓰는 코드와는 꽤 다르긴 하다.)


<p class="center">
	<img src="/attachs/colorscripter-6th/csld-accuracy.png" width="461"><br>
	<span class="caption">현재 정확도 테스트 결과</span>
</p>


현재 해당 코드는 오픈소스로 공개한 상태이고, [github.com/Prev/shaman](https://github.com/Prev/shaman) 에서 볼 수 있다. 실제 서비스 내 코드는 위 라이브러리에 `redis` 캐시를 써서 속도를 증가시킴과 동시에 서버 부하를 낮추게끔 개선한 버전으로 사용하고 있다.

[colorscripter.com](http://colorscripter.com)에 들어가 바로 에디터에 코드를 붙여 넣으면 상단 언어 툴바에 `자동(html)`과 같은 표시를 볼 수 있는데, 이는 언어 탐지기를 통해서 **어떤 언어인지 분석한 후 그 언어로 하이라이팅**을 하고 있음을 의미한다. 현재는 안정적으로 이 **기능이 적용**되어 약 **4~50%**의 사용자가 언어를 따로 바꾸지 않고 자동으로 설정된 언어로 이용하고 있다.



<p class="center">
	<img src="/attachs/colorscripter-6th/language-detection.png" width="369"><br>
	<span class="caption">이렇게 자동으로 언어를 찾아낸다. 직접 가서 써봐도 좋다!</span>
</p>



## 6년 - 현재와 미래

기존 코드가 정말 더럽기에 (특히 UI 쪽 코드는 매우 더럽다) 4.0 판올림을 할까도 생각을 했었다. 하지만 이제는 네이버 에디터에서 코드를 지원하고, [jsfiddle](https://jsfiddle.net/)등 코드와 더불어 결과까지 확인할 수 있는 서비스들도 많이 등장하고, 또 이용되고 있어 Color Scripter의 사용자는 **계속 떨어지고** 있다. (많을 땐 일 5~600명도 방문을 했었다. 현재는 400명 수준.)

때문에 최근에는 굳이 시간을 내서 업데이트를 하기보다는, 머신러닝 등의 공부를 할 때 이 서비스에 활용해보자는 목표를 가지고 이용하는 용도로 개발과 운영을 진행했었다.


<p class="center">
	<img src="/attachs/colorscripter-6th/screenshot-admin.png"><br>
	<span class="caption">통계를 보다 보면 주말이나 연휴때는 사용자가 적어진다는 재미있는 점을 확인할 수도 있다</span>
</p>




물론 Color Scripter는 여전히 내 포트폴리오에 빠지지 않고 들어가는 프로젝트이고, 그만큼 많은 애정이 있기에 사용자가 계속 줄어들어도 서비스는 계속 운영을 하지 않을까 싶다. 지금 상황에 있어서는 운영을 꾸준히 하면서 확장스토어나 언어 탐지기처럼 **새로운 시도를 해볼 만한 재밌는 아이디어**가 있다면 그 기능들을 추가해가며 조금씩 업데이트되어 나가는 형식이 가장 낫다고 생각된다.

Color Scripter를 6년간 만들어가며 개발 뿐만 아니라 운영 관점, 사용자 편의성 관점에서도 다양한 발전을 해 나갈 수 있었는데, 이에 대해 감사하며 앞으로도 좋은 서비스를 만들 기회가 있다면 이를 경험삼아 해 내가면 좋을 것 같다.

*여튼 Happy Anniversary, Color Scripter!*
