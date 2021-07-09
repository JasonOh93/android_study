# MVVM EXAMPLE SORCE CODE
* ## MODEL VIEW VIEWMODEL
	* [Model](#model)
	* [ViewModel](#view-model)
	* [View](#view)
    * [참고 사이트](https://github.com/stonybean/DesignPatterns/tree/master/app/src/main/java/com/github/stonybean/designpattern_sample/MVVM)

----

<br>

![Android MVVM Project Structure](/mvvm_images/mvvm_image3.png)
Android MVVM Project Structure  <br><br>

<br>

# Model

## Model.Java (class)

```java
package com.github.stonybean.designpattern_sample.MVVM;

/**
 * Created by stonybean on 2019. 2. 1.
 */
class Model {
    String clickedTextView() {
        return "Hello World! - MVVM";
    }
}
```

# View Model

## ViewModel.java (class)

```java
package com.github.stonybean.designpattern_sample.MVVM;

import android.app.Activity;
import android.view.View;
import android.widget.TextView;

import com.github.stonybean.designpattern_sample.R;

/**
 * Created by stonybean on 2019. 2. 1.
 */

class ViewModel {
    private Activity activity;
    private Model model;
    private TextView textView;

    ViewModel(Activity activity) {
        this.activity = activity;
        this.model = new Model();
        initView();
    }

    private void initView() {
        textView = activity.findViewById(R.id.textView);
        textView.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                textView.setText(model.clickedTextView());
            }
        });
    }
}
```

# View

## MVVMActivity (class)

```java
package com.github.stonybean.designpattern_sample.MVVM;

import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;

import com.github.stonybean.designpattern_sample.R;

/**
 * Created by stonybean on 2019. 2. 1.
 */

public class MVVMActivity extends AppCompatActivity {
    private ViewModel viewModel;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_basic);

        viewModel = new ViewModel(MVVMActivity.this);
    }
}
```
* MainActivity의 경우 Android 내부에서 View일수도 있으며 Controller일수도 있다.