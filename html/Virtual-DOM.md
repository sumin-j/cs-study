## Virtual DOM

---

### React의 존재이유

- 큰 SPA(Single Page Application) 또는 Dynamic UI의 웹페이지를 만들기 위한 목적
  `SPA: Single Page Application : 페이지 전환없이 서비스를 이용할 수 있는 애플리케이션 UI`

### Virtual DOM

- regular DOM의 추상화 개념을 활용한 새로운 DOM이다. 이것은 빈번한 repaint/reflow`(브라우저 레이아웃 렌더링 중 연산할 때 리소스를 가장 많이 잡아먹는 연산)`문제를 보안했으며, regular DOM보다 최적의 성능을 발휘한다.
  <br/>

- `reflow` : 색상이 변경되거나 글자의 내용이 바뀌었을 때 발생되는 연산
- `repaint` : 하나의 DOM객체의 크기나 위치가 변경되었을 때
  <br/>

![browser layout engine](https://i.imgur.com/0XdloJi.png)

**React가 가상돔을 반영하는 절차**

1. 데이터가 업데이트 되면, 전체 UI를 Virtual DOM에 리렌더링
2. 이전 Virtual DOM에 있던 내용과 현재의 내용을 비교함 (가상 돔 끼리 비교)
3. 바뀐 부분만 실제 DOM에 적용이 됨 (컴포넌트가 업데이트 될때 , 레이아웃 계산이 한번만 이뤄짐)

**Virtual DOM vs DOM**
![Comparison of Virtual DOM and DOM](https://codingmedic.files.wordpress.com/2020/11/virtualdom.png?w=1024)

**결론**
작은 규모의 레이아웃(리플로우)이 여러번 발생하는 것보다
큰 규모의 레이아웃이 한 번 발생하는 것은 성능상의 큰 차이를 나타냄
