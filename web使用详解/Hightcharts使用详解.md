#####引用:
```js
	var chart = Highcharts.chart('container' , {
		chart:{
			//图标参数				
		},
		title:{
			text:'标题'
		},
		annotations:[{ //包含注释
			labelOptions:{
				//规定标签的样式
			}
		}]
	})
```
###highcharts各种方法
```js
chart.events.addSeries：添加数列到图表中。

chart.events.click：整个图表的绘图区上所发生的点击事件。

chart.events.load：图表加载事件。

chart.events.redraw：图表重画事件，当点击图注显示和隐藏绘图时可以触发。

chart.events.selection：当图表曲线可选择放大时，当选择图表操作时，可以触发该事件。

chart.height：所绘制图表的高度值。

chart.inverted：图表中的x，y轴对换。

chart.polar：是否为极性图表。

chart.reflow：当窗口大小改变时，图表宽度自适应窗口大小改变。

chart.renderTo：图表加载的位置，是页面上的一个DOM对象。

chart.showAxes：在空白图表中，是否显示坐标轴。

chart.type：图表的类型，默认为line，还有bar/column/pie……

chart.width：图表绘图区的宽度，默认为自适应。

chart.zoomType：图表中数据报表的放大类型，可以以X轴放大，或是以Y轴放大，还可以以XY轴同时放大。

colors：图表中多数列时，各数列之间的颜色。是一个数组，一般不动。

credits.enabled：是否允许显示版权信息。

credits.href：版权所有的链接。

credits.text：版权信息显示文字。

exporting.buttons.exportButton.enabled：是否允许显示导出按钮。

exporting.buttons.exportButton.menuItems：导出按钮的菜单选项。

exporting.buttons.exportButton.onclick：导出按钮被点击的事件，不是内部的菜单。

exporting.buttons.printButton.enabled：是否允许打印按钮。

exporting.buttons.printButton.onclick：打印按钮的点击事件。

exporting.enabled：打印和导出按钮是否被允许。

exporting.filename：被导出文件的文件名。

exporting.type：默认导出图片的文件格式。

exporting.url：SVG图表转换并导出的接口处理地址。

exporing.width：默认导出图片的宽度。

labels：标签，可以加载到图表的任何位置，里面有items，style。

lang：语言参数配置，与导出按钮菜单有关的配置，时间名称的配置等。

legend.enabled：是否允许图注。

navigation.buttonOptions.enabled：图表中所有导航中的按钮是否可被点击。

plotOptions.area.allowPointSelect：是否允许数据点的点击。

plotOptions.area.color：绘图的颜色。

plotOptions.area.dataLabels.enabled：是否允许数据标签。

plotOptions.area.enableMouseTracking：是否允许数据图表中，数据点的鼠标跟踪气泡显示。

plotOptions.area.events.checkboxClick：数据图表中图注中复选框的点击事件。

plotOptions.area.events.click：数据图表中，数据点的点击事件。

plotOptions.area.events.hide：数据图表中，某一数据序列隐藏时的事件。

plotOptions.area.events.show：数据图表中，某一数据序列显示时的事件。

plotOptions.area.events.legendItemClick：数据图表中，图注中的项目被点击时的事件，直接赋值false，则不可点击。

plotOptions.area.events.mouseOut：数据点的鼠标移出事件。

plotOptions.area.events.mouseOver：数据点的鼠标经过事件。

plotOptions.area.marker.enabled：图表中绘图中是否显示点的标记符。

plotOptions.area.marker.states.hover.enabled：是否允许标记符的鼠标经过状态。

plotOptions.area.marker.states.select.enabled：是否允许标记符的选择状态。

plotOptions.area.point.events.click：图表中每一个单独的点点击事件。

plotOptions.area.point.events.mouseOut

plotOptions.area.point.events..mouseOver

plotOptions.area.point.events.remove：删除图表中的点时的事件。

plotOptions.area.point.events.select：图表中点选择事件。

plotOptions.area.point.events.unselect：图表中点取消选择时的事件。

plotOptions.area.point.events.update：图表中数据发生更新时的事件。

plotOptions.area.visible：加载时，数据序列默认是显示还是隐藏。

plotOptions.area.zIndex：在多序列的情况下，调整每一个序列的层叠顺序。

以上的point.events同样还适用于其他面积类图表（arearange、areaspline、areasplinerange），其他的柱状图（bar、column）及所有图表。

plotOptions.area.showInLegend：是否在图注中显示。

plotOptions.area.stacking：是以值堆叠，还是以百分比堆叠。

plotOptions.area.states.hover.enabled：鼠标放上的状态是否允许。

plotOptions.area.stickyTracking：鼠标粘性跟踪数据点。

plotOptions.arearange，plotOptions.areaspline，plotOptions.areasplinerange类同于plotOptions.area

plotOptions.bar.groupPadding：对于柱状图分组，每个分组之间的间隔。

plotOptions.bar.grouping：是否对数据进行分组。

plotOptions.bar.minPointLength:：定义当point值为零时，点的最小长度为多少

plotOptions.bar.showInLegend：是否在图注中显示。

plotOptions.bar.stacking：是以值堆叠，还是以百分比堆叠（normal/percent）。

plotOptions.column，plotOptions.columnrange类同于plotOptions.bar

plotOptions.line的相关配置类似于plotOptions.area配置。

plotOptions.pie.ignoreHiddenPoint：在饼状图中，某一个序列经图注点击隐藏后，整个饼状图是重新以100%分配，还是只在原图基础上隐藏，呈现一个缺口。

plotOptions.pie.innerSize：绘制饼状图时，饼状图的圆心预留多大的空白。

plotOptions.pie.slicedOffset：与allowPointSelect结合使用，当点被点击时，对应的扇区剥离，这个参数即配置离开的距离。

plotOptions.pie的其他常用配置参数类同于plotOptions.area,plotOptions.scatter，plotOptions.series，plotOptions.spline的相关配置类似于plotOptions.area配置。

series：是一个数组。

series.data.color：某一个数据的颜色。

series.data.dataLabels：序列中某一个数据的数据标签。

series.data.events类同于plotOptions.area.point.events的相关配置。

series.data.marker类同于plotOptions.area.marker的相关配置。

series.data.name：配置数据点的名称。

series.data.sliced：配置在饼图中，扇区的分离距离大小。

series.data.x：点的x值。

series.data.y：点的y值。

series.name：数据序列的名称。

series.stack：堆叠的分组索引。

series.type：数据序列的展示类型。

series.xAxis，series.yAxis：当使用多坐标轴时，指定某个数列对应哪个坐标轴。

subtitle：配置图表的子标题。

title：配置图表的标题。

tooltip：配置图表中数据的气泡提示。

tooltip.valueDecimals：允许的小数点位数。

tooltip.percentageDecimals：允许百分比的小数点后位数。

xAxis，yAxis配置设置坐标轴

allowDecimals：坐标轴上是否允许小数。

categories：是一个数组，坐标轴的分类。

plotLines：绘制主线。

tickColor：刻度颜色。

tickInterval：刻度的步进值。

labels.rotation：刻度标签旋转度数
```
