#### 在项目的project的build.gradle文件中添加

```
  implementation "com.jakewharton:butterknife:10.0.0"
  androidTestImplementation "com.jakewharton:butterknife-compiler:10.0.0"
  annotationProcessor 'com.jakewharton:butterknife-compiler:10.0.0'
```

#### 在Activity中绑定ButterKnife

```java
  @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        ButterKnife.bind(this);
    }
```

#### 由于使用了java8的新特性,故需要

```java
android {
	...
    compileOptions{
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}
```

