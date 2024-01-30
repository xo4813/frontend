# recoil

## 1. 사용법

recoil을 사용하기 위해서는 우선 사용하고자 하는 컴포넌트를 `RecoilRoot` 컴포넌트로 감싸주어야한다.  
만약 앱 전체에 사용하고자 한다면 최상의 컴포넌트에 감싸주면 된다.

- 최상위 컴포넌트 감싸는 예시 코드

```js
export default function App({ Component, pageProps }: AppProps) {
  return (
    <RecoilRoot>
      <Component {...pageProps} />;
    </RecoilRoot>
  );
}
```

## Atoms

Atoms는 상태의 단위이며, 업데이트와 구독이 가능하다. atom이 업데이트되면 각각 구독된 컴포넌트는 새로운 값을 반영하려고 다시 랜더링 된다.

- atoms 생성

```js
const todoState = atom({
  key: "fontSizeState",
  default: 14,
});
```

## useRecoilState

useRecoilState hook은 atom의 state를 get,set 할수있게 해줍니다

```js
const [fontSize, setFontSize] = useRecoilState(fontsizeState);
```

## useRecoilValue

useRecoilValue hook은 atom의 state를 get 할수있게 해줍니다

```js
const fontSize = useRecoilValue(fontsizeState);
```

## useSetRecoilValue

useSetRecoilValue hook은 atom의 state를 set 할수있게 해줍니다

```js
const setFontSize = useSetRecoilValue(fontsizeState);
```

## Selector

state 데이터 가공이 필요할경우 사용한다, get 프로퍼티를 사용하여
state를 가공후 반환할수 있다.

```js
const filteredTodoListState = selector({
  key: "filteredTodoListState",
  get: ({ get }) => {
    const filter = get(todoListFilterState);
    const list = get(todoListState);

    switch (filter) {
      case "Show Completed":
        return list.filter((item) => item.isComplete);
      case "Show Uncompleted":
        return list.filter((item) => !item.isComplete);
      default:
        return list;
    }
  },
});
```
