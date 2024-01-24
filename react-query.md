# react-query

## 1. 사용법

react-query을 사용하기 위해서는 우선 사용하고자 하는 컴포넌트를  
QueryClientProvider 컴포넌트로 감싸주고 QueryClient 값을 props로 넣어주어야 한다.  
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
useQuery는 queryKey, queryFn 두가지 인자값을 기본적으로 사용합니다.

```js
export const useTodoList = (params: TodoListFilter) => {
  return useQuery([TodoQueryKey.list], () => TodoService.list(params));
};
```

### 2. 1. queryKey

queryKey는 useQuery 마다 부여되는 고유 key값입니다.  
querykey는 query 캐싱을 관리합니다.

## 3. useMutaion

useMutaion는 데이터 변경(추가,수정,삭제) 작업을 할때 사용합니다.
