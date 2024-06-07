## 문제

프론트엔드 배포가 이루어지면 사용자가 chunkLoadError를 겪는 문제

- chunkLoadError는 webpack 기준 Error이다. (vite에서는 preloadError)
- chunkLoadError는 code Splitting으로 분리된 chunk를 Dynamic import로 불러오지 못해 발생하는 문제다.

## 원인

간단히 말하면 파일 hash가 변경되어 존재하지 않는 chunk를 가져오려는 문제이다.

아래 블로그 글에 자세히 기술

[Chunk Load Error 문제이해편](https://sa02045.github.io/chunk-load-error/)

## 해결

[Chunk Load Error 해결편](<https://sa02045.github.io/chunk-load-error(2)/>)

- 여러가지 해결 방법이 있지만 가장 간단한 방법으로 해결
- chunk를 불러오지 못하면 새로고침을 발생시켜 새로운 index와 chunk를 불러오도록 해결

```ts
window.addEventListener("vite:preloadError", (event) => {
  window.location.reload();
});
```
