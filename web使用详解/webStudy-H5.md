###classList新增方法<br>
```js
<div id="box" class="a b"></div>
    <input type="button" value="添加">
    <input type="button" value="删除">
    <input type="button" value="获取">
    <input type="button" value="toggle">
    <input type="button" value="contains">
    <script>
        const box = document.querySelector('#box');
        const aButton = document.querySelectorAll('input');

        aButton.forEach((item , index)=> {
            item.onclick = function () {
                switch (index) {
                    case 0 :
                        box.classList.add('abc' , 'xyz');//添加多个类名
                        break;
                    case 1:
                        box.classList.remove('abc');//移除
                        break;
                    case 2 :
                        console.log(box.classList.length);//获取类名的个数
                        break;
                    case 3 :
                        box.classList.toggle('a');//有删除a,无添加a
                        break;
                    case 4 :
                        let onOff = box.classList.contains('xyz');//判断是否有类名
                        onOff?box.classList.remove('xyz'):box.classList.add('abc','xyz');
                        break;
                }
            }
        })
    </script>
```