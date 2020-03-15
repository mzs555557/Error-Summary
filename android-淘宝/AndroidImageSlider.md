###  AndroidImageSlider的使用
- `https://github.com/daimajia/AndroidImageSlider/wiki/Slider-child-view-animation`
- 布局
```xml
<com.daimajia.slider.library.SliderLayout
        android:id="@+id/slider"
        android:layout_width="match_parent"
        android:layout_height="200dp"
/>
```
- 引用
```java
SliderLayout sliderShow = findViewById(R.id.slider);
```
- 使用
```java
TextSliderView textSliderView = new TextSliderView(this);
textSliderView
	.description("Game of Thrones")
	.image("http://images.boomsbeat.com/data/images/full/19640/game-of-thrones-season-4-jpg.jpg");
	
sliderShow.addSlider(textSliderView);
```

- ##### picasso的版本问题需要注意!!

