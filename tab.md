# tab 选项卡

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>原生事件选项卡</title>
        <style>
            * {
                margin: 0;
                padding: 0;
            }

            .main {
                width: 500px;
                margin: 100px auto;
                border: 1px solid red;
                display: flex;
            }

            .main-left {
                width: 100px;
                display: flex;
                flex-wrap: wrap;
                border: 1px solid green;
            }

            .left-title {
                width: 100%;
                background-color: #eee;
                color: black;
                padding: 10px 20px;
                box-sizing: border-box;
                margin-bottom: 10px;
                transition: all 0.5s linear;
            }

            .left-title:last-child {
                margin-bottom: 0px;
            }

            .act-title {
                background-color: orange;
                color: #fff;
            }

            .main-right {
                width: 400px;
                text-align: center;
            }

            .right-text {
                font-size: 30px;
                display: none;
                overflow: hidden;
                text-overflow: ellipsis;
                white-space: nowrap;
                margin-top: 100px;
            }

            .act-text {
                display: block;
            }
        </style>
    </head>

    <body>
        <div class="main">
            <div class="main-left">
                <span class="left-title act-title">标题一</span>
                <span class="left-title">标题二</span>
                <span class="left-title">标题三</span>
                <span class="left-title">标题四</span>
                <span class="left-title">标题五</span>
            </div>
            <div class="main-right">
                <p data-set="标题一" class="right-text act-text">
                    标题1111111111111111111111111111
                </p>
                <p data-set="标题二" class="right-text">
                    标题2222222222222222222222222222
                </p>
                <p data-set="标题三" class="right-text">
                    标题3333333333333333333333333333
                </p>
                <p data-set="标题四" class="right-text">
                    标题4444444444444444444444444444
                </p>
                <p data-set="标题五" class="right-text">
                    标题5555555555555555555555555555
                </p>
            </div>
        </div>
        <script>
            // 获取 菜单栏 父类
            var mainLeft = document.querySelector(".main-left");
            // 获取菜单栏子类
            var leftTitle = document.querySelectorAll(".left-title");
            // 获取内容区父类
            var mainRight = document.querySelector(".main-right");
            // 获取内容区子类
            var rightText = document.querySelectorAll(".right-text");
            // 循环菜单栏子类
            for (let i = 0; i < leftTitle.length; i++) {
                //    单击 菜单子选项的时候执行事件
                leftTitle[i].onclick = function() {
                    // 清楚 菜单子选项的 激活样式
                    document
                        .querySelector(".left-title.act-title")
                        .classList.remove("act-title");
                    //    给当前菜单子元素添加 上激活样式
                    this.classList.add("act-title");
                    //    关键 : 怎么把 内容与 菜单栏绑定到一起
                    var index = rightText[i].dataset.set;
                    // 判断当前点击的子菜单内容 与 当前 的  内容区域的 字内容的dataset的值是否一样
                    // 必须要一样
                    if (event.target.innerText == index) {
                        // 切换 内容的 激活样式
                        // 移除
                        document
                            .querySelector(".right-text.act-text")
                            .classList.remove("act-text");
                        // 添加
                        rightText[i].classList.add("act-text");
                    }
                };
            }
        </script>
    </body>
</html>
```

```html
<!-- <!DOCTYPE html>
<html lang='en'>

<head>
    <meta charset='UTF-8'>
    <meta name='keywords' content='关键字描述网站内容'>
    <meta name='viewport' content='width=device-width, initial-scale=1.0'>
    <title>更换标题111</title>
    <link rel='stylesheet' href=''>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .main {
            width: 600px;
            height: 240px;
            border: 1px solid red;
            display: flex;
            justify-content: space-between;
        }

        .main-left {
            width: 180px;
            height: 100%;
            border: 2px solid black;
        }

        .main-right {
            width: 420px;
            height: 100%;
            border: 2px solid orange;
            display: flex;
            flex-wrap: wrap;

        }

        .left-title {
            width: 100%;
            height: 48px;
            background-color: powderblue;
            font-size: 18px;
            color: black;
            display: block;
            border-bottom: 2px solid #ffffff;
            text-align: center;
            line-height: 48px;
            cursor: pointer;
            transition: all .3s linear;
        }

        .left-title:hover {
            background-color: red;
            color: #ffffff;
        }

        .left-title:first {
            border-bottom: none;
        }

        .right-title {
            width: 420px;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
            /* display: none; */
        }

        .act {
            display: block;
        }

        .act-color {
            background-color: red;
            color: #ffffff;
        }
    </style>
</head>

<body>

    <div class="main">
        <div class="main-left">
        </div>
        <div class="main-right">
        </div>
    </div>

    <script>
        const infoList = [
            {
                title: '你好',
                content: [
                    '你好111',
                    '你好1111111',
                    '你好1111111111111',
                    '你好11111111111111111111',
                ]
            },
            {
                title: '明天',
                content: [
                    '明天1111',
                    '明天111111111',
                    '明天111111111111111',
                    '明天11111111111111111111'
                ]
            },
        ]

        var mainLeft = document.querySelector('.main-left')
        var mainRight = document.querySelector('.main-right')

        getTitle(infoList)
        getContent(infoList[0].content)
        function getTitle(ele) {
            var str = ''
            for (var i = 0; i < ele.length; i++) {
                str += `
                    <span data-set="title2" class="left-title">${ele[i].title}</span>
                    `
            }
            mainLeft.innerHTML = str
        }
        
        function getContent(ele) {
            var str = ''
            for (var i = 0; i < ele.length; i++) {
                str += `
                <p class="right-title">${ele[i]}</p>
                    `
            }
            mainRight.innerHTML = str
        }

        mainLeft.onclick = function(e){
            if(e.target.tagName =="SPAN"){
                var index =infoList.findIndex(ele =>ele.title == e.target.innerHTML)
                console.log(index)
                console.log(e.target.innerHTML)
                console.log(e.target.innerText)
                getContent(infoList[index].content)
            }
        }
    </script>
</body>

</html> -->

<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>原生实现选项卡</title>
        <style>
            * {
                margin: 0;
                padding: 0;
            }

            .main {
                width: 600px;
                height: 240px;
                border: 1px solid red;
                display: flex;
                justify-content: space-between;
            }

            .main-left {
                width: 180px;
                height: 100%;
                border: 2px solid black;
            }

            .main-right {
                width: 420px;
                height: 100%;
                border: 2px solid orange;
                display: flex;
                flex-wrap: wrap;
            }

            .left-title {
                width: 100%;
                height: 48px;
                background-color: powderblue;
                font-size: 18px;
                color: black;
                display: block;
                border-bottom: 2px solid #ffffff;
                text-align: center;
                line-height: 48px;
                cursor: pointer;
                transition: all 0.3s linear;
            }

            .left-title:hover {
                background-color: red;
                color: #ffffff;
            }

            .left-title:first {
                border-bottom: none;
            }

            .right-title {
                width: 420px;
                overflow: hidden;
                text-overflow: ellipsis;
                white-space: nowrap;
                display: none;
            }

            .act {
                display: block;
            }

            .act-color {
                background-color: red;
                color: #ffffff;
            }
        </style>
    </head>

    <body>
        <div class="main">
            <div class="main-left">
                <!-- <span class="left-title act-color">标题一</span> -->
            </div>
            <div class="main-right">
                <!-- <p data-set="标题1" class="right-title act">
                标题111111111111111111111111111111111111111111111111111111111111111111111</p> -->
            </div>
        </div>
        <script>
            const list = [
                {
                    title: "标题1",
                    content:
                        "标题111111111111111111111111111111111111111111111111111111111111111111111"
                },
                {
                    title: "标题2",
                    content:
                        "标题222222222222222222222222222222222222222222222222222222222222222222222"
                },
                {
                    title: "标题3",
                    content:
                        "标题333333333333333333333333333333333333333333333333333333333333333333333"
                },
                {
                    title: "标题4",
                    content:
                        "标题444444444444444444444444444444444444444444444444444444444444444444444"
                },
                {
                    title: "标题5",
                    content:
                        "标题555555555555555555555555555555555555555555555555555555555555555555555"
                }
            ];
            // 获取 左边的菜单栏的父类
            var mainLeft = document.querySelector(".main-left");
            // 获取 右边的 内容区的父类
            var mainRight = document.querySelector(".main-right");
            // 执行 数据的插入
            setInfo(list);
            function setInfo(list) {
                // 声明两个字符串 存放 菜单和内容
                var str = ""; // 菜单
                var info = ""; // 内容
                // 循环 渲染 数据
                for (var i = 0; i < list.length; i++) {
                    str += `<span data-set="标题${i + 1}" class="left-title  ${
                        i === 0 ? "act-color" : ""
                    }">${list[i].title}</span>`;
                    info += ` <p data-set="标题${i + 1}" class="right-title ${
                        i === 0 ? "act" : ""
                    }">${list[i].content}</p>`;
                }
                // 把数据 插入 内容区中
                mainLeft.innerHTML = str;
                mainRight.innerHTML = info;
                // console.log(str)
                // console.log(info)
            }
            // 获取 所有的 菜单子项
            var leftTitle = document.querySelectorAll(".left-title");
            // 获取 所有的 内容子项
            var rightTitle = document.querySelectorAll(".right-title");
            // 循环点击事件
            for (let i = 0; i < leftTitle.length; i++) {
                // 点击第一个 菜单子元素的时候 执行的事件
                leftTitle[i].onclick = function() {
                    // 清楚菜单子元素的 激活样式
                    document
                        .querySelector(".left-title.act-color")
                        .classList.remove("act-color");
                    // 给当前的元素添加上
                    this.classList.add("act-color");
                    // 获取 菜单子元素的 dataset值
                    var ctitle = rightTitle[i].dataset.set;
                    // 获取 内容子元素的 dataset 值
                    var ltitle = leftTitle[i].dataset.set;
                    // 清除 内容子元素的 激活样式
                    // document.querySelector('.right-title.act').classList.remove('act')
                    // 点击的时候 判断内容是否一致
                    // if (ctitle == event.target.innerHTML) {
                    // 如果 内容一致
                    if (ctitle == ltitle) {
                        // 清除 内容子元素的 激活样式
                        document
                            .querySelector(".right-title.act")
                            .classList.remove("act");
                        //    ctitle.classList.add('act')
                        // console.log(rightTitle[i].classList.remove('act'))
                        // 就切换 内容的 激活状态
                        rightTitle[i].classList.add("act");
                        // console.log(ctitle)
                    }
                };
            }
        </script>
    </body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>原生事件选项卡</title>
        <style>
            * {
                margin: 0;
                padding: 0;
            }

            .main {
                width: 500px;
                margin: 100px auto;
                border: 1px solid red;
                display: flex;
            }

            .main-left {
                width: 100px;
                display: flex;
                flex-wrap: wrap;
                border: 1px solid green;
            }

            .left-title {
                width: 100%;
                background-color: #eee;
                color: black;
                padding: 10px 20px;
                box-sizing: border-box;
                margin-bottom: 10px;
                transition: all 0.5s linear;
            }

            .left-title:last-child {
                margin-bottom: 0px;
            }

            .act-title {
                background-color: orange;
                color: #fff;
            }

            .main-right {
                width: 400px;
                text-align: center;
            }

            .right-text {
                font-size: 30px;
                display: none;
                overflow: hidden;
                text-overflow: ellipsis;
                white-space: nowrap;
                margin-top: 100px;
            }

            .act-text {
                display: block;
            }
        </style>
    </head>

    <body>
        <div class="main">
            <div class="main-left">
                <span class="left-title act-title">标题一</span>
                <span class="left-title">标题二</span>
                <span class="left-title">标题三</span>
                <span class="left-title">标题四</span>
                <span class="left-title">标题五</span>
            </div>
            <div class="main-right">
                <p data-set="标题一" class="right-text act-text">
                    标题1111111111111111111111111111
                </p>
                <p data-set="标题二" class="right-text">
                    标题2222222222222222222222222222
                </p>
                <p data-set="标题三" class="right-text">
                    标题3333333333333333333333333333
                </p>
                <p data-set="标题四" class="right-text">
                    标题4444444444444444444444444444
                </p>
                <p data-set="标题五" class="right-text">
                    标题5555555555555555555555555555
                </p>
            </div>
        </div>
        <script>
            // 获取 菜单栏 父类
            var mainLeft = document.querySelector(".main-left");
            // 获取菜单栏子类
            var leftTitle = document.querySelectorAll(".left-title");
            // 获取内容区父类
            var mainRight = document.querySelector(".main-right");
            // 获取内容区子类
            var rightText = document.querySelectorAll(".right-text");
            // 循环菜单栏子类
            for (let i = 0; i < leftTitle.length; i++) {
                //    单击 菜单子选项的时候执行事件
                leftTitle[i].onclick = function() {
                    // 清楚 菜单子选项的 激活样式
                    document
                        .querySelector(".left-title.act-title")
                        .classList.remove("act-title");
                    //    给当前菜单子元素添加 上激活样式
                    this.classList.add("act-title");
                    //    关键 : 怎么把 内容与 菜单栏绑定到一起
                    var index = rightText[i].dataset.set;
                    // 判断当前点击的子菜单内容 与 当前 的  内容区域的 字内容的dataset的值是否一样
                    // 必须要一样
                    if (event.target.innerText == index) {
                        // 切换 内容的 激活样式
                        // 移除
                        document
                            .querySelector(".right-text.act-text")
                            .classList.remove("act-text");
                        // 添加
                        rightText[i].classList.add("act-text");
                    }
                };
            }
        </script>
    </body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8" />
        <title>tab切换</title>
        <style type="text/css">
            * {
                padding: 0;
                margin: 0;
                font: normal 15px "微软雅黑";
                color: #000;
            }

            ul {
                list-style-type: none;
                /* padding-left: 5px; */
                margin-bottom: -2px;
            }

            .tab {
                width: 500px;
                margin: 10px auto;
            }

            a {
                text-decoration: none;
            }

            .title li {
                display: inline-block;
                border: 1px solid #999;
                background: #fff;
                text-align: center;
                width: 60px;
                height: 30px;
                margin: 0 1px;
                line-height: 30px;
            }

            .title .active {
                border-bottom: 2px solid #fff;
                background-color: #eee;
            }

            #content {
                margin: 0;
                border: 1px solid #ccc;
                width: 300px;
            }

            #content div {
                display: none;
                padding: 10px 0;
            }

            #content .mod {
                display: block;
            }
        </style>
    </head>

    <body>
        <div class="tab">
            <ul class="title">
                <li class="active"><a href="#">神州</a></li>
                <li><a href="#">小娜</a></li>
                <li><a href="#">神娜</a></li>
                <!--<li><a href="#">家居</a></li>-->
            </ul>
            <div id="content">
                <div class="mod">
                    <ul>
                        <li><a href="#">神州123123</a></li>
                        <li><a href="#">神州123123</a></li>
                        <li><a href="#">神州123123</a></li>
                    </ul>
                </div>
                <div class="mod" style="display: none">
                    <ul>
                        <li><a href="#">小娜456456</a></li>
                        <li><a href="#">小娜456456</a></li>
                        <li><a href="#">小娜456456</a></li>
                    </ul>
                </div>
                <div class="mod" style="display: none">
                    <ul>
                        <li><a href="#">神娜789789</a></li>
                        <li><a href="#">神娜789789</a></li>
                        <li><a href="#">神娜789789</a></li>
                    </ul>
                </div>
            </div>
        </div>
    </body>
</html>
<script src="https://cdn.bootcss.com/jquery/3.4.1/jquery.min.js"></script>
<script type="text/javascript">
    $(function() {
        $(".title li").click(function() {
            $(this)
                .addClass("active")
                .siblings()
                .removeClass("active");
            $("#content .mod")
                .eq($(".title li").index(this))
                .show()
                .siblings("#content .mod")
                .hide();
        });
    });
</script>
```

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>Title</title>
        <style type="text/css">
            * {
                padding: 0;
                margin: 0;
                box-sizing: border-box;
            }

            div {
                width: 70%;
                margin: 20px auto;
            }

            ul {
                list-style: none;
                overflow: hidden;
            }

            #nav {
                width: 400px;
                height: 40px;
                text-align: center;
                line-height: 40px;
                background: #c5c5c5;
            }

            #nav li {
                width: 25%;
                height: 40px;
                float: left;
                border: 1px solid #c5c5c5;
                border-bottom: none;
            }

            #nav li.active {
                background: #fff;
            }

            #content {
                width: 400px;
                height: 300px;
                position: relative;
                border: 1px solid #c5c5c5;
                border-top: none;
            }

            #content li {
                width: 100%;
                height: 100%;
                position: absolute;
                padding: 10px;
                display: none;
            }
        </style>
    </head>

    <body>
        <div>
            <ul id="nav">
                <li class="active">选项一</li>
                <li>选项二</li>
                <li>选项三</li>
                <li>选项四</li>
            </ul>
            <ul id="content">
                <li style="display: block">内容一</li>
                <li>内容二</li>
                <li>内容三</li>
                <li>内容四</li>
            </ul>
        </div>
    </body>
</html>

<script type="text/javascript">
    // 获取  菜单栏 父类
    var nav = document.getElementById("nav");
    // 获取 菜单栏子类
    var navlist = nav.children;
    // 获取 内容区父类
    var con = document.getElementById("content");
    // 获取 内容区子类
    var conlist = con.children;
    // 循环 菜单栏子类
    for (var i = 0; i < navlist.length; i++) {
        // 每次循环都把 当前的 i 保存下来
        navlist[i].index = i;
        // 当前的 i 点击的时候
        navlist[i].onclick = function() {
            // 遍历 内容区的 子类
            for (var m = 0; m < conlist.length; m++) {
                // 切换 菜单类的 激活样式
                navlist[m].className = "";
                // 设置内容区的 显示隐藏
                conlist[m].style.display = "none";
            }
            // 当前的 菜单子类的 激活样式
            this.className = "active";
            // 当前内容 区域的 的样式的显示
            conlist[this.index].style.display = "block";
        };
    }
</script>
```
