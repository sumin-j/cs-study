##브라우저 렌더링 동작 과정

###웹 브라우저의 구조

![Basic structure of the browser](https://blog.kakaocdn.net/dn/99dKj/btqIl9g441B/2zBd7Ya63bkgHiSdM8Vm4k/img.png)

- `User Interface` : 주소 표시줄, 이전/다음/새로고침 버튼 등 웹페이지를 제외하고 사용자와 상호작용하는 사용자 인터페이스
- `Rendering Engine` : HTML과 CSS를 파싱하여 요청한 웹 페이지를 표시하는 렌더링 엔진
- `Browser Engine` : 유저 인터페이스와 렌더링 엔진을 연결하는 브라우저 엔진
- `Networking` : 각종 네트워크 요청을 수행하는 네트워킹 파트
- `UI Backend` : 체크박스나 버튼과 같은 기본적인 위젯을 그려주는 UI 백엔드 파트
- `Data Persistence` : localStorage나 Cookie와 같이 보조 기억장치에 데이터를 저장하는 파트
- `Javascript Interpreter` : 자바스크립트 코드를 실행하는 인터프리터 (크롬의 경우 V8)

###렌더링 엔진의 목표

1. HTML,CSS,JS,이미지 등 웹 페이지에 포함된 모든 요소들을 화면에 보여준다.
2. 업데이트가 필요할 때, 효율적으로 렌더링을 할 수 있도록 자료 구조를 생성한다.
   여기서 업데이트는 사용자 동작으로 인해서 입력 발생, 스크롤 발생, 애니메이션 동작, 비동기요청으로 인한 데이터 로딩 등

###Critical Rendering Path

1. HTML 파일과 CSS파일을 파싱해서 각각 Tree를 만든다. (Parsing)
2. 두 Tree를 결합하여 Rendering Tree를 만든다. (Style)
3. Rendering Tree에서 각 노드의 위치와 크기를 계산한다. (Layout)
4. 계산된 값을 이용해 각 노드를 화면상의 실제 픽셀로 변환하고, 레이어를 만든다.(Paint)
5. 레이어를 합성하여 실제 화면에 나타낸다. (Composite)

- `Parsing`

  - HTML파일을 해석하여 DOM(Document Object Model) Tree를 구성하는 단계 <br/>
  - 파싱 중 HTML에 CSS가 포함되어 있다면 CSSOM(CSS Object Model) Tree구성도 함께한다.
    <br/>

- `Style`

  - Parsing 단계에서 생성된 DOM Tree와 CSSOM Tree를 매칭시켜서 Render Tree 구성
    <br/>

  **Render Tree는 실제로 화면에 그려진 Tree**
  **화면에 표시되어야 할 모든 노드의 컨텐츠, 스타일 정보를 포함하는 Tree**

          ex) visibility:hidden; //요소가 공간을 차지하고, 보이지만 않기 때문에 Render Tree 포함

              display:none; // 이 경우는 Render Tree에서 제외된다.

- `Layout` / `Reflow`

  - Render Tree를 화면에 어떻게 배치해야 할 것인지 노드의 정확한 위치와 크기를 계산한다.
    <br/>

- `Painting`

  - Layout 단계에서 계산된 값을 이용해 Render Tree의 각 노드를 화면상의 실제 픽셀로 변환, 이때 픽셀로 변환된 결과는 하나의 레이어가 아닌 여러 개의 레이어로 관리
  - CSS 규칙이 작으면 작을수록 Paint 시간 단축
    <br/>

- `Composite`
  - Paint 단계에서 생성된 레이어를 합성하여 실제 화면에 나타낸다.
  - 화면에서 웹 페이지를 볼 수 있다.
    <br/>

**UI가 업데이트되는 3가지 상황**

1. 다시 Layout이 발생하는 경우

   - 주로 요소의 크기나 위치가 바뀔 때, 혹은 브라우저 창의 크기가 바뀌었을 때 다시 발생
     <br/>

2. Paint부터 다시 발생되는 경우

   - 주로 배경 이미지나 텍스트 색상, 그림자 등 레이아웃의 수치를 변화시키지 않는 스타일의 변경이 일어났을 때 발생
     <br/>

3. 레이어의 합성만 다시 발생하는 경우 (포토샵 레이어와 비슷)

   - Layout과 Paint를 수행하지 않고 레이어의 합성만 발생하기 때문에 성능상으로 가장 큰 이점을 가짐
     <br/>

####DOM과 Virtual DOM
자바스크립트 로직에 의해 항목 중 한 군데라도 변화가 일어나면 DOM의 모든 항목은 다시 그려진다. 이에 따라 속도가 저하된다.

반면에, 리액트는 DOM을 추상화한 객체인 Virtual DOM이라는 것을 일종의 사본처럼 미리 생성해두고 항목에 변화가 생기면 전체 UI를 Re-render를 한다. 그러나 새로 렌더된 뷰를 다시 그리는 것이 아닌 DOM과 비교 후 바뀐 부분만 실제 DOM에 적용하여 새로 그려지도록 한다.

따라서 상대적으로 속도가 빠르다.
