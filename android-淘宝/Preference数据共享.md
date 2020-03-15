###  SharedPreferences 轻量级数据存储
- 使用Activity类的getSharedPreferences方法获取SharedPreferences对象
- 使用SharedPreferences接口的edit方法获取SharedPreferences.Editor对象
- 使用SharedPreferences接口的put{object}方法保存key-value对
- 通过SharedPreferences.Editor的commit方法保存key-value对
### 示例
```java
	/**
     * 保存用户信息
     */
    private void saveUserInfo(){
        SharedPreferences userInfo = getSharedPreferences(PREFS_NAME, MODE_PRIVATE);
        SharedPreferences.Editor editor = userInfo.edit();//获取Editor
        //得到Editor后，写入需要保存的数据
        editor.putString("username", "一只猫的涵养");
        editor.putInt("age", 20);
        editor.commit();//提交修改
        Log.i(TAG, "保存用户信息成功");
    }
    /**
     * 读取用户信息
     */
    private void getUserInfo(){
        SharedPreferences userInfo = getSharedPreferences(PREFS_NAME, MODE_PRIVATE);
        String username = userInfo.getString("username", null);//读取username
        int age = userInfo.getInt("age", 0);//读取age
        Log.i(TAG, "读取用户信息");
        Log.i(TAG, "username:" + username + "， age:" + age);
    }
    /**
     * 移除年龄信数据
     */
    private void removeUserInfo(){
        SharedPreferences userInfo = getSharedPreferences(PREFS_NAME, MODE_PRIVATE);
        SharedPreferences.Editor editor = userInfo.edit();//获取Editor
        editor.remove("age");
        editor.commit();
        Log.i(TAG, "移除年龄数据");
    }

    /**
     * 清空数据
     */
    private void clearUserInfo(){
        SharedPreferences userInfo = getSharedPreferences(PREFS_NAME, MODE_PRIVATE);
        SharedPreferences.Editor editor = userInfo.edit();//获取Editor
        editor.clear();
        editor.commit();
        Log.i(TAG, "清空数据");
    }
```
-  SharedPreferences的监听事件

```java
 SharedPreferences.OnSharedPreferenceChangeListener changeListener = new OnSharedPreferenceChangeListener() {
            @Override
            public void onSharedPreferenceChanged(SharedPreferences preferences, String key) {
                //preferences被 编辑的SharedPreferences实例
                //该SharedPreferences中被编辑的条目所对应的key
            }
        };
        //userInfo注册监听事件
        userInfo.registerOnSharedPreferenceChangeListener(changeListener);
        //userInfo注销监听事件
        userInfo.unregisterOnSharedPreferenceChangeListener(changeListener);
```

- 对Proference的封装

```java
  public class CartProvider {
  
    private final String CART_JSON = "cart_json";
  
    Context mContext;
  
    SparseArray<ShowCart> cartSparseArray = null;
  
    public CartProvider(Context context) {
  
        this.mContext = context;
        cartSparseArray = new SparseArray<>(50);
        listToSparse();
    }
    public void update(ShowCart cart) {
        cartSparseArray.put(cart.getId().intValue(),cart);
        commit();
    }
    
    public void put(ShowCart cart) {
        ShowCart temp = cartSparseArray.get(cart.getId().intValue());
    
        if (temp != null) {
            temp.setCount(temp.getCount()+1);
        } else {
            temp = cart;
            temp.setCount(1);
        }
    
        cartSparseArray.put(temp.getId().intValue(), temp);
        commit();
    }
    
    public void delete(ShowCart showCart) {
        cartSparseArray.delete(showCart.getId().intValue());
        commit();
    }
    
    public void commit() {
        List<ShowCart> carts = sparseToList();
    
        PreferencesUtils.putString(mContext,CART_JSON, JSONUtil.toJSON(carts));
    
    }
    
    public List<ShowCart> getAll() {
        return getDataFromLocal();
    }
    
    private List<ShowCart> sparseToList() {
    
        int size = cartSparseArray.size();
    
        List<ShowCart> list = new ArrayList<>(size);
        for (int i = 0; i< size; i++) {
            list.add(cartSparseArray.valueAt(i));
        }
        return list;
    
    }
    
    private void listToSparse() {
        List<ShowCart> list = getDataFromLocal();
    
        if (list != null && list.size() > 0) {
            for (ShowCart cart: list ) {
                cartSparseArray.put(cart.getId().intValue(), cart);
            }
        }
    }
  
    private List<ShowCart> getDataFromLocal() {
        String json = PreferencesUtils.getString(mContext, CART_JSON);
    
        List<ShowCart> carts = null;
    
        if (json != null) {
            carts = JSONUtil.fromJson(json, new TypeToken<List<ShowCart>>(){}.getType());
        }
    
        return carts;
    }
  }
```
