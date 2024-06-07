## 문제

사용자가 뒤로가기를 하면 모달을 띄우는 기능에서 특정 iOS에서만 페이지 진입시에 모달이 뜨는 이슈

## 원인

### 특정 iOS 버전의 safari에서 페이지 진입시에 popstate 이벤트를 발생시킴

- https://stackoverflow.com/questions/28441025/ignore-safaris-initial-page-load-popstate

1. popstate 이벤트는 브라우저의 세션 히스토리가 변경될 때 발생하는 이벤트
2. 주로 사용자가 브라우저의 뒤로 가기 버튼이나 앞으로 가기 버튼을 클릭할 때 발생하거나
3. history.back(), history.forward(), history.go() 메서드를 호출할 때 발생

## 해결

- page load 상태를 저장하는 변수를 생성하여 page load가 완료되었을 때에만 popstate를 listen하도록 해결

```js
let page_loaded = false;

window.addeventlistener("popstate", () => {
  if (isIos()) {
    if (!page_loaded) {
      page_loaded = true;
      return false;
    }

    // 모달 띄우기
  }
});
```
