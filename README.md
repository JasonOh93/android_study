# android_study


<br>

----

<br>

## Design Pattern
* ### [MVC](#mvc-디자인-패턴)
    * [EX_CODE](./ex_sorce_code/ex_mvc_sorce_code.md)
* ### [MVP Pattern](#mvp-디자인-패턴)
    * [EX_CODE](./ex_sorce_code/ex_mvp_sorce_code.md)
* ### [MVVM Pattern](#mvvm_pattern)
* ### [flux Pattern](#flux_pattern)

<br>

----

<br>

## 마크다운 문법 주의
* ### 내부 링크로 가는 아이디의 경우 소문자로 만들어야 함

----

<br>

[참고 블로그 1](https://velog.io/@iamjoo/mvc-mvp-mvvm-flux-%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4-86ocg4bf), [참고 블로그 2](https://heegs.tistory.com/17), [참고 블로그 3](https://stonybean.blogspot.com/2019/03/blog-post.html)<br>
[MVC Ex Code 참고사이트 1](https://protocoderspoint.com/model-view-controller-android-mvc-example-login-validation/), [MVC Ex code 참고사이트 2](https://jroomstudio.tistory.com/21)<br>
[MVP Ex code 참고사이트 1](https://cjw-awdsd.tistory.com/9), [MVP Ex code 참고사이트 2](https://youngest-programming.tistory.com/111)<br>
[의존성 참고 블로그](https://velog.io/@huttels/%EC%9D%98%EC%A1%B4%EC%84%B1%EC%9D%B4%EB%9E%80),

## MVC 디자인 패턴
### MVC (Model View Controller)

<br>
<img src="./mvc_images/mvc_image_pattern_diagram1.png" width="200px" alt="MVC DESION PATTERN DIAGRAM">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img src="./mvc_images/mvc_image_pattern_diagram2.png" width="230px" alt="MVC DESION PATTERN DIAGRAM">
<br><br>

**상태가 변경되었다는 정보를 View와 Model이 서로 양방향으로 주고받는 형태**

* Model : 데이터 처리하는 부분
* View : 화면 UI 담당
* Controller : 사용자의 입력을 받고 Model, View의 중개인 역할을 담당
    * 사용자의 입력이 들어오면 View와 Model에게 각각 어떠한 일을 할지 알려주는 역할<br>
    때문에 View와 Model의 ***의존성 (A는 B없이 작동할 수 없고 B를 재사용하지 않으면 A또한 재사용할 수 없다.)*** 이 생기고, Controller를 통해 복잡하게 연결되면 유지보수가 어려워진다.

* 특징 : 
    * Controller와 View는 ***1:1*** 관계가 아닌 ***1:N*** 관계로, Controller가 여러 개의 View를 선택하여 Model을 나타낼 수 있다.
    * View와 Model 서로간의 의존성이 높다는 단점이 있다.<br/><br/>
    따라서, View와 Model간의 **의존성을 최대한 낮게 설계한 경우** 좋은 MVC 패턴이라 할 수 있다.
<br>

---

<br>

## MVP 디자인 패턴
### MVP (Model View Presenter)

<br>
<img src="./mvp_images/mvp_image_pattern_diagram1.png" width="300px" alt="MVC DESION PATTERN DIAGRAM">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<br><br>

* Model : 데이터 처리하는 부분
* View: 화면 UI 담당 + 사용자 입력 받음
* Presenter: View와 Model 사이에서 자료 전달 역할

* 특징 : 
    * Presenter를 통해 Model, View **완벽하게 분리**가 가능합니다.
    * View와 Presenter의 관계는 **1:1** 입니다.
    * 앱이 커질수록 View와 Presenter의 의존성이 생기게 됩니다.
    * MVC에서는 사용자의 이벤트에 Controller가 먼저 반응한 후 View를 가져와 적절한 작업 후 반환한다.<br>
    MVP에서는 사용자의 이벤트에 View가 먼저 반응한 후 Presenter에 알리고 작업을 처리한 후 View한테 다시 알려준다.
    * Contrller와 역할이 비슷하지만 Interface를 사용한다는 것의 차이가 있다.<br> 
    View에서 전달된 이벤트에 따라 Model에서 데이터 요청후 전달하는 중간 역할 담당.
<br>

---
