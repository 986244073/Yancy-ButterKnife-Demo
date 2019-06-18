# `Butter Knife`

在app的gradle里面导入依赖

```
implementation 'com.jakewharton:butterknife:10.1.0'
annotationProcessor 'com.jakewharton:butterknife-compiler:10.1.0'
```

在MainActivity中使用

```java
public class MainActivity extends AppCompatActivity {
    @BindView(R.id.mBtn)
    Button mBtn;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        //绑定初始化ButterKnife
        ButterKnife.bind(this);
        mBtn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(MainActivity.this, "好了", Toast.LENGTH_SHORT).show();
            }
        });
    }
}

```

gradle

```
buildscript {
    repositories {
        google()
        jcenter()
        mavenCentral()

    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.4.1'
        classpath 'com.jakewharton:butterknife-gradle-plugin:10.1.0'
    }
}
```

# app

java8

```
    // Butterknife requires Java 8.
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
```



```
//apply plugin: 'com.android.library'
//apply plugin: 'com.jakewharton.butterknife'
```

然后使用教程

```java
@BindView----> 绑定一个 view；id 为一个 view 变量
@BindView(R.id.tv_fm1)
TextView tvFm1;

@BindViews ----> 绑定多个 view；id 为一个 view 的 list 变量
@BindViews({ R.id.btn1,R.id.btn2 })
List buttons;

@BindArray----> 绑定 string 里面 array 数组；
@BindArray(R.array.city )
String[] citys ;

@BindBitmap----> 绑定图片资源为 Bitmap；
@BindBitmap(R.mipmap.wifi )
Bitmap bitmap;

@BindBool ----> 绑定 boolean 值

@BindColor ----> 绑定 color；
@BindColor(R.color.colorAccent)
int black;

@BindDimen ----> 绑定 Dimen；
@BindDimen(R.dimen.borth_width)
int mBorderWidth;

@BindDrawable ----> 绑定 Drawable；
@BindDrawable(R.drawable.test_pic)
Drawable mTestPic;

@BindFloat ----> 绑定 float

@BindInt ----> 绑定 int

@BindString ----> 绑定一个 String id 为一个 String 变量；
@BindString(R.string.app_name )
String meg;
```

fragment中使用

```java
@Override
public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
    view = inflater.inflate(R.layout.fragment_smart_home, container, false);
    ButterKnife.bind(this, view);
    initRecycerView();
    return view;
}
@Override
public void onDestroyView() {
    if (unbinder != null) {
        unbinder.unbind();
    }
    super.onDestroyView();
}
```

activity中使用

```java
@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        requestWindowFeature(Window.FEATURE_NO_TITLE);
        setContentView(R.layout.activity_main);
        ButterKnife.bind(this);
    }
```

adapter

```java
public class MyAdapter extends BaseAdapter {  

  @Override   
  public View getView(int position, View view, ViewGroup parent) {  
    ViewHolder holder;  
    if (view != null) {  
      holder = (ViewHolder) view.getTag();  
    } else {  
      view = inflater.inflate(R.layout.testlayout, parent, false);  
      holder = new ViewHolder(view);  
      view.setTag(holder);  
    }  

    holder.name.setText("Donkor");  
    holder.job.setText("Android");
    // etc...  
    return view;  
  }  

  static class ViewHolder {  
    @BindView(R.id.title) TextView name;  
    @BindView(R.id.job) TextView job;  

    public ViewHolder(View view) {  
      ButterKnife.bind(this, view);  
    }  
  }  
}  
```

