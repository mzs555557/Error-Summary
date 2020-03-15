

#### 底部tab栏的selector的状态

- android: state_pressed="true/fase" `按下状态下使用`

- android: state_focused="true/false" `聚焦状态下使用`

- android:state_selected="true/false" `被选中状态下使用`

- android:state_active="true/false" `勾选状态时使用`

- android:state_checkable="true/false"  `勾选状态下使用`

- ````xml
  <!--底部导航栏选中与未选中图标的颜色-->
  <?xml version="1.0" encoding="utf-8"?>
  <selector xmlns:tools="http://schemas.android.com/tools" xmlns:android="http://schemas.android.com/apk/res/android">
      <item android:drawable="@mipmap/icon_discover_press" android:state_pressed="true"/>
      <item android:drawable="@mipmap/icon_discover_press" android:state_focused="true" />
      <item android:drawable="@mipmap/icon_discover_press" android:state_checked="true" />
      <item android:drawable="@mipmap/icon_discover_press" android:state_selected="true"/>
    <item android:drawable="@mipmap/icon_discover_press" android:state_active="true" />
      <item android:drawable="@mipmap/icon_discover_press" android:state_checkable="true"/>
      <item android:drawable="@mipmap/icon_discover_press" android:state_activated="true"/>
  
      <item android:drawable="@mipmap/icon_discover" android:state_pressed="false"/>
      <item android:state_focused="false" android:drawable="@mipmap/icon_discover"/>
      <item android:state_checked="false" android:drawable="@mipmap/icon_discover"/>
      <item android:state_selected="false" android:drawable="@mipmap/icon_discover"/>
      <item android:state_active="false" android:drawable="@mipmap/icon_discover"/>
      <item android:state_checkable="false" android:drawable="@mipmap/icon_discover"/>
      <item android:drawable="@mipmap/icon_discover" android:state_activated="false"/>
  </selector>
  ````
  
- ```xml
  <!--底部导航栏选中与未选中字体的颜色-->
  <?xml version="1.0" encoding="utf-8"?>
  <selector xmlns:android="http://schemas.android.com/apk/res/android">
  
      <item  android:state_pressed="true" android:color="#EB4F38"/>
      <item  android:state_focused="true" android:color="#EB4F38"/>
      <item  android:state_checked="true" android:color="#EB4F38"/>
      <item  android:state_selected="true" android:color="#EB4F38"/>
      <item  android:state_active="true" android:color="#EB4F38"/>
      <item  android:state_checkable="true" android:color="#EB4F38"/>
      <item  android:state_activated="true" android:color="#EB4F38"/>
  
      <item android:state_pressed="false" android:color="#000"/>
      <item android:state_focused="false" android:color="#000"/>
      <item android:state_checked="false" android:color="#000"/>
      <item android:state_selected="false" android:color="#000"/>
      <item android:state_active="false" android:color="#000"/>
      <item android:state_checkable="false" android:color="#000"/>
      <item android:state_activated="false" android:color="#000"/>
  </selector>
  ```

  

#### 底部导航栏的制作
```java
public class MainActivity extends FragmentActivity {

    private LayoutInflater mInflater;
    private FragmentTabHost mTabHost;

    ArrayList<Tab> tabs = new ArrayList<>(5); //set count of tabs
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        initTab();
    }

    private void initTab() {
        Tab home = new Tab(R.mipmap.icon_home, R.string.home, HomeFragment.class);
        Tab my = new Tab(R.mipmap.icon_user, R.string.my, MyFragment.class);
        Tab cart = new Tab(R.mipmap.icon_cart, R.string.cart, CartFragment.class);
        Tab discover = new Tab(R.mipmap.icon_discover, R.string.discover, DiscoverFragment.class);
        Tab Hot = new Tab(R.mipmap.icon_hot, R.string.hot, HomeFragment.class);

        tabs.add(home);
        tabs.add(my);
        tabs.add(cart);
        tabs.add(discover);
        tabs.add(Hot);

        mInflater = LayoutInflater.from(MainActivity.this);
        mTabHost = this.findViewById(android.R.id.tabhost);
        mTabHost.setup(MainActivity.this, getSupportFragmentManager(), R.id.realtabcontent);


        for (Tab tab : tabs) {
            TabHost.TabSpec mTabSpec = 			 mTabHost.newTabSpec(String.valueOf(tab.getText()));
            View view = getBundleView(tab);
            mTabSpec.setIndicator(view);
            mTabHost.addTab(mTabSpec, tab.getFragment(), null);
        }

    }

    private View getBundleView(Tab tab) {
        View view = mInflater.inflate(R.layout.tab_indicator, null);
        ImageView imageView = view.findViewById(R.id.icon_tab);
        TextView textView = view.findViewById(R.id.txt_indicator);
        imageView.setBackgroundResource(tab.getIcon());
        textView.setText(tab.getText());
        return view;
    }
}

public class Tab {
    public int icon; // specify the icon of tab
    public int text; // specify the text of tab
    public Class fragment; // set class

    public Tab(int icon, int text, Class fragment) {
        this.icon = icon;
        this.text = text;
        this.fragment = fragment;
    }

    public int getIcon() {
        return icon;
    }

    public void setIcon(int icon) {
        this.icon = icon;
    }

    public int getText() {
        return text;
    }

    public void setText(int text) {
        this.text = text;
    }

    public Class getFragment() {
        return fragment;
    }

    public void setFragment(Class fragment) {
        this.fragment = fragment;
    }
}

public class MyFragment extends Fragment {
    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.fragment_my, container, false);
        return view;
    }
}


```

#### 顶部导航栏的制作

- 