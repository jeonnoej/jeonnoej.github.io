---
layout: post
title:  "[JS] Viewport 체크하기"
date:   2016-11-29 18:57:57 +0900
---

# 개요
Lazyload나 Scroll-Spy 기능을 구현하기 위해서 Viewport를 체크하는 기능이 필요하다.
현재 ViewPort안에 들어와 있는 엘리먼트의 리스트나 특정 엘리먼트가 Viewport에 존재하는지 여부를 파악하는 함수를 개발하기 위해
현재 Opensources 들에서는 어떤 형식으로 Viewport를 체크하는지 확인해볼 필요가 있다.

## jQuery-scrollspy
1. 스크롤 이벤트 발생 시 Viewport의 영역을 구한다.
{% highlight javascript %}
var $win = $(window);
var top = $win.scrollTop(),
    left = $win.scrollLeft(),
	right = left + $win.width(),
	bottom = top + $win.height();
{% endhighlight %}

2. 대상 엘리먼트리스트를 반복하며 엘리먼트가 Viewport 영역에 포함되는지 확인한다.
{% highlight javascript %}
var hits = $();
$.each(elements, function(i, element) {
    var elTop = element.offset().top,
    	elLeft = element.offset().left,
    	elRight = elLeft + element.width(),
    	elBottom = elTop + element.height();

    var isIntersect = !(elLeft > right ||
    	elRight < left ||
    	elTop > bottom ||
    	elBottom < top);

    if (isIntersect) {
    	hits.push(element);
    }
});
{% endhighlight %}


## egjs-infiniteGrid

## jQuery-lazyload
