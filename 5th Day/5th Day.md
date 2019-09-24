## content

[TOC]



## Experience Activity Lifecycle

create an new project, add two activity:

'Normal_Activity'

```xml
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="This is a normal activity"
        />
```

'dialog activity'

```xml
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="This is a dialog activity"
        />
```

### configuration  in 'AndroidMainfest.xlm'

```xml
        <activity android:name=".dialog_activity"
            android:theme = "@style/Theme.AppCompat.Dialog"
        />
```

### Add two buttons in 'activity_main.xm'

```xml
    <Button
        android:id="@+id/normal"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="normal"
        tools:layout_editor_absoluteX="64dp"
        tools:layout_editor_absoluteY="272dp" />

    <Button
        android:id="@+id/button2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="dialog"
        tools:layout_editor_absoluteX="239dp"
        tools:layout_editor_absoluteY="279dp" />
```

### MainActivity.java

```java
package com.wangs.activitylifecycle;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;

public class MainActivity extends AppCompatActivity {

    public static final String TAG = "MainActivity";
    @Override
    protected void onStart() {
        super.onStart();
        Log.d(TAG,"onStart");
    }

    @Override
    protected void onStop() {
        super.onStop();
        Log.d(TAG,"onStop");
    }

    @Override
    protected void onRestart() {
        super.onRestart();
        Log.d(TAG,"onRestart");
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        Log.d(TAG,"onDestroy");
    }

    @Override
    protected void onPause() {
        super.onPause();
        Log.d(TAG,"onPause");
    }

    @Override
    protected void onPostResume() {
        super.onPostResume();
        Log.d(TAG,"onResume");
    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        Log.d(TAG,"onCreate");
        setContentView(R.layout.activity_main);
        Button normal_b = (Button) findViewById(R.id.normal_button);
        Button dialog_b = (Button) findViewById(R.id.dialog_button);
        normal_b.setOnClickListenter(new View.OnClickListener(){
            @Override
            public void onClick(View V) {
                Intent normal_intent = new Intent(MainActivity.this, Normal_Activity.class);
                startActivity(normal_intent);
            }
        });
        dialog_b.setOnClickListener(new View.OnClickListener(){
            @Override
            public void onClick(View V){
                Intent dialog_intent = new Intent(MainActivity.this, dialog_activity.class);
                startActivity(dialog_activity);
            }
        });
    }
}

```

## What if Activity was collected by System

Activity provides a method 'onSaveInstanceState()' method, which will execute before activity was collected

```java
    @Override
    protected void onSaveInstanceState(@NonNull Bundle outState) {
        super.onSaveInstanceState(outState);
        String tempData = "Something you just typed.";
        outState.putString("data_key",tempData);
    }
```

> Ctrl+O shortcut

and in 'onCreate()' method, parameter savedInstanceState is what we saved before.

```java
        if(savedInstanceState != null){
            String tempData = savedInstanceState.getString("data_key");
            Log.d(TAG,tempData);
        }
```

