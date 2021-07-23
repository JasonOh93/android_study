## Abstract & Interface
* ### [Abstract 알아보기](#abstract)
* ### [Interface 알아보기](#interface)
* ### [Abstract vs Interface 알아보기](#abstract-vs-interface)

<br>

----

<br>

## Kotlin 함수형 프로그래밍
* ### [참고 블로그1](https://medium.com/@sket8993/kotlin-%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%B4%88%EA%B0%84%EB%8B%A8-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-4dbf36dfc9a7),

<br>

----

<br>

## Abstract

* ### Abstract : 
    * 없거나 **하나 이상의 추상 메소드**를 가지는 것.
    * 추상 메소드 : 구현되어 있지 않은 abstract로 정의된 메소드.

[참고 블로그 1](https://velog.io/@jaeyunn_15/JavaKotlin-Interface-Abstract-class-%EC%B0%A8%EC%9D%B4-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0),

* 클래스 안에 메소드가 **한개**라도 추상메소드가 있다면 해당 클래스는 **반드시 abstract 클래스로 표기** 되어야 하며 **abstract와 final은 동시 표기 불가하다.**
* 일반적인 메소드도 있을 수 있고 추상 메소드가 있을 수도 있다.  
    **추상 클래스도 인터페이스처럼 추상 클래스가 아닌 클래스에서 상속을 받는다면 추상 메소드가 있을 경우 모두 구현해줘야 한다.(필수로 상속받아야하는 내용들 : Adapter를 extends할때 받아야하는 메소드처럼!!)**<br> 물론 추상클래스에서 추상 클래스를 상속 받는다면 모두 구현하지 않아도 된다.
* 추상클래스는 생성자를 가질 수 있다.  
    추상클래스는 인스턴스를 만들 수 없지만 추상 클래스를 상속받은 클래스를 통하면 인스턴스화가 가능하다.
* extens를 사용해서 상속 받으며 추상 클래스의 **궁극적인 목적은 상속을 위함**이다.

<br>

---

<br>

## Interface

* ### Interface : 
    * body가 비어있는 메소드들의 형태들만 써놓은 것이며 상속하는 클래스들에서 해당 메소드들의 내용을 구현해서 사용해야 하는 메소드들의 집합이다.
    * 개발 코드를 직접 수정하지 않고도 사용하고 있는 객체만 변경할 수 있도록 하기 위함!

[참고 블로그 1](https://velog.io/@jaeyunn_15/JavaKotlin-Interface-Abstract-class-%EC%B0%A8%EC%9D%B4-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0),

* 인터페이스 안의 모든 메소드들은 추상 메소드이다.
* 인터페이스는 final을 붙일 수 없고 인터페이스 변수들은 static이어야 한다.  
**즉, 인터페이스는 일반 변수를 가질 수 없다.**
* 인터페이스는 **생성자를 가질 수 없다.**  
인터페이스는 인스턴스를 만들 수 없지만 인터페이스를 구현한 클래스를 통해 인스턴스화가 가능하다.
* 접근 지정자가 아예 없거나 public 이거나 아님 abstract만 가능하다!  
다른 클래스에선 implements를 통해 구현한다.
* 하나 이상의 인터페이스를 상속할 수 있다.

<br>

---

<br>

## Abstract VS Interface

* 추상클래스와 인터페이스는 **둘 다 인스턴스화 하는 것이 불가**하다.
* 인터페이스는 **모든 변수가 기본적은 static final이며 모든 메소드가 public abstract이지만, 추상 클래스는 static이나 final이 아닌 필드를 지정할 수 있고 public, protected, private 메소드를 가질 수 있다.**
* 인터페이스를 구현하는 어떤 클래스는 다른 여러개의 **인터페이스를 다중 구현이 가능**하지만<br>
**추상 클래스는 상속을 통해 구현이 가능하기에 다중 상속이 불가**