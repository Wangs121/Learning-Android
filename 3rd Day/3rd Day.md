## Content

[TOC]

## 1 Create a second activity

### 1.1 add a button

> id = @+id/button

#### 1.1.1 layout  config

``` xml
layout_width = "wrap_content"	//width as text
layout_width = "match_parent"	//width as screen
```

## 2 Intent

> 各阻间之间进行交互的一种重要方式。其不仅可以知名当前组件想要执行的动作，还可以在不同阻间之间传递数据。

### 2.1 显式Intent

#### 2.1.1 method:

``` java
Intent(Context packageContext, Class<?>);
```

> Context is launched activity
>
> Class is target activity

``` java
startActivity(Intent);
```

> to start target Intent.

#### 2.1.2 code

change onClick method to:

``` java
            public void onClick(View v) {
                Intent intent = new Intent(FirstActivity.this, Second_activity.class);
                startActivity(intent);}
```

#### 2.1.3  resualt

Click button1 , jump to page with button 2.

### 2.2 隐式Intent

>不明确指出想要启动哪个活动，而是指定了一系列更为抽象的action和category等信息，然后交由系统去分析这个Intent，并帮我们找到合适的活动去启动

#### 2.2.1 config

``` xml
<activity>
    <inter-filter>
        //Your config
    </inter-filter>
</activity>
```

#### 2.2.2 code

> add below code in AndroidMainfest.xml

```xml
        <activity android:name=".Second_activity">
            <intent-filter>
                <action android:name="android.intent.action.ACTION_START" />
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
```

in <action> label we assign that current activity will respond 

"com.wangs.noactivity.ACTION_START" action

> In FirstActivity.java change to:
>
> ```java
>             public void onClick(View v) {
>                 Intent intent = new Intent("android.intent.action.ACTION_START");
>                 startActivity(intent);
>             }
> ```
>
> Every intent could assign only one action, but it could assign more than one category. So far, intent only assigned a default category, here we assign another by add
>
> ```java
>  intent.addCategory("android.intent.category.MY_CATEGORY");
> ```
>
> after intent object.

#### 2.2.3 run

While click button, we got an Error:

``` bat
E/AndroidRuntime: FATAL EXCEPTION: main
    Process: com.wangs.noactivity, PID: 6689
    android.content.ActivityNotFoundException: No Activity found to handle Intent { act=android.intent.action.ACTION_START }
```

which shows no Activity could respond that intent.

add 

```xml
<category android:name="android.intent.category.MY_CATEGORY" />
```

will solve it

> Besides CHECK your WORD SPELL !!!

#### 2.2.4 resualt

click button1 jump to the page with button 2

### 2.3 More Usage about  Intent

#### 2.3.1 Open web with Browser

Simply replace code with :

``` java
Intent intent = new Intent(Intent.ACTION_VIEW);
                intent.setData(Uri.parse("http://www.baidu.com"));
```

#### 2.3.2 expand

there are more commands in <inter-filter> label :

```xml
<intent-filter>
    <data>
    	android:scheme = ""<?指定数据协议?>
        android:host = ""<?主机名称?>
        android:port = ""<?指定数据的端口部分?>
    </data>
</intent-filter>
```

etc.

#### 2.3.3 Try to respond Internet Intent

* Create a new Empty Activity

* Add a button 

* Add:

* ``` xml
          <activity android:name=".Third_Activity">
              <intent-filter>
                  <action android:name="android.intent.action.VIEW" />
                  <category android:name="android.intent.category.DEFAULT" />
                  <data android:scheme="http"/>
              </intent-filter>
          </activity>
  ```

*  run the app

*  click button1, noactivity app was in the chosen list

#### 2.3.4 start a call

* Change code to :

  ```java
                  Intent intent = new Intent(Intent.ACTION_DIAL);
                  intent.setData(Uri.parse("tel:10086"));
  ```

* run the app, click button, jump to call app, with 10086 number.
* 

