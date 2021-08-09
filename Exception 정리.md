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

   1. Exception클래스 및 모든 자손클래스 : 외적인 요소에 의해 발생하는 예외

      ex) IOException : 입출력 예외 / ClassNotFoundException : 클래스가 존재하지 않음

   2. RuntimeException클래스 : 개발자의 실수로 발생하는 예외

      ex) ArihmeticException : 산술계산 예외(0으로 나눌때) / ClassCastException : 형변환 예외 / 

      NullPointerException : 널포인트 예외(참조변수가 null 일 때) / IndexOutOfException : 배열범위 벗어남

4. 예외 처리 방법 (try-catch 문)

   ```java
   try{
       	//예외가 발생할 가능성이 있는 문장
   	} catch(Exception e1){
           //e1이 발생시 처리하기 위한 문장
       } catch(Exception e2){
   		//e2이 발생시 처리하기 위한 문장    
   	} catch(Exceprion eN){
       	//eN이 발생시 처리하기 위한 문장
   	}
   
   ```

5. printStackTrace()와 getMessage()

   - printStackTrace() : 예외발생 당시의 호출스택에 있던 메소드 정보와 예외 메세지를 화면에 출력
   - getMessage() : 발생한 예외 클래스의 인스턴스에 저장된 메세지

6.  멀티 catch 블럭

   - 내용이 같은 catch 블럭을 하나로 합친것

   - 합쳐지는 두개의 클래스가 부모 자식관계 일땐 성립불가( 쓸이유가 없음 : 조상것으로 처리하면 됨)

   - ex) ExceptionA, ExceptionB 둘중 하나만 있는 메소드는 호출 불가, 공통된 메소드만 사용가능(instanceof로 형변환 해서 사용 가능)

     ```java
     try{
         
     }catch(ExceptionA e ){
         e.printStackTrace();
     }catch(ExceptionB e2) {
         e2.printStackTracce();
     }
     
     //위와 동일
     try{
         catch(ExceptionA | ExceptionB e){
             e.printStackTrace();
         }
     }
     ```

7.  예외 발생시키기

   - 연산자 new를 이용해서 발생시키려는 예외 클래스를 객체로 만든 다음 키워드 throw를 이용해서 예외를 발생 시킨다.(throw 하게되면 catch에서 잡는다. )

     ```java
     Exception e = new Exception("고의로 예외 객체 생성");
     throw e;
     //e.getMessage() : "고의로 예외 객체 생성"
     ```

8.  checked, unchecked 예외

   - checked 예외 : 컴파일러가 예외 처리 여부를 체크(예외 처리 필수) -> Exception과 그 자손
   - unchecked 예외 : 컴파일러가 예외 처리 여부를 체크 안함(예외 처리 선택) -> RuntimeException과 그자손

9. 메소드 예외 선언

   - try-catch 이외의 예외처리하는 방법으로 예외 처리가 아니라 호출시에 처리하는 것  

     ```java
     void method() throws Exception1, Exception2, ExceptionN{
         //메소드 내용
     }
     
     void method() throws Exception{
         //메소드 내용
     }
     ```

10.  finally 블럭

    - 예외 발생 여부와 상관없이 수행되는 코드
    - try-catch에서 동일하게 실행되는 코드를 finally{}블럭에 넣는다.

11. 사용자 정의 예외

    - 사용자가 직접 예외 클래스로 처리하는것
    - 조상은 Exception, RuntimeException중에서 선택하여 처리가능하다.

    ```java
    class MyException extends Exception{
        MyException(String msg){ //문자열을 매개변수로 받는 생성자
            super(msg);//조상인Exception클래스의 생성자를 호출한다.
        }
    }
    ```

12. 예외 되던지기(exception re-throwing)

    - 예외를 분담 처리 시에 사용함. 예외 처리 후 다시 예외를 발생키시는 것

    - 호출한 메소드와 호출된 메소드 양쪽에서 모두 예외처리를 하는 것

      ```java
      class ExceptionTest{
          public static void main(String[] args){
              try{
                  method1();
              } catch(Exception e){ //4. 다시발생된 예외 처리
                  System.out.println("main 메소드에서 예외처리 완료");
              }
          }
          
          static void method1() throws Exception{
              try{
                  throw new Exception(); //1. 예외발생
              } catch(Exception e){
                  System.out.println("method1메소드에서 예외처리 완료");//2. 예외처리
                  throw e; //3. 다시 예외 발생
              }
          }
      }
      ```

13.  연결된 예외(chained exception)

    - 하나의 예외가 다른 예외를 발생키시는 것 ( 예외A가 예외B를 발생킬시 A는 B의 원인 예외(cause exception))

    - 하나의 예외 안에 또 다른 예외를 포함시키는 것

    - 여러 예외를 하나의 예외로 묶어서 처리 가능

    - checked 예외를 unchecked예외로 변경하여 처리 가능

      ```java
      public class Thorwable implements Serializable{
          //Throwable : Exception과 Error의 조상
          private Throwable cause = this; //객체 자신(this)을 원인 예외로 등록
          
          public synchronized Throwable initCause(Throwable cause){
              this.cause = cause; //cause를 원인 예외로 등록
              return this;
          }
      }
      ```

      

