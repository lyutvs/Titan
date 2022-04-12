# 스프링 예외 발생 위치와 처리 방법

---
![](../../images/spring filter.png)

스프링의 처리 과정을 보면 예외가 발생하는 부분은 크게 두 가지로 나눌 수 있다.

1. `DispatcherServlet` 내에서 발생하는 예외 (Controller, Service, Repository 등)
2. `DispatcherServlet` 전의 서블릿(Filter)에서 발생하는 예외

[Dispatcher-Servlet?](https://github.com/lyutvs/Muttukttung-gamjachip/blob/main/spring%20boot/filter/Dispatcher-Servlet%3F.md)

[****DispatcherServlet 내에서 발생한 예외****](https://github.com/lyutvs/Muttukttung-gamjachip/blob/main/spring%20boot/filter/DispatcherServlet%20%EB%82%B4%EC%97%90%EC%84%9C%20%EB%B0%9C%EC%83%9D%ED%95%9C%20%EC%98%88%EC%99%B8.md)

[****DispatchherServlet 전에 발생한 예외 (Filter 에서 터진 에러)****](https://github.com/lyutvs/Muttukttung-gamjachip/blob/main/spring%20boot/filter/DispatchherServlet%20%EC%A0%84%EC%97%90%20%EB%B0%9C%EC%83%9D%ED%95%9C%20%EC%98%88%EC%99%B8.md)

[****HandlerExceptionResolver의 예외 처리 방법****](https://github.com/lyutvs/Muttukttung-gamjachip/blob/main/spring%20boot/filter/HandlerExceptionResolver%EC%9D%98%20%EC%98%88%EC%99%B8%20%EC%B2%98%EB%A6%AC%20%EB%B0%A9%EB%B2%95.md)