---
layout: post
title: "HTML 속의 자바스크립트"
description: "프론트엔드 개발자를 위한 자바스크립트 프로그래밍 2장 HTML 속의 자바스크립트 요약"
category: blog
tags: [javascript, jquery, beginner, guide, study, studyjs, facebook, group]
---

이 포스팅은 "프론트엔드 개발자를 위한 자바스크립트(2013 인사이트, 한선용 옮김)"에서 발췌 요약한 것이며, 인사이트와 저작권에 대한 부분을 의논하여 사전 허락을 받은 것입니다. 자세한 내용은 페이스북 [자바스크립트 제대로 하기 스터디 그룹](https://www.facebook.com/groups/learnjsproperly/)의 [해당 포스트](https://www.facebook.com/groups/learnjsproperly/permalink/364077967076150/?stream_ref=2)를 참조하시기 바랍니다.

# 2장. HTML 속의 자바스크립트

### 2.1 `<script>` 요소

자바스크립트를 HTML 페이지에 삽입하는 일차적인 방법이며, async, charset, defer, language, src, type의 여섯가지 속성이 있다. 현재 language는 페기되었고, charset 값은 무시된다. type 속성은 아직 습관적으로, 또는 브라우저 호환성을 위해 “text/javascript” 라 표기하곤 하나, 기본값이라서 생략 가능하다.

`<script>` 요소 안의 인라인 자바 스크립트 코드는 위에서부터 차례로 해석되며 코드 전체를 해석하기 전에는 페이지의 나머지 콘텐츠를 불러오지도 않고 표시하지도 않는다.

인라인 자바스크립트 코드에서 문자열 “</script>”는“/” 문자를 `\`로 이스케이프해야 한다.

자바스크립트를 외부 파일에서 불러오려면 파일의 URL을 속성값으로 src 속성을 사용한다. 외부 파일의 코드를 내려받고 해석하는 동안 페이지 처리가 멈춘다.

    <script type="text/javascript" src="example.js"></script>

**중요**: `<script>`와 `</script>` 태그 사이에 스크립트 코드가 있고 `src` 속성도 사용했다면 브라우저는 스크립트 파일을 내려받아 실행하며 인라인 코드는 무시합니다.

신뢰할 수 있는 외부 도메인의 코드를 마치 페이지의 원래 일부였던 것처럼 불러와서 해석할 수 있다.

    <script type="text/javascript" src="http://www.somewhere.com/afile.js"> </script>

#### 2.1.1 태그 위치

전통적으로 `<script>` 요소는 외부 파일에 참조를 한곳에 관리하기 위해 페이지의 `<head>` 요소 안에 쓰는 것이 일반적이었다. 그러나, 최신 웹 앱에선 페이지 렌더링 시간의 지연을 막기 위해 `<body>` 요소 안에, 페이지 콘텐츠 마지막에 - `</body>` 태그 바로 앞에 - 쓴다.

#### 2.1.2 스크립트 처리 지연(defer 속성)

defer 속성을 설정하면 브라우저는 즉시 코드를 내려받지만 실행은 페이지 전체를 파싱한 후에 한다. 그러나, 지연시킨 스크립트가 항상 순서대로 실행되지는 않으므로 `<script>` 요소를 하나만 쓰는 것이 최선이다. 그러나, 여러 브라우저 지원 문제 때문에 스크립트는 페이지 맨 마지막에 놓는 것이 최상이다.

#### 2.1.3 비동기 스크립트(async 속성)

스크립트를 모두 내려받을 때까지 기다릴 필요없이 페이지 렌더링을 시작해도 좋으며, 앞선 스크립트 파일을 기다리지 않고 위의 스크립트 파일을 받아도 좋다고 명시하는 것이다. 스크립트가 순서대로 실행된다는 보장이 없어 여러 스크립트 파일 사이에 의존성이 있으면 안되며, DOM을 조작하는 스크립트는 비동기적으로 불러오지 않는 것이 좋다.

#### 2.1.4 XHTML에서 바뀐 점

XHTML에서는 `<` 기호 다음 공백문자가 있으면 문법 에러가 발생하는데, `<`를 HTML 엔티티 `&lt;`로 변경하거나, CDATA 섹션으로 감싸줄 수 있다. **브라우저가 CDATA 섹션을 지원하지 않으면 CDATA 마크업 앞에 자바스크립트 주석 기호를 써야 한다.**

### 2.2 인라인 코드와 외부 파일(src 속성)

외부 파일을 쓸 때 이점.

* 관리가 쉽다.
* 캐싱으로 페이지 불러오는 시간이 짧아진다.
* 외부 파일 불러오는 문법이 HTML과 XHTML 모두 똑같으므로, 위의 편법을 쓰지 않아도 된다.

### 2.3 문서 모드

IE 5.5는 쿽스와 표준의 두 가지 문서모드 개념을 처음 도입했다. 두 모드의 주요 차이는 콘텐츠 렌더링과 관련된 것이지만 자바스크립트에도 영향이 있다. 다른 브라우저 들도 이를 도입함에 따라 '거의 표준 모드'라는 엄격하지 않은 표준 모드가 등장했다. 이미지 주변의 공백과 테이블 이미지 등에서 차이가 크다.

쿼크 모드는 브라우저 사이의 일관성을 전혀 기대할 수 없으므로 독타입을 이용하여 표준 모드로 사용한다. 표준 모드와 '거의 표준' 모드는 차이를 느낄 수 없기 때문에 일반적으로 '표준 모드'라는 용어는 쿽스 모드를 제외한 둘 모두를 말한다.

### 2.4 `<noscript>` 요소

`<noscript>`는 브라우저가 자바스크립트를 지원하지 않거나 지원이 꺼져 있을 때 대체 콘텐츠를 제공하며, `<script>` 요소를 제외한 모든 HTML 요소를 사용할 수 있다. 브라우저에서 스크립트를 사용할 수 있을 때는 `<noscript>` 요소의 콘텐츠는 결코 표시되지 않습니다.

## 관련 글들

* [자바스크립트란 무엇인가](http://nolboo.github.io/blog/2014/03/20/javascript-for-web-developer-1/)
* [자바스크립트 제대로 배우기](http://nolboo.github.io/blog/2014/03/13/how-to-learn-javascript-properly/)
* [자바스크립트 제대로 배우기 스터디 그룹](http://nolboo.github.io/blog/2014/03/18/how-to-learn-javascript-properly-study/)