## content

[TOC]



# Launch mode

change lunch mode bu change `<activity>` label `android:launchMode` property.

## `standard`

* Default mode
* Whenever launch an activity with standard mode, it will push a new activity into the `Back Stack` 

### code

* Add a button 

* ```java
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          Log.d("First Activity",this.toString());
          setContentView(R.layout.activity_main);
  
          Button but1 = (Button) findViewById(R.id.button1);
          but1.setOnClickListener(new View.OnClickListener(){
              @Override
                      public void onClick(View V){
                  Intent intent = new Intent(MainActivity.this,MainActivity.class);
                  startActivity(intent);
              }
  
          });
  
      }
  ```

### result

Click Button1 a new activity float out. Click Button1 for serval times, the press back, it returns to last activity, press back for enough time to back to menu.

## `singleTop`

If and only target activity is on the top of `Back Stack`, it will not be create any more.

### code1

```xml
        <activity android:name=".MainActivity"
            android:launchMode="singleTop">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
```

add `android:launchMode="singleTop"`

### result1

Click Button1, `MainActivity` no longer pop up.



But if target is not in the top of `Back Stack` it will be create.

### code2

```java
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second_activity);
        Button button = (Button) findViewById(R.id.button2);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(Second_activity.this, MainActivity.class);
                startActivity(intent);
            }
        });
    }
```

and make `MainActivity` launch `Second_activity`

### result

click `BUTTON1` or `BUTTON2` , keeps launch new activity.

## `singleTask`

Activity will exist at most one in `Back Stack` .

### code

```xml
        <activity android:name=".Second_activity"
            android:launchMode="singleTask"></activity>
        <activity android:name=".MainActivity"
            android:launchMode="singleTask">
```

### result

click `button1`, `Second_activity` launch, click `button2`, `Second_activity` exit, back to `MainActivity`

## `singleInstance`

`singleInstance` launch mode will create a new stack to store target activity.

* Use condition:

  If in a Application, there is an activity which was made for other activity to use, we can use `singleInstance` mode to create a stack which only store this kind activity.

### test

just make `MainActivity` launch `ThirdActivity`, `ThirdActivity` launch `Second_activity`, and `ThirdActivity` launch mode is `singleInstance`

### result

click `BUTTON1`, click `BUTTON3`, then click `BUTTON2`, press back, screen shows `BUTTON1`, `BUTTON2` , `BUTTON3` in alternate.





## plus

Yesterday was a busy day, and I didn't overcome my tired. In fact I could finish it at night yesterday. :<

But today I typed a lot, found I'm more familiar with Android Studio. Happy:>

Good Luck in the future.