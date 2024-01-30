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
