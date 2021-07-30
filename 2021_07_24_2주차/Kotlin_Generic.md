## Android Generic
* ### [Generic 알아보기](#generic)

<br>

----

<br>

## Kotlin 함수형 프로그래밍
* ### [참고 블로그1](https://medium.com/@sket8993/kotlin-%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%B4%88%EA%B0%84%EB%8B%A8-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-4dbf36dfc9a7),

<br>

----

<br>

## Generic

[참고 블로그 1](https://medium.com/mj-studio/%EC%BD%94%ED%8B%80%EB%A6%B0-%EC%A0%9C%EB%84%A4%EB%A6%AD-in-out-3b809869610e), [참고 블로그 2](https://iosroid.tistory.com/70), [참고 블로그 3](https://mrgamza.tistory.com/419), [참고 블로그 4](https://lcw126.tistory.com/336?category=815752)

* ### Generic : 
    * 클래스나 인터페이스 혹은 함수 등에서 동일한 코드로 여러 타입을 지원해주기 위해 존재
    * 사용하는 이유 :
        * 타입의 안정성을 제공하고 타입 체크와 형변환을 생략 가능하도록하여 코드가 간결해질수 있다.
        * 내가 사용하려는 형을 넣어주므로써 다른 타입은 사용할수 없는것이다.
        <br>예를 들어 list변수가 ArrayList```<String>``` 일 경우에는 Int형식은 넣어서 **사용할 수 없도록** 하는 것이다.
<br>    
<br>

    | 형식 매개변수 이름 | 의미 |
    |:-----:|:---------:|
    | E | 요소(Element) |
    | K	| 키(Key) |
    | N	| 숫자(Number) |
    | T | 형식(Type) |
    | V	| 값(Value) |
    | S, U, V etc | 두 번째, 세 번째, 네 번째 형식(2nd, 3rd, 4th types) |

<br>

## variance는 자바에서 와일드 카드(Wild card)와 비슷
<br>

### Java Wild Card
* T : Read / Write 모두 가능
* ? extends T : Read만 가능한 서비스타입 와일드 카드
* ? super T : Write만 가능한 슈퍼 타입 와일드 카드

### Kotlin Variance
* T : Read / Write 모두 가능
* out T : Read만 가능
* in T : Write만 가능

<br>

* T : 형식 인자(Type parameter)
    * Int, String, Double등 여러 형식을 저장할 수 있습니다.

<br>

### 주 생성자나 부 생성자에 형식 매개변수를 지정해 사용할 수 있습니다.
```kotlin
class MyClass<T>(val myProp: T){}   //  주 생성자의 프로퍼티

class MyClass<T>{
    val myProp: T   // 프로파티
    constructor(myProp: T){ //  부 생성자 이용
        this.myProp=myProp
    }
}

//오류 상황
class MyClass<T>{
    val myProp: T   // 오류! 프로퍼티는 초기화되거나 abstract로 선언되어야 함
}
```

### 형식 매개변수에 null이 가능한 제네릭 클래스
```kotlin
class GenerucNull<T>{   //  기본적으로 null이 혀용되는 형식
    fun EqualityFunc(arg1: T, arg2: T){
        println(arg1?.equals(arg2))
    }
}
fun main(){
    val obj = GenerucNull<String>() //  non-null로 선언됨
    obj.EqualityFunc("Helllo","World")  //  null이 허용되지 않음
    
    val obj2 = GenerucNull<Int?>()  //  null이 가능한 형식으로 선언됨
    obj2.EqualityFunc(null,10)  //  null 사용
}
```

### null을 허용하지 않으려면 Any 자료형 사용
```kotlin
class GenerucNull<Any>{   //  자료형 Any가 지정되어 null을 허용하지 않음
   ...
}

val obj2 = GenerucNull<Int?>()  //  오류! null이 허용되지 않음
```

### 제네릭 메서드
```kotlin
fun <T> genericFunc(arg: T): T? {...}	//	매개변수와 반환 자료형에 형식 매개변수 T가 사용됨
fun <K, V> put(key: K, value: V): Unit{...}	//	형식 매개변수가 2개인 경우
```

### 배열의 인덱스 찾기
```kotlin
fun <T> find(a: Array<T>, Target: T): Int{
    for(i in a.indices){
        if(a[i] == Target) return i
    }
    return -1
}
fun main(){
    val arr1: Array<String> = arrayOf("Apple", "Banana", "Cherry", "Durian")
    val arr2: Array<Int> = arrayOf(1,2,3,4)

    println("arr.indices ${arr1.indices}")  //  indices는 배열의 유효 범위 반환   //  arr.indices 0..3
    println(find<String>(arr1, "Cherry"))   //  요소 C의 인덱스 찾기    //  2
    println(find(arr2,2))   //  요소 2의 인덱스 찾아내기  //  1
}

```
* List, MutableList, Set, MutableSet, Map 등도 초기화될 때 형식 인자를 한두개씩 받아서 어떤 데이터를 저장할 것인지를 사전에 알고있습니다.
* 타입 추론으로 listOf(1,2)가 자동으로 List```<Int>```로 추론이 될 수도 있습니다.

<br>

---

<br>

