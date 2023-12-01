### CompletableFuture 테스트

```text
CompletableFuture 를 사용하여 비동기 통신을 하기 위해 테스트로 만든 서버와 클라이언트
서버 : localhost:9091
클라이언트 : localhost:9092
```
### 테스트 방법
```text
1. CompletableFutureTestServer 실행
2. CompletableFutureTestClient 실행
3. 테스트 시작
http://localhost:9091/  - 동기 방식
http://localhost:9091/future - 비동기 방식

동기방식은 15초
비동기 방식은 5초의 시간이 소요됨
```