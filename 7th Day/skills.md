[TOC]

# Tips

## Know which activity u are in

* Create a new java class which extends `AppCompatActivity`, and override `onCreate()` method

### code

```java
public class BaseAcitvity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState){
        super.onCreate(savedInstanceState);
        Log.d("Base Activity",getClass().getSimpleName());
    }
}

```

then make other activity extends `BaseActivity` rather than `AppCompatActivity`

### result

```cmd
2019-09-27 10:08:11.156 18189-18189/com.wangs.launch_mode D/Base Activity: MainActivity
2019-09-27 10:08:19.124 18189-18189/com.wangs.launch_mode D/Base Activity: ThirdActivity
2019-09-27 10:08:21.164 18189-18189/com.wangs.launch_mode D/Base Activity: Second_activity
```

## Exit in any activity

* build a collection to manage all activity

1. create a class

   ```java
   public class ActivityCollector {
       public static List<Activity> activities = new ArrayList<>();
   
       public static void addActivity(Activity activity) {
           activities.add(activity);
       }
       public static void removeActivity(Activity activity){
           activities.remove(activity);
       }
       public static void finishAll(){
           for(Activity activity: activities){
               if(!activity.isFinishing()){
                   activity.finish();
               }
           }
           activities.clear();
       }
   }
   
   ```

   * This class create a list to store activities, which provide an `addActivity()` method to add  activity to the list, a `removeActivity()`  method to remove one and a `finishAll()` method to destroy all activity in the list.

   2. Then change code in activity

      * add in `onCreate()` method

      ```java
       ActivityCollector.addActivity(this);
      ```

      * add in `onDestroy()` method

      ```java
      ActivityCollector.removeActivity(this);
      ```

   3.  If you wanna to exit, only need to execute `ActivityCollector.finishAll();`

* additionally, add `android.os.Process.killProcess(android.os.Process.myPid());` after`onDestroy()` to make sure application entirely exit.

## Better way to launch an activity

If `SecondActivity` needs two important parameter to launch.

origin launch :

```java
                Intent intent = new Intent(ThirdActivity.this,Second_activity.class);
                intent.putExtra("param1","data1");
                intent.putExtra("param2","data2");
                startActivity(intent);
```

launch by a method:

```java
public static void actionStart(Context context, String data1, String data2){
    Intent intent = new Intent(context,Second_activity.class);
    intent.putExtra("param1",data1);
    intent.putExtra("param2",data2);
    context.startActivity(intent);
}
```

and launch by:

```java
actionStart(ThirdActivity.this,"data1","data2");
```

