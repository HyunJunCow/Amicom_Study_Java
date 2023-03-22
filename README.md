# Amicom 자바 스터디 연습장

- 아미콤 자바 스터디 전용 레포지토리입니다.
- 매 주차마다 학습 내용과 실습 내용을 README 파일과 main 클래스 파일에 자유롭게 작성합니다.
- 정해진 작성 형식은 없습니다.

## 1주차 배운 내용
- 
0. 참조 타입은 포인터의 개념과 유사하다.

1. new 연산자를 사용하는 것과 리터럴을 사용하는 것의 차이

  Heap 영역 안에 존재하는 Constant pool은 리터럴 상수 값을 저장하는 곳이다. 
  여기에는 String 뿐 아니라, 모든 종류의 숫자, 문자열, 식별자 이름, Class 및 Method 에 대한 참조와 같은 값이 포함된다. 
  String literal로 생성한 객체는 "String Pool"에 들어간다.
  String literal로 생성한 객체의 값(ex. "Cat")이 이미 String Pool에 존재한다면, 해당 객체는 String Pool의 reference를 참조한다. 
  그림에서 s1과 s2가 같은 곳을 가리키고 있는 것도 이 때문이다(https://url.kr/own6fv).
  반면, new 연산자를 사용하면 constant pool과는 별개로 heap 메모리 안에 독자적인 부분이 할당되게 된다.
  new 연산자로 생성한 String 객체는 같은 값이 String Pool에 이미 존재하더라도, Heap 영역 내 별도의 객체를 가리키게 된다(리터럴과는 다른 참조 타입을 가진다).
  
2. '==' 연산자는 참조 타입(번지)를 서로 비교하는 것이다.

3. 객체를 제거하는 방법은 객체의 모든 참조를 없애는 것이다(그 객체를 참조하는 변수가 더 이상 없도록 만들기).

4. str1.equals(str2) 메소드는 참조 타입과 무관하게 str1과 str2의 순수 문자만을 비교한다.

5. String.charAt(int index) 메소드를 통해 문자열에서 특정 인덱스의 문자 하나를 얻을 수 있다.

6. String.length() 메소드는 문자열의 길이를 int 형식으로 리턴한다(공백 포함).

7. 기존 문자열의 수정본(완전히 새로운 문자열)을 리턴하는 함수는 oldStr.replace("수정할 부분","어떻게 고칠 지");

8. 참조 타입 배열은 각 항목에 객체의 번지를 저장할 수 있다(포인터 배열이라고 이해할 수 있음).

9. System.arraycopy(원본 배열, 복사 시작 인덱스, 새 배열, 붙여넣기 시작 인덱스, 복사 항목 수) 메소드를 통해 배열을 복사할 수 있다.

10. 189p에서 newStrArray[3] = null인데 System.out.print(newStrArray[3])의 결과로 "null"이라는 문자열이 출력되는 것은 printIn 메소드를 분석하면 알 수 있다.
 
 public void println(Object x) {
     String s = String.valueOf(x);
     synchronized (this) {
         print(s);
         newLine();
      }
  }
  // String.class
  public static String valueOf(Object obj) {
     return (obj == null) ? "null" : obj.toString();
  }
  //
  public void print(String s) {
     if (s == null) {
         s = "null";
     }
     write(s);
  }
  public void print(Object obj) {
      write(String.valueOf(obj));
  }
  코드를 보고 의문이 드는 점은, 그냥 바로 print(Object obj) 메소드만 실행시키면 될 것 같은데(그 안에 valueOf 메소드가 포함되어 있으므로),
  왜 valueOf 메소드와 print(String s) 메소드를 호출하는 지였다(왜 굳이 2개의 메소드를?).
  아마 그 이유는 synchronized 불록에 있는 것 같아서 이에 대해 조사하였고, 그 내용은 다음과 같다.
  :블록으로 쓰인 synchronized 키워드는 해당 블록이 오직 한 스레드만이 실행될 수 있도록 보장하여 블록 내부에 있는 코드가 모두 실행되기 전에 다른 스레드가 이 블록에 접근하는 것을   막아 공유 자원에 대한 경쟁 조건을 방지할 수 있지만, 과도한 사용은 성능에 악영향을 미칠 수 있으므로 최대한 적게 사용하는 것이 좋다고 한다. 
  특히 syncrhonized 블럭 내의 static method 호출은 교착상태를 일으킬 수 있다고 하니 더욱 주의해야 한다고 한다(https://url.kr/nk1c7x). 
  
  11. 추가적으로, system.out에 대하여도 조사하였다. 
    java.io 파일에는 PrintStream class가 정의되어 있다.
    public class PrintStream extends FilterOutputStream implements Appendable, Closeable {
	    ...
  	  public void println(Object x) {
    	  	...
		   }
	   }
	    public void print(String s) {
		   ...
  	  }
    	@overroad
	   public void print(Object obj) {
	    	...
	    }
    }
  
    한편, java.lang 파일에는 System class가 정의되어 있다.
    public final class System {
          ...
         public static final PrintStream out = null;
         ...
    }
    PrintStream 객체 out이 static으로 선언되어 있으므로 System 객체를 생성하지 않고 바로 System.out을 사용할 수 있다.
  
  12. 

## 2주차 배운 내용
- 이곳에 작성하시면 됩니다.

## 3주차 배운 내용
- 이곳에 작성하시면 됩니다.

## 4주차 배운 내용
- 이곳에 작성하시면 됩니다.

## 5주차 배운 내용
- 이곳에 작성하시면 됩니다.

## 6주차 배운 내용
- 이곳에 작성하시면 됩니다.

## 7주차 배운 내용
- 이곳에 작성하시면 됩니다.

## 8주차 배운 내용
- 이곳에 작성하시면 됩니다.

## 9주차 배운 내용
- 이곳에 작성하시면 됩니다.

## 10주차 배운 내용
- 이곳에 작성하시면 됩니다.
