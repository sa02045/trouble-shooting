## 문제

### 사용자가 쿠키를 차단하면 홈페이지가 동작하지 않고 흰 화면이 나오는 이슈

<img src="https://velog.velcdn.com/images/sa02045/post/a71b7d79-317e-4147-a42f-5242efe91056/image.png" width="600" />

## 원인

### "모든 쿠키 차단" 설정을 활성화 하면 Chrome은 Storage 접근을 차단한다

<img src="https://velog.velcdn.com/images/sa02045/post/3ec74bc1-9dfb-4de1-900d-a54ab6ca44f8/image.png" width="600"/>

<img src="https://velog.velcdn.com/images/sa02045/post/071f8612-0a93-4b27-a3de-87161696e1c4/image.png" width="600"/>

- 쿠키차단 설정을 하면 유저의 개인정보보호를 위해 쿠키나 localStorage와 같이 브라우저에 데이터를 읽고 저장하는 기능을 차단시킨다.

## 해결

1. 다형성을 사용하여 브라우저 Storage를 사용하지 못하는 경우 인메모리 Storage를 사용하기

<img src="https://velog.velcdn.com/images/sa02045/post/20b6bdf2-a77c-4393-8b8c-a2b32f0e653e/image.png" width="400"/>

```ts
class MemoryStorage implements SafeStorage {
  // 생략
}
class LocalStorage implements SafeStorage {
  // 생략
}

// 코드에서 window.localStorage 대신 safeLocalStorage를 사용하기
export const safeLocalStorage = storageAvailable("localStorage")
  ? new LocalStorage()
  : new MemoryStorage();
```

참고

- https://www.slash.page/ko/libraries/common/storage/README.i18n

2. Stroage Access API 사용하기

참고

- https://developers.google.com/privacy-sandbox/3pcd/storage-access-api?hl=ko
