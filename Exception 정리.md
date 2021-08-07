# 자바 개념정리

### <예외처리(Exception)>

1. 프로그램 오류
   * 컴파일 에러(compile-time error) : 컴파일 할 때 발생하는 에러
   * 런타임 에러(runtime error) : 실행 할 때 발생하는 에러/ 종류(error, exception)
   * 논리적 에러(logical error) : 작성 의도와 다르게 동작

``` java
//컴파일러 역할 : 구문체크/번역/소스코드의 최적화 
public class ExceptionTest{

	public static void main(String[] args){
		System.out.println(args[0]);
    }
}
//원래는 이렇게 다 확인을 해야하나 이클립스나 인텔리제이 같은 툴들이 알아서 처리를 해줌
```

2. 예외 처리 정의와 목적

   - 정의 : 프로그램 실행시 발생할 예외 발생을 대비한 코드
   - 목적 : 프로그램의 비정상 종료를 막고, 정상 실행상태 유지

3. Exception & RuntimeException

   - Exception클래스 및 모든 자손클래스 : 외적인 요소에 의해 발생하는 예외

      ex) IOException : 입출력 예외 / ClassNotFoundException : 클래스가 존재하지 않음

   - RuntimeException클래스 : 개발자의 실수로 발생하는 예외

      ex) ArihmeticException : 산술계산 예외 / ClassCastException : 형변환 예외 / 

     NullPointerException : 널포인트 예외 / IndexOutOfException : 배열범위 벗어남

