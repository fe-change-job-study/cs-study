# prepare_frontend_interview

## HTML/ CSS

<b>프론트엔드 기술 면접을 위한 핸드북 만들기</b>

## HTML 목차

- [DOCTYPE 🔥](#DOCTYPE)

  - DOCTYPE에 대하여 설명하시오
  - meta 태그에 대해서 알고 있나요?
  - meta 태그의 요소에 대해서 아는대로 말해보세요

- [웹 표준 및 웹 접근성 🔥](#웹-표준-및-웹-접근성)

  - 웹 표준이란?
  - HTML5에서 추가된 내용이 있나요?
  - 웹 접근성이란?
  - 웹 접근성에 맞는 마크업 예시 몇가지 말해보시오
  - 시멘틱 태그란 무엇인가 왜 사용하는가
  - 텍스트 관련 태그
  - SEO란 무엇인가?
  - Button 태그의 Default type은 무엇인가?
  - Section 태그와 article 태그의 차이점
  - 크로스 브라우징이란 무엇인가요?

- [그 외 🔥](#그-외)

  - 이미지 크기가 클 경우 렌더링 속도가 느려질텐데 이를 개선하기 위한 방법
  - UI란 무엇인지 설명하시오
  - 이미지 태그에 src 속성을 사용하는 이유는 무엇인가?
  - 왜 일반적으로 CSS `<link>`를 head 태그 사이에 위치시키고, JS `<script>` 태그를 body 직전에 위치시키는 것이 좋은 방법인지 설명하시오
  - `data-속성` 은 무엇에 좋은지 설명하시오

- [SVG란?🔥](#SVG란)

  - SVG 장점과 단점
  - SVG 내부 도형에 대해 아는게 있나요?

## CSS 목차

- [display 🔥](#display)

  - block 이란?
  - inline 이란?
  - inline-block 이란?
  - none 이란?

- [position 속성에 대하여 🔥](#position-속성에-대하여)

  - static
  - relative
  - fixed
  - absolute

- [float가 어떻게 작동하는가🔥](#float가-어떻게-작동하는가)

- [Flexbox나 Grid 각각의 특징🔥](#Flexbox나-Grid-각각의-특징)

  - flex 를 사용하는 이유가 무엇인가요?
  - Grid를 사용하는 이유가 무엇인가요?

- [이미지 태그를 스타일로 대체하는 법 🔥](#이미지-태그를-스타일로-대체하는-법)

- [반응형 웹의 3요소 🔥](#반응형-웹의-3요소)

- [CSS selector가 어떠한 원리로 동작하나요? 🔥](#CSS-selector가-어떠한-원리로-동작하나요?)

- [반응형웹과 적응형웹에 설명하시오 🔥](#반응형웹과-적응형웹에-설명하시오)

  - 반응형 웹이란?
  - 적응형 웹이란?

- [PX, EM에 대해 설명하시오 🔥](#PX,-EM에-대해-설명하시오)

- [CSS 적용 우선순위 🔥](#CSS-적용-우선순위)

- [CSS-in-JS에 대해서 설명해 주세요 🔥](#CSS-in-JS에-대해서-설명해-주세요)

- [CSS 전처리기를 사용해보셨나요? 🔥](#CSS-전처리기를-사용해보셨나요)

  - 사용해봤다면 장점과 단점

- [padding과 margin의 차이가 무엇인가요? 🔥](#padding과-margin의-차이가-무엇인가요)

  - padding에 대하여
  - margin에 대하여

- [리플로우와 리페인트에 대해 설명하시오 🔥](#리플로우와-리페인트에-대해-설명하시오)
  - 리플로우에 대하여
  - 리페인트에 대하여

## 리플로우와 리페인트에 대해 설명하시오

브라우저의 작동 방식부터 설명을 하자.

브라우저는 최초로 렌더링을 시작할 때 HTML, CSS, 자바스크립트 파일을 불러온다.

HTML 파일은 DOM Tree로 변환, CSS 파일은 CSSOM Tree로 변환한다.

이후 DOM Tree와 CSSOM Tree를 합쳐 Render Tree를 만든다.

이 때 display:none, head 같은 태그는 렌더 트리에서 제외된다.

이후 Render Tree를 기반으로 렌더링을 시작한다. 이 과정을 Layout이라고 한다.

마지막으로 요소에 스타일을 적용하는 Paint 과정을 거친다.

이 때 레이아웃과 페인트 과정을 최초로 그린 다음 레이아웃과 페인트 과정을 다시 그리는 것을 리플로우와 리페인트라고 한다.

### 리플로우

리플로우는 요소의 크기, 위치, 레이아웃 등이 변경되어 렌더 트리를 재생성하는 작업이다.

발생시점은

1. DOM 요소의 기하학적 속성이 변경될 때
2. 브라우저의 사이즈가 변할때

위 두 가지 경우에 발생한다.

리플로우는 비용이 상당히 큰 작업이다. 특정 요소에서 리플로우가 발생하면 주변요소(부모, 자식, 형제)에게 영향을 주기 때문이다.

또한 위 두가지 경우 외에도 offsetWidth, offsetHeight, clientWidth, clientHeight, scrollWidth, scrollHeight 등의 속성이 변경되거나 조회할때 발생한다.
https://gist.github.com/paulirish/5d52fb081b3570c81e3a

### 리페인트

리페인트는 변경된 요소를 화면에 그려주는 작업을 의미한다.

발생시점은

1. 리플로우가 발생했을때
2. 요소의 스타일(background, color, border 등)이 변경될 때
3. visibility가 변경될 때

리페인트는 요소의 스타일이 변경되었을 때 발생하므로 리플로우보다 비용이 적다.

### 어떻게 하면 리플로우, 리페인트를 줄일 수 있을까?

#### 1. 애니메이션 요소의 위치를 absolute, fixed로 두기

애니메이션으로 요소의 위치를 변경할 때, 주변 요소의 위치도 변경되어 리플로우가 여러번 발생한다.

리플로우가 여러번 발생하지 않도록, 애니메이션이 적용된 요소의 position을 absolute, fixed로 두면 된다.

#### 2. display: none 을 사용하기

display: none이 적용된 요소는 렌더트리에서 제외된다. 따라서 요소의 여러 스타일이 변경되어야하는 경우에는 display: none을 설정하고, 스타일을 변경한 뒤, display: block으로 변경하면 리플로우, 리페인트를 줄일 수 있다.

#### 3. DOM 속성 변경 코드 모으기

JS에서 DOM 속성을 변경할 때, 여러번 변경하는 것보다 한번에 변경하는 것이 좋다.

```typescript
  // BAD
  const el1 = document.querySelector('.target-first');
  el1.style.width = '10px';

  const el2 = document.querySelector('.target-second');
  el2.style.width = '10px';

  const el3 = document.querySelector('.target-third');
  el3.style.width = '10px';

  // GOOD

  const el1 = document.querySelector('.target-first');
  const el2 = document.querySelector('.target-second');
  const el3 = document.querySelector('.target-third');

  // dom의 스타일 변경 코드를 한 곳으로 모아둠
  el1.style.width = '10px';
  el2.style.width = '10px';
  el3.style.width = '10px';
```

브라우저의 리플로우 처리방식 때문

브라우저는 변경할 요소가 있을 때 즉시 처리하지 않고 큐에 저장한다.

큐에 변경 작업이 쌓였을 때 리플로우를 실행한다.

결국 DOM의 수저을 모아두면 이 수정코드가 큐에 쌓여있다 한번에 처리되기 때문에 리플로우 횟수를 줄일 수 있다.

#### 4. 리플로우 유발 함수의 호출을 제한하기

리플로우를 발생시키는 함수나 속성을 매변 호출하지 않고 변수에 저장한다.

#### 5. CSS로 스타일을 한 번에 변경하기

만약 DOM의 여러 스타일을 변경해야한다면, 스타일을 CSS클래스로 정의해두고 한번에 변경하자.

#### 6. 가상 DOM 사용하기

리액트나 뷰를 사용한다면 가상 DOM을 사용하기 때문에 리플로우, 리페인트를 줄일 수 있다.

가상 DOM은 생성한 DOM을 저장했다가 DOM에 변화가 있다면 메모리에 저장했던 DOM과 현재 변경된 DOM을 비고해 변경된 부분만 실제 DOM에 반영하기 때문이다.
