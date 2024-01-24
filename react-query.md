# react-query

데이터 Fetching, 캐싱, 동기화, 서버쪽 데이터 업데이트 등을 쉽게 만들어 주는 React 라이브러리

## 1. 사용법

react-query을 사용하기 위해서는 우선 사용하고자 하는 컴포넌트를 `QueryClientProvider` 컴포넌트로 감싸주고 `QueryClient` 값을 props로 넣어주어야 한다.  
만약 앱 전체에 사용하고자 한다면 최상의 컴포넌트에 감싸주면 된다.

- 최상위 컴포넌트 감싸는 예시 코드

```js
export default function App({ Component, pageProps }: AppProps) {
  const queryClient = new QueryClient();

  return (
    <QueryClientProvider client={queryClient}>
      <Component {...pageProps} />;
    </QueryClientProvider>
  );
}
```

## 2. useQuery

useQuery는 서버로 부터 데이터를 조회할때 사용합니다  
useQuery는 `queryKey`, `queryFn` 두가지 인자값을 기본적으로 사용합니다.

| 인자       | 설명                                                              |
| :--------- | :---------------------------------------------------------------- |
| `queryKey` | useQuery 마다 부여되는 고유 key값입니다. query 캐싱을 관리합니다. |
| `queryFn`  |                                                                   |

- useQuery 사용 예시 코드

```js
export const useTodoList = (params: TodoListFilter) => {
  return useQuery([TodoQueryKey.list], () => TodoService.list(params));
};
```

## 3. useQueries

여러개의 useQueries를 한번에 실행하고자 하는 경우 기존의 promise.all()처럼 묶어서 사용할수 있다.
두개의 반환값은 배열로 묶어서 반환된다.

```js
const results = useQueries({
  queries: [
    { queryKey: ["testKey1"], qyeryFn: () => TodoService.list(params) },
    { queryKey: ["testKey2"], qyeryFn: () => TodoService.list(params) },
  ],
});
```

## 4. useMutation

useMutation 데이터 변경(추가,수정,삭제) 작업을 할때 사용합니다.

```js
export const useTodoPost = () => {
  const queryClient = useQueryClient();

  return useMutation(TodoService.post, {
    onSuccess: () => {
      return queryClient.invalidateQueries([TodoQueryKey.list]);
    },
  });
};
```
