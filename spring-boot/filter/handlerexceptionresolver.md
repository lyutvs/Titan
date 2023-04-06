# HandlerExceptionResolver의 예외 처리 방법

---

- Controller Level: `@ExceptionHandler`
- Global Level: `@ControllerAdvice`
- Method Level: `try/catch`

## 1. Controller Level: `@ExceptionHandler`

---

`@ExceptionHandler` 어노테이션을 통해 Controller의 메서드에서 throw된 Excpetion에 대한 공통적인 처리를 할 수 있다.

TestController내에서 발생하는 TestException에 대해서 예외가 발생하면 `controllerExceptionHandler` 메소드에서 모두 처리해준다

Controller 메서드 내의 하위 서비스 (Service, Repository등등)에서 예외가 발생하더라도,

중간에 처리하지 않는 이상 Controller단까지 예외가 던져지게 되고 `@ExceptionHandler`가 예외를 처리하게 된다.

**~~*그런데 거의다 비즈니스 로직 단에서 예외 처리를 해야겠죠...?*~~**

```java
@RestController
public class TestController {

    // 예외 핸들러
    @ExceptionHandler(value = TestException.class)
    public String controllerExceptionHandler(Exception e) {
        log.error(e.getMessage());
        return "/error/404";
    }

    @GetMapping("hello1")
    public String hello1() {
        throw new TestException("hello1 에러 "); // 예외 발생
    }

    @GetMapping("hello2")
    public String hello2() {
        throw new TestException("hello2 에러 "); // 예외 발생
    }
}
```

## 2. **Global Level: `@ControllerAdvice`**

`@ControllerAdvice`는 모든 Controller에서 발생하는 예외를 처리할 수 있게 해주는 어노테이션이다.

Q. Controller의 `@ExceptionHandler`와 ControllerAdvice의 `@ExceptionHandler`중 높은 우선순위는?

A. Controller의 `@ExceptionHandler`가 먼저다.

## 3. **Method Level: `try/catch`**

```java
public void subscribeTopic(List<User> users, NotificationRequest request) {
        try {
            for (int i = 0; i < users.size() / 1000; i++) {
                List<String> deviceTokenListToSubscribe = users.subList(i, i * 1000)
                        .stream().map(User::getDeviceToken)
                        .collect(Collectors.toList());

                FirebaseMessaging.getInstance(FirebaseApp.getInstance())
                        .subscribeToTopic(
                                deviceTokenListToSubscribe, request.getType().toString()
                        );
            }
        } catch (FirebaseMessagingException e) {
            log.error(e.getMessage());
        }
 }
```

알아서 try/catch ~~