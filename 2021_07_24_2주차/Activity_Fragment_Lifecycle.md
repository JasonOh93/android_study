## Activity & Fragment Lifecycle
* ### [Activity 생명주기](#activity-lifecycle)
* ### [Fragment 생명주기](#fragment-lifecycle)

<br>

----

<br>

## Kotlin 함수형 프로그래밍
* ### [참고 블로그1](https://medium.com/@sket8993/kotlin-%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%B4%88%EA%B0%84%EB%8B%A8-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-4dbf36dfc9a7),

<br>

----

<br>

### 생명 주기는 Android 작동 방식의 핵심으로, 생명 주기를 준수하지 않으면 메모리 누출 또는 애플리케이션의 비정상 종료가 발생할 수 있습니다.

<br>

## Activity Lifecycle

* ### Activity class : Android 앱의 중요한 구성요소로 활동이 실행되고 결합되는 방식은 플랫폼 애플리케이션 모델의 기본 요소입니다.

[Android Developer Site](https://developer.android.com/reference/android/app/Activity), [Android Developer Site(한국어)](https://developer.android.com/guide/components/activities/activity-lifecycle?hl=ko)

![Activity 생명주기](./activity_lifecycle_imgs/activity_lifecycle_diagram_1.png)

**홈화면을 눌러서 나갈경우 onPause() -> onStop()상태로 나오며 이후 다시 들어오면 onRestart() -> onStart() -> onResume()으로 온다.**

* onCreate() : 시스템이 먼저 활동을 생성할 때 실행되는 것, **필수**
    * 활동의 전체 수명 주기 동안 **한 번만 발생**해야 하는 기본 애플리케이션 시작 로직을 실행합니다.
    *  onCreate() 메서드가 실행을 완료하면 시작됨 상태가 되고, 시스템이 연달아 onStart()와 onResume() 메서드를 호출합니다.
* onStart() : 활동이 시작됨 상태에 들어가면 시스텡이 호출
    * 활동이 사용자에게 표시되고, 앱은 활동을 포그라운드에 보내 상호작용할 수 있도록 준비합니다.
    * Ex) 이 메서드에서 앱이 **UI를 관리하는 코드를 초기화**합니다.
    * 이 메서드는 **매우 빠르게 완료**되고, 생성됨 상태와 마찬가지로 활동은 시작됨 상태에 머무르지 않습니다. 이 콜백이 완료되면 활동이 재개됨 상태에 들어갑니다.
* onResume() : 활동이 재개됨 상태에 들어가면 포그라운드에 표시되고 시스템이 호출
    * 어떤 이벤트가 발생하여 **앱에서 포커스가 떠날 때까지 앱이 이 상태에 머무릅니다.**
    * 예를 들어 전화가 오거나, 사용자가 다른 활동으로 이동하거나, 기기 화면이 꺼지는 이벤트가 이에 해당합니다.(포커스가 떠나는 행동)
    * 활동이 일시중지됨 상태에서 재개됨 상태로 돌아오면 시스템이 onResume() 메서드를 다시 한번 호출합니다.
* onPause() : 시스템은 사용자가 활동을 떠나는 것을 나타내는 첫 번째 신호로 이 메서드를 호출,<br> 즉 활동이 포그라운드에 있지 않게 되었다는 것을 나타냅니다.(다만 사용자가 멀티 윈도우 모드에 있을 경우에는 여전히 표시 될 수도 있음)
    * 수명 주기 구성요소는 구성요소가 포그라운드에 있지 않을 때 실행할 필요가 없는 기능을 모두 정지할 수 있습니다(예: 카메라 미리보기 정지)
    * 시스템 리소스, 센서 핸들(예: GPS) 또는 활동이 일시중지 중이고 사용자가 필요로 하지 않을 때 배터리 수명에 영향을 미칠 수 있는 모든 리소스를 해제할 수도 있습니다.
    * 멀티 윈도우 모드에서 여전히 완전히 보이는 상태일 수 있기 때문에, 멀티 윈도우 모드를 더욱 잘 지원하기 위해 UI 관련 리소스와 작업을 완전히 해제하거나 조정할 때는 onPause() 대신 onStop()을 사용하는 것이 좋습니다.
    * **아주 잠깐 실행**되므로 저장 작업을 실행하기에는 시간이 부족할 수 있습니다.
    * 애플리케이션 또는 사용자 데이터를 저장하거나, 네트워크 호출을 하거나, 데이터베이스 트랜잭션을 ***실행해서는 안 됩니다.***
    *  부하가 큰 종료 작업은 **onStop() 상태일 때 실행**
* onStop() : 활동이 사용자에게 더 이상 표시되지 않으면 중단됨 상태
    * 새로 시작된 활동이 화면 전체를 차지할 경우에 적용됩니다.
    * 수명 주기 구성요소는 구성요소가 화면에 보이지 않을 때 실행할 필요가 없는 기능을 모두 정지할 수 있습니다.
    * CPU를 비교적 많이 소모하는 종료 작업을 실행해야 합니다. 
    * 예를 들어 정보를 데이터베이스에 저장할 적절한 시기를 찾지 못했다면 onStop() 상태일 때 저장할 수 있습니다.
* onRestart() : 활동이 중단 되었다가 다시 시작되기 직전에 호출됩니다.
* onDestroy() : 활동이 소멸되기 전에 호출됩니다.
    * 시스템은 다음 중 하나에 해당할 때 이 콜백을 호출합니다.
        1. (사용자가 활동을 완전히 닫거나 활동에서 finish()가 호출되어) 활동이 종료되는 경우
        2. 구성 변경(예: 기기 회전 또는 멀티 윈도우 모드)으로 인해 시스템이 일시적으로 활동을 소멸시키는 경우
* onNewIntent() : 해당 활동에서 자신을 다시 호출 할 때 발동

<br>

---

<br>

## Fragment Lifecycle

[참고 블로그 1](https://ddangeun.tistory.com/50), [참고 블로그 2](https://re-build.tistory.com/4)

* ### Fragment : 앱 UI의 재사용 가능한 부분을 나타냅니다.
    *  자체 레이아웃을 정의 및 관리하고 자체 수명 주기를 보유하며 자체 입력 이벤트를 처리할 수 있습니다.
    * **독립적으로 존재할 수 없고** 활동이나 다른 프래그먼트에서 호스팅되어야 합니다. 
    * 액티비티(default : 백스택에 저장)와 프래그먼트(default : 백스택에 저장 안함)의 수명 주기에서 가장 중요한 차이점은 백스택에 저장되는 방법에 있습니다.

![Fragment 생명주기](./fragment_lifecycle_imgs/fragment_lifecycle_diagram_1.png)

* onAttach() : 프래그먼트가 액티비티와 연결되어 있었던 경우 호출, 여기서 액티비티가 전달됩니다.
* onCreate() : 프래그먼트를 생성할 때 호출, 프래그먼트가 일시정지 혹은 중단 후 재개되었을 때 유지하고 있어야 하는 것을 여기서 초기화 해야합니다. (Activity와 동일)
* onCreateView() : 프래그먼트가 생성된후 호출
    * 프래그먼트가 자신의 인터페이스를 **처음 그리기 위해 호출**합니다. 
    * **View를 반환**해야 합니다. 
    * 이 메서드는 **프래그먼트의 레이아웃 루트**이기 때문에 UI를 제공하지 않는 경우에는 null을 반환하면 됩니다.
    * 몇가지의 뷰들은 적절히 초기화 되어있지 않았을 수 있기 때문에 **findViewById 등을 사용하여 초기화 하지는 않아야** 합니다.
    * 그래서 View가 완전히 생성되었을때 호출되는 onViewCreated() 메서드에서 findViewById를 사용하여 초기화 해야 합니다. 
    * onViewCreated는 완전히 View가 생성되었음을 확신시켜줍니다.
* onViewCreated() : onCreateView가 실행 된 후에 실행, View가 모두 만들어 진 후에 작업을 진행할 수 있다.
* onActivityCreated() : deprecated되어 있습니다.<br>
Activity가 모두 만들어 진 후 실행하게 되는 메소드입니다.
* onStart() : 액티비티가 시작됨 상태에 들어가면 이 메서드를 호출합니다. (Activity와 동일)
    * 매우 빠르게 완료
    * 완료되면 Resumed(재개)상태로 들어가 onResume() 메서드를 호출합니다.
* onResume() : 사용자와 상호작용 합니다. (Activity와 동일)
* onPause() : (Activity와 동일)
    * 사용자가 프래그먼트를 떠나면 첫번 째로 이 메서드를 호출합니다. 
    * 사용자가 돌아오지 않을 수도 있으므로 여기에 현재 사용자 세션을 넘어 지속되어야 하는 변경사항을 저장합니다. 
* onStop() : (Activity와 동일)
* onDestoryView() : 프래그먼트와 연결된 View Layer가 제거되는 중일 때 호출됩니다.
* onDestroy() : (Activity와 동일)
* onDetach() : 프래그먼트가 액티비티와 연결이 끊어지는 중일 때 호출됩니다.

``` markdown
***테스트 용으로 확인 해본 액티비티와 프래그먼트의 확인 사항***

2021-07-20 14:51:07.307 13106-13106/com.jasonoh.lifecycletest E/TAG: MainActivity2 -> onCreate: 
2021-07-20 14:51:07.315 13106-13106/com.jasonoh.lifecycletest E/TAG: Fragment1 -> onAttach: 
2021-07-20 14:51:07.315 13106-13106/com.jasonoh.lifecycletest E/TAG: Fragment1 -> onCreate: 
2021-07-20 14:51:07.319 13106-13106/com.jasonoh.lifecycletest E/TAG: Fragment1 -> onCreateView: 
2021-07-20 14:51:07.319 13106-13106/com.jasonoh.lifecycletest E/TAG: Fragment1 -> onViewCreated: 
2021-07-20 14:51:07.323 13106-13106/com.jasonoh.lifecycletest E/TAG: Fragment1 -> onActivityCreated: 
2021-07-20 14:51:07.325 13106-13106/com.jasonoh.lifecycletest E/TAG: Fragment1 -> onStart: 
2021-07-20 14:51:07.325 13106-13106/com.jasonoh.lifecycletest E/TAG: MainActivity2 -> onStart: 
2021-07-20 14:51:07.326 13106-13106/com.jasonoh.lifecycletest E/TAG: MainActivity2 -> onResume: 
2021-07-20 14:51:07.326 13106-13106/com.jasonoh.lifecycletest E/TAG: Fragment1 -> onResume: 
2021-07-20 14:51:07.828 13106-13106/com.jasonoh.lifecycletest E/TAG: MainActivity -> onStop: 
```