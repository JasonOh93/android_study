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

* ### Generic : 
    * 클래스나 인터페이스 혹은 함수 등에서 동일한 코드로 여러 타입을 지원해주기 위해 존재
    * 사용하는 이유 :
        * 타입의 안정성을 제공하고 타입 체크와 형변환을 생략 가능하도록하여 코드가 간결해질수 있다.
        * 내가 사용하려는 형을 넣어주므로써 다른 타입은 사용할수 없는것이다.
        <br>예를 들어 list변수가 ArrayList```<String>``` 일 경우에는 Int형식은 넣어서 사용할 수 없도록 하는 것이다.
<br>    
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

[참고 블로그 1](https://medium.com/mj-studio/%EC%BD%94%ED%8B%80%EB%A6%B0-%EC%A0%9C%EB%84%A4%EB%A6%AD-in-out-3b809869610e), [참고 블로그 2](https://iosroid.tistory.com/70), [참고 블로그 3](https://mrgamza.tistory.com/419)

```kotlin
class Wrapper<T>(var value: T)

fun main(vararg args: String) {
    val intWrapper = Wrapper(1)
    val strWrapper = Wrapper<String>("1")
    val doubleWrapper: Wrapper<Double> = Wrapper<Double>(0.1)
}
```
* T : 형식 인자(Type parameter)
    * Int, String, Double등 여러 형식을 저장할 수 있습니다.

```kotlin
// 함수에 제네릭을 적용한 예시
fun <T : Comparable<T>> greaterThan(lhs: T, rhs: T): Boolean {
    return lhs > rhs
}
```
* List, MutableList, Set, MutableSet, Map 등도 초기화될 때 형식 인자를 한두개씩 받아서 어떤 데이터를 저장할 것인지를 사전에 알고있습니다.
* 타입 추론으로 listOf(1,2)가 자동으로 List```<Int>```로 추론이 될 수도 있습니다.

<br>

---

<br>

