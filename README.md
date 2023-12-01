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


```java
package org.example;

import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ForkJoinPool;

public class Main {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        long startTime = System.currentTimeMillis();
        Test t = new Test();
        ForkJoinPool customThreadPool = new ForkJoinPool(4); // 원하는 스레드 수로 조정
        CompletableFuture<String> futureFirst  =t.CompletableFutureTestMethod("first",customThreadPool);
        CompletableFuture<String> futureSecond =t.CompletableFutureTestMethod("second",customThreadPool);
        CompletableFuture<String> futureThird =t.CompletableFutureTestMethod("third",customThreadPool);
        CompletableFuture.allOf(futureFirst, futureSecond, futureThird).join();
        System.out.println(futureFirst.get());
        System.out.println(futureSecond.get());
        System.out.println(futureThird.get());

        long endTime = System.currentTimeMillis();
        long elapsedTime = endTime - startTime;
        System.out.println("메서드 실행 시간: " + elapsedTime + " 밀리초");
    }


}

class Test {
    public CompletableFuture<String> CompletableFutureTestMethod(String message,ForkJoinPool customThreadPool) {

        return CompletableFuture.supplyAsync(() -> {
            for (int i = 0; i < 1000000; i++) {
                System.out.println(message + i);
            }
            return "success";
        }, customThreadPool);
    }
}
```