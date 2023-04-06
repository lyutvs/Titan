# DispatchherServlet 전에 발생한 예외 (Filter 에서 터진 에러)

---

DispatcherServlet 전의 서블릿(Filter)에서 발생하는 예외는 `HandlerExceptionResolver`의 처리를 받을 수 없다.

Filter에서 예외가 발생하면 Web Application 레벨에서 처리를 해줘야 한다.

### 해결 방

---

1. web.xml 에서 error-page 등록, 사용자에게 에러 응답
2. Filter 내부 예외 처리를 위한 Filter 생성, try-catch문을 사용하여 예외 처리
3. Filter 내부 try-catch문에서 발생한 예외를 HandlerExceptionResolver를 빈으로 주입받아 `@ExceptionHandler`에서 처리