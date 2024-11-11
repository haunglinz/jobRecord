### 优点
1. 不用在业务模块写重复的代码。比如try cache
### 缺点
1. 无法明确的自定义捕获异常和异常后的处理

### 做法
1. 在springboot中用@RestControllerAdvice或者@ControllerAdvertise注解，定义一个全局异常处理的handler，然后使用注解@ExceptionHandler注解在方法上处理异常