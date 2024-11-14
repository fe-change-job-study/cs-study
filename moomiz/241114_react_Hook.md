# Hooks의 종류 🔥🔥
- ## 장점
  - 컴포넌트 간의 계층을 바꾸지 않고 상태로직을 재사용 할 수 있다.
  - 하나의 컴포넌트를 생명주기가 아닌 ## 기능을 기반으로 작은 함수 단위로 나눌 수 있다.
  - Class 문법 없이도 React 기능을 사용할 수 있게끔 해준다.
- ## Hook 규칙
  - 같은 훅 여러번 호출 가능
  - 컴포넌트 최상위에서만 호출가능.
  - React 함수 내에서만 호출 할 수 있다.
  - 비동기 함수(async가 붙은 함수)는 콜백함수로 사용할 수 없다. 
## useState
### 컴포넌트의 상태를 관리할 수 있는 hook
- 상태 값 변경 시 리렌더링이 발생한다.
- setState 호출 => 상태 변경 => 리렌더링 (변경된 상태 값 사용)
  
```
const [number, setNumber] = useState(1);
```
 
## useEffect
### 컴포넌트 내의 상태의 변화가 있을 때, 이를 감지하여 특정 작업을 해줄 수 있는 훅
- 일반적으로 sideEffect의 처리를 위해서 사용된다.
  - sideEffect란?
    - 컴포넌트가 화면에 렌더링된 이후에 비동기로 처리 되어야 하는 부수적인 효과들
    - 함수에서 함수 안의 내용물만으로 결과값을 만드는 것 외에 다른 행위들
    - 함수의 output를 만들기 위해 외부에 값을 사용하는 것
    - 외부 변수를 함수 안에서 변경시키는 것
      
### useEffect 사용법
```
useEffect(()=>{
},[])
``
- 두번째 인자로 어떤 값을 전달하는 지에 따라, 첫번째 인자로 전달된 콜백 함수가 언제 실행되는지가 결정된다.

### 아무것도 전달하지 않으면 
```
useEffect(()=>{
})// 아무것도 전달 x 
```
첫 렌더링(마운트)과 그 이후에 모든 업데이트에 대해서 effect를 수행하게 된다.
-> 클래스 컴포넌트의 componentDidMount, componenetDidUpdata를 합쳐놓은 것과 같다.
- 불 필요한 렌더링이 많이 생길 확률 있다.

### 빈 배열 전달
```
useEffect(()=>{
  console.log("Component Loaded");
},[]); // 컴포넌트가 마운트 됐을때만 실행된다. 
```
맨 처음 컴포넌트 생성 시, 즉 마운트 될 때만 실행된다.
=> 마운트 시 발생하는 렌더링 이후에 실행된다.

### 변수 전달 시, [count]
```
useEffect(()=>{
  document.title = `You clicked ${count} times`
},[count])
```
- 맨 처음 마운트 되었을 때와, count state의 값이 바뀔 때만 실행 된다. 

## useReducer
- 상태 업데이트 로직을 reducer 함수에 따로 분리 
## useMemo
- 의존성 배열에 적힌 값이 변할 때만 값 또는 함수를 다시 정의 
## useCallback
## useRef
  - DOM에 직접 접근할 때 사용
    => 리액트는 DOM으로의 직접 접근을 막고 있기 때문에 ref를 통해 접근해야한다.

  - 변수의 값이 변하더라도 리렌더링을 유발하고 싶지 않을 때 사용
    => ref 안에 저장되어 있는 값이 변경되어도 컴포넌트는 다시 렌더링 되지 않는다.
      또한 컴포넌트가 아무리 렌더링 되어도 ref 안에 저장되어 있는 값은 변화되지 않고 그댈 ㅗ유지
    => ref의 값은 컴포넌트의 전 생애주기를 통해 유지되기 때문,
      유지 기간 : 컴포넌트가 브라우저에 마운팅 된 시점 ~ 마운트가 해제될 때 까지
1. dom에 접근
```
const inputRef = useRef();
<input ref={inputRef} />
```
inputRef.current로 input 태그에 접근 가능
1-1. 하위 컴포넌트 dom 접근
App => Input 컴포넌트 접근
forwardRef 이용해서 접근 
```
function app(){
  const inputRef = useRef(); // useRef 선언 

  return (
  <div>
    <input ref={inputRef}/>// ref 전달 
    <button onClick={()=>inputRef.current.focus()}>Focus</button>
  </div>
  );
}
```
```
const Input = React.forwardRef(( _, ref ) => {
    return (
    <>
    	Input: <input ref={ref} />
    </>
    );
});

export default Input;
```
2. 리렌더링 유발하지 않는 변수로 사용
 - useRef 함수는 current 속성을 가지고 있는 객체를 반환하는데, 인자로 넘어온 초기값을 current 속성에 할당
 - current 속성을 변경해도 상태를 변경할 때 처럼 React 컴포넌트가 다시 랜더링 되지 않습니다.
 - 컴포넌트가 다시 렌더링 되어도 current 속성 값은 유실되지 않는다. 


## 커스텀 Hooks

- 개발자가 스스로 커스텀한 훅,이를 이용해 반복되느 로직을 함수로 뽑아내어 재사용 할 수 있다.
1. 상태관리 로직 재활용 가능
2. 클래스 컴포넌트보다 적응 양의 코드로 동일한 로직을 구현 할 수 있다.
3. 함수형으로 작성하기 때문에 보다 명료하다는 장점이 있다. 
