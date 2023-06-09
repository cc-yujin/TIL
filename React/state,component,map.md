# 리액트에서 레이아웃 만들 때 쓰는 JSX 문법 3개

js 파일 안에서 html 쓰네?

실은 JSX라는 언어임

.js 파일에서 쓰는 html 대용품

### JSX 문법 1. class 넣을 땐 className
### JSX 문법 2. 데이터바인딩은 {중괄호}
### JSX 문법 3. style 넣을 땐 style={{스타일명 : '값'}} (오브젝트 형식으로)

참고: 먼가 코드를 잘못 짰을 때 에러 메시지는 터미널/브라우저/개발자도구에서 확인 할 수 있음

<br><br>

# state

return() 안에는 병렬로 태그 2개 이상 기입 금지

자료를 잠깐 저장할 땐 변수(var, let, const)를 쓴다.

근데 state 써도 됩니다.

1. import{ useState }
3. let[작명a, 작명b] = useState(보관할 자료)
- a 는 {a} 로 써서 변수 처럼 쓸 수 있고
- b 는 state 변경 도와주는 함수

Q. 변수 문법 있는데 왜 state 써야함?

- 일반 변수는 갑자기 변경되면 html에 자동으로 반영 안됨
- state쓰던 html은 자동 재렌더링됨

Q. state 언제 써야함?

- 변동시 자동으로 html에 반영되게 만들고 싶으면 state 쓰셈
- 블로그 제목은 당연히 안 써도 되겠지.. 매일 업뎃되는 사항이 아님

<br><br>

# 버튼에 기능개발을 해보자 & 리액트 state변경하는 법
### onClick 쓰는 법
- onClick={} 안에 함수이름을 넣는다   
### state 변경하는 법 
- 등호로 변경 금지. ex) 따봉변경(따봉 = 1) --> ❌
- state변경함수(새로운state) : 기존 state를 새로운 state로 갈아치움.

```jsx
let [따봉, 따봉변경] = useState(0);

<h4><span onClick={ () => {따봉변경(따봉+1);} }>👍</span> {따봉} </h4>
```
-> 👍 버튼을 누르면 0에서 1씩 증가한다.

<br><br>
# array, object, state 변경하는 법

```jsx
let [글제목, 글제목변경] = useState(['녹용','뿔','사슴'])

<button onClick={() => {
            글제목변경(['변경1', '변경2', '변경3'])
          }}
        >
          나는버튼👁
        </button>
```
이렇게 코딩하면 기존 state를 변경할 수 있겠지만, 변경할 때마다 모든 자료를 작성하기 힘들고 비효율적. 또한 array/object 다룰 때는 원본을 보존하는 방식으로 코딩하는 게 좋다. copy본 생성하기!

```jsx
<button onClick={() => {
            let copy = [...글제목];
            copy[0] = '배불러디짐';
            글제목변경(copy);
          }}
        >
          나는버튼👁
        </button>
```

**state변경함수 특징**

기존state와 신규state가 같을 경우 변경 안 해줌! (에너지절약..)   
state가 array/object면 독립적 카피본(shallow copy)을 만들어서 수정하기

<br><br>
# Component : 많은 div들을 한 단어로 줄이고 싶으면

html 넘 더러움… 만들다 보면 길어질텐데.. 축약하여 깔끔하게 해주는 ‘컴포넌트’문법이 있다

- 첨보는 사람도 이해 쉬울 듯
- 미래의 나도 이해 쉬울 듯

### 컴포넌트 만드는 법

1. function 생성 
(주의! 다른 function 바깥에 써야 하며, 영어대문자로 작명하기)
2. return() 안에 html 담기
- 하나의 태그로 시작하여 하나의 태그로 끝나야 함
- 두개의 `<div>` 병렬로 넣는다던가.. 그런 거 안됨
3. <함수명></함수명> 쓰기

- 근데! 나는 병렬적으로 태그 두개 이어진 걸 함수로 만들어야 한다. 하면 새로운 `<div>`로 묶어줘도 됨. 그치만 이러면 맨 바깥에 있는 `<div>`태그는 의미가 없음. 그럴 때  `<></>` 를 사용가능 (fragment 문법)

```jsx
function Modal() {
  return(
		<>
    <div className='modal'>
            <h4>제목</h4>
            <p>날짜</p>
            <p>상세내용</p>
      </div>
			<div>병렬로 넣고 시퍼</div>
		</>
  )
}
```

**어떤 걸 컴포넌트로 만들면 좋은가?**

1. 반복적인 것들
2. 큰 페이지들
3. 자주 변경되는 것들
4. 다른 팀원과 협업할 때 웹페이지를 컴포넌트 단위로 나눠서 작업을 분배하기도 한다

컴포넌트의 단점 
- state 가져다 쓸 때 문제 생김 (A함수에 있던 변수는 B함수에서 맘대로 가져다 쓸 수 없음. 당연함)

참고) 컴포넌트 만드는 문법2. 변수에 넣기

```jsx
const com = () => {
	return (
	<div></div>
)
}
```

- const로 쓰면 에러메시지 뜨는 이점이 있음

App.js 파일에서 쓰고 있는

function App() { } 이것도 사실 컴포넌트이다.

<br><br>
# 리액트 환경에서 동적인 UI 만드는 법 (모달창 만들기)

### 동적인 UI 만드는 step

1. html css로 미리 디자인 완성
2. UI의 현재 상태를 state로 저장
3. state에 따라 UI가 어떻게 보일지 작성 (조건문 등으로)

```jsx
let [modal, setModal] = useState(false);
```

- state 작명시 왼쪽 state 함수는 `set어쩌구`로 하는게 일반적 관습이다.

**state에 무슨 자료를 넣어야 하지?**

- 암거나 맘대로 하면 된다
- `‘닫힘’ / ‘열림’`, `0/1`, `true/false`

**JSX에서 조건문 쓰는 법 : 삼항연산자(ternary operator)**

JSX안에서는 if문을 바로 사용할 수 없다. 대신 삼항연산자를 JSX 중괄호 안에 쓰면 된다.

```jsx
조건식 ? 참일 때 : 거짓일 때
```
```jsx
{
  Modal == true ? <Modal /> : null
}
```

**제목 클릭시 모달창 띄우기?**

→ 클릭시 state만 조절하면 된다

<br><br>
# map : 많은 div들을 반복문으로 줄이고 싶은 충동이 들 때

### map() 함수가 몬데?

1. array 자료 갯수만큼 함수 안의 코드 반복 실행해줌
2. return 오른쪽에 있는 걸 array로 담아줌
3. 유용한 파라미터 2개(array자료, 1씩증가정수)

중괄호 안에서는 for반복문 못쓰니까 map을 쓰면 된다.

파라미터 2개까지 가능
- 첫번째는 array 자료 순서대로 반환
- 두번째는 반복문 돌 때마다 0부터 1씩 증가하는 정수

```jsx
{
        글제목.map(function(a, i){
          return (
          <div className='list' key={i}>
          <h4>{ a }</h4>
          <p>4월 23일 발행</p>
        </div>)
        })
      }
```

*{글제목[i]} or {a} 로 작성하면 된다.   
*반복문으로 html 생성하면 `key={html마다 다른숫자}` 추가해야 한다.

결론 : 비슷한 html 반복생성하려면 map() 쓰면 됩니다

<br><br>
