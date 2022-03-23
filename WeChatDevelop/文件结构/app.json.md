# app.json
app.json文件是小程序的全局配置文件，主要**包含了小程序所有页面的路径地址、导航栏样式等**。  

文件中仅有一个对象，包含若干属性和值的键值对  

-------------

## pages 属性
``` Json
{
    "pages": [
        "pages/index/index",
        "pages/about/about",
        "pages/study/study"
    ]
}
```

**pages 属性用于保存小程序所有用到的页面路径**  

如果有多个，则默认第一个为初始页面，即主页  

--------------

## window 属性
``` Json
{
    "window": {
        "navigationBarTitleText": "HelloWorld",
        "navigationBarTextStyle": "black",
        "navigationBarBackgroundColor": "#E0E0F8"
    }
}
```

**window 属性定义了窗口的样式，主要是针对小程序上方的头部导航栏**  

**window属性的值是也是一个对象**，其中包括了小程序页面顶端导航栏的背景颜色、标题文字内容、以及文字颜色等属性内容。  

常用的属性有：  
* **navigationBarBackgroundColor**：定义了标题栏的背景颜色  
* **navigationBarTextStyle**：定义了标题栏的显示文字的颜色，只能是 white(缺省) 或者 black   
* **navigationBarTitleText**：定义了标题栏显示文字的内容  
* **enablePullDownRefresh**：值为布尔值，定义了是否开启下拉刷新功能

------------

## tabBar 属性
``` Json
{
    "tabBar": {
        "list": [
            {}
        ],
        "color": "#1C1C1C",
        "backgroundColor": "#FAFAFA",
        "selectedColor": "#1C1C1C"
    }
}
```

**tabBar 属性定义了小程序的 tab 栏表现形式，其值是一个对象**  

如果小程序是一个多 tab 应用（客户端窗口的底部有 tab 栏可以切换页面），可以通过 tabBar  
配置项指定 tab 栏的表现，以及 tab 切换时显示的对应页面  

**tab 最少2个，最多5个**  

常用的属性有：  
* **list**：必填，按顺序定义了各 tab 页的初始页面路径  
  每一个 tab 页面用一个对象表示，对象中需含有信息：  
  * **text** 必填，tab按钮上的文字  
  * **pagePath** 必填，tab页面的路径  
  * **iconPath** tab 按钮上要显示的图标路径  
  * **selectedIconPath** 选中时的图标路径  
* **backgroundColor**：必填，tab 的背景色  
* **color**：必填，tab 文字的颜色  
* **selectedColor**：必填，选中时 tab 文字的颜色  
* **position**：tabBar 的位置，可以是 top 或 bottom  