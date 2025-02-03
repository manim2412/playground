# 스프링 부트 예외 처리 방식 2가지
## 1. @ControllerAdvice를 이용하여 모든 Controller에서 발생하는 예외 처리
## 2. @ExceptionHandler를 이용하여 특정 Controller에서 발생하는 예외 처리
[usage]
@ControllerAdvice로 모든 컨트롤러에서 발생할 예외를 정의하고, 
@ExceptionHandler를 통해 발생하는 예외마다 처리할 메소드를 정의
