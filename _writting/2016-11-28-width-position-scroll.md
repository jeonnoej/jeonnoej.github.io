---
layout: post
title:  "[JS] Element Size, Position, Scroll"
date:   2016-11-28 02:24:40 +0900
---

# 개요
viewport 체크, Sticky 등의 컴포넌트를 작업하다 보면 엘리먼트의 크기나 위치를 계산해야하는 경우가 생긴다.
각 속성과 함수들이 제공하는 값이 각 속성이나 함수마다 달라서 애를 먹는 경우가 많다.

아래는 넓이나 위치 등의 값을 제공해주는 프로퍼티, 함수이다.

# 크기 관련 속성
## offsetWidth / offsetHeight
 - border, padding 포함
 - margin 제외
 - $.outerWidth / $.outerHeight와 동일

## clientWidth / clientHeight
 - padding 포함
 - margin, border 제외
 - $.innerWidth, $.innerHeight와 동일

 ## clientTop / clientLeft
  - 요소의 테두리 넓이
  - read-only
  - clientLeft의 경우 텍스트의 방향이 오른쪽에서 -> 왼쪽이고 스크롤이 있는 경우 스크롤의 넓이를 포함 한다

## $.width / $.height
 - 순수 자신의 크기만을 기준으로 한다.
 - margin, border, padding 전부 제외된다.

## $.innerWidth / $.innerHeight
 - padding 포함
 - margin, border 제외

## $.outerWidth / $.outerHeight
 - border, padding 포함
 - margin 제외

---

# 위치 관련 속성
## offsetTop / offsetLeft
 - offsetParent 기준으로 border 경계선 까지의 거리
 - read-only property

## $.offset()
 - return {top: n, left: n}
 - 최상위 노드기준으로 border 경계선 까지의 거리

## $.position()
 - return {top: n, left: n}
 - offsetParent 기준으로 margin 경계선 까지의 거리

---

# 스크롤 관련 속성
## window.pageXOffset / window.pageYOffset
 - 왼쪽 상단 모서리 기준으로 스크롤된 픽셀의 크기를 리턴한다.
 - scrollX, scrollY와 동일

## .scrollTop / .scrollLeft
 - 엘리먼트의 스크롤 수직위치(Y좌표)를 반환한다. / 엘리먼트의 스크롤을 top 위치로 이동한다.
 - Read/Write
 - IE8 이전버전에서는 물리적인 좌표를 반환한다.
  예를 들어 화면이 200% 확대 되어있을 경우 2배 큰값을 반환한다.

## $.scrollTop() / $.scrollLeft
 - 엘리먼트의 스크롤 수직위치(Y좌표)를 반환한다. / 엘리먼트의 스크롤을 top 위치로 이동한다.
 - Read/Write
 - IE8 이전버전에서는 물리적인 좌표를 반환한다.
  예를 들어 화면이 200% 확대 되어있을 경우 2배 큰값을 반환한다.

## .scrollWidth / .scrollHeight

---

## object.getBoundingClientRect()
 - top : 상단으로부터 border 경계선 까지
 - left : 좌측으로부터 border 경계선 까지
 - right : left + padding + border
 - bottom : top + padding + border
 - width : width size + padding + border
 - height : height size + padding + border
