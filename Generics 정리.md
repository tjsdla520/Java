# 자바 개념정리

### <제네릭스(Generics)>

1. 제네릭스(Generics)란?

   - 컴파일시 타입을 체크해 주는 기능(compile-time type check)

   - 객체 타입의 안정성을 높이고 형변환의 번거로움을 줄여주기 때문에 코드가 간결해짐 

   - ClassCastException 을 막아 줄 수 있음(실행전에 확인가능 RuntimeException보다 빠르게 수정가능)

     ```java
     // 컴파일시에는 list.get(2)가 반환 타입이 object라서 Integer로 변환 시 문제 없으나 
     // 실행시에 list.get(2)가 String이기떄문에 ClassCastException(형변환)발생
     public class GenericTest{
         public static void main(String[] args){
             ArrayList list = new ArrayList();
             list.add(10);
             list.add(20);
             list.add("30");//String 추가
             Integer i = (Integer)list.get(2); //컴파일 ok
             
             System.out.println(list);
         }
     }
     
     // 컴파일에서 오류를 잡아주면 실행시에 더 간편하게 오류확인 가능 
     public class GenericTest{
         public static void main(String[] args){
             //1. Integer라는 타입정보를 컴파일러에게 주게되면 
             ArrayList<Integer> list = new ArrayList<Integer>();
             list.add(10); //2. = list.add(new Integer(10)); 로 변환됨
             list.add(20);
             list.add("30");//3. String 타입을 넣게 되면 잘못된 타입을 잡아준다.
             
             //Integer i = (Integer)list.get(2);
             Integer i = list.get(2);//형변환 생략가능 이미 integer로 선언했기때문
             
             System.out.println(list);
         }
     }
     ```

2.  타입 변수

   - 클래스를 작성할 때 Object타입 대신 타입변수(E)를 선언해서 사용

      일반클래스(object)  - > 제네릭 클래스(타입변수(E))  

     ```java
     public class ArrayList extends AbstractList{
         private transient Object[] elementData;
         public boolean add(Object o){}
         public object get(int index){}
     }
     
     public class ArrayList<E> extends AbstractList<E>{
         private transient E[] elementData;
         public boolean add(E o){}
         public E get(int index){}
     }
     ```

   - 객체 생성시, 타입 변수(E) 대신 실제 타입(Type)을 지정(대입) 

   - Tv 타입의 객체만 저장가능 다른 타입일 경우 컴파이 에러 발생
   
     ```java
     ArrayList<TV> tvList = new ArrayList<TV>();
     ```
   
3. 제네릭스 용어

   - 지네릭 클래스 

     ```java
     Box<T>
     ```

   - 타입 변수

     ```java
     T
     ```

   - 원시타입(raw type)

     ```java
     Box
     ```

   - 참조변수와 생성자의 대입된 타입을 일치해야 한다.

     (제네릭 클래스간, 매개변수의 다형성은 성립되나 대입된 타입은 다형성 성립x )

