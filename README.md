## 目录

*   [依赖列表](https://github.com/panteng/wechat-h5-boilerplate#%E4%BE%9D%E8%B5%96%E5%88%97%E8%A1%A8)
*   [项目结构](https://github.com/panteng/wechat-h5-boilerplate#%E9%A1%B9%E7%9B%AE%E7%BB%93%E6%9E%84)
*   [开发流程](https://github.com/panteng/wechat-h5-boilerplate#%E5%BC%80%E5%8F%91%E6%B5%81%E7%A8%8B)
*   [发布流程](https://github.com/panteng/wechat-h5-boilerplate#%E5%8F%91%E5%B8%83%E6%B5%81%E7%A8%8B)
*   [开发指南](https://github.com/panteng/wechat-h5-boilerplate#%E5%BC%80%E5%8F%91%E6%8C%87%E5%8D%97)
*   [待办事项](https://github.com/panteng/wechat-h5-boilerplate#%E5%BE%85%E5%8A%9E%E4%BA%8B%E9%A1%B9)

## 依赖目录
---
1.  [Swiper](https://github.com/nolimits4web/swiper/) --> 用于实现页面的banner、列表滚动
2.  [jQuery](https://github.com/jquery/jquery) --> 用于操作DOM

## 项目结构
    /WANTSWebView
        /css                      --> 插件得样式库
            /swiper.min.css       --> swiper插件
        /js                       --> 插件得操作库
            /swiper.min.js        --> swiper插
            /jquery-2.1.1.min.js  --> jQuery插件
        /f2c.html                  --> 视图

## 开发流程
**将本项目clone到本地**

    在控制台中运行：
    ```

     git clone git@github.com:wantsdev/WANTSWebView.git
     cd <WANTSWebView>

    ```

> 或者你也可以直接在[Release](https://github.com/panteng/wechat-h5-boilerplate/releases)页面下载WHB的源码压缩包。

## 发布流程

发布时，只需要将文件夹中的文件上传到服务器即可。

## 开发指南

1.  **加载动画**

    H5页面通常包含大量图片和背景音乐，因此一个好看的加载动画是必要的。

    你可以自己写一些CSS3动画，将动画相关的HTML代码插入在app/src/index.html中的`<div class="loading-overlay"></div>`中，并将相关的CSS3 Animation代码整合进app/src/scss中。

    想省事的话，[loading.io](http://loading.io/)这个网站可以帮你生成现成的加载动画（打不开请翻墙）。建议生成SVG格式的动画图像文件，将文件改为为loading.svg并替换/images/下的同名文件即可。

    此外分享一些优秀的CSS3加载动画库：

    *   [Spinkit](http://tobiasahlin.com/spinkit/)
    *   [CSS Loaders](http://projects.lukehaas.me/css-loaders/)
2.  **页面切换效果**

    页面切换暂时只支持Swiper自带的四种：slide，fade, flip和coverflow（cube不支持，因为不符合此场景）。详见[Swiper文档](http://idangero.us/swiper/api)中关于effect的部分。

    WHB尚无法对不同页面指定不同的切换方式，我将在后续版本中考虑加入此功能以及更多更酷的切换方式。

3.  **页面内元素（图片、文字）动画**

    在WHB中为图片和文字添加动画非常简单。

    例如在第一页中有一段文字需要以动画显示，代码如下：

    ```
     <div class="swiper-slide">
         <p class="animated" data-ani-name="slideInRight" data-ani-duration="1s" data-ani-delay="0.3s">I'm a coder!</p>
     </div>
    ```

    只需要在这段文字上添加类名`animated`，并指定`data-ani-name`（动画名称）,`data-ani-duration`（动画执行时间），`data-ani-delay`（动画延迟时间）三个属性即可。

    WHB的动画由Animate.css提供，支持的动画名称可以在[Animate.css官网](https://daneden.github.io/animate.css/)上查看。

4.  **字体图标**

    WHB自带的字体图标文件中只有两个图标，分别是右上角的音乐符号，和屏幕下方的上划提示符号。如果你需要更多图标，建议使用[Icomoon.io](https://icomoon.io/#icon-font)进行定制，选择你需要的图标（也可以自己设计并上传），打包成字体文件即可。

    这里不建议使用Font-Awesome等通用字体包的原因是，Font-Awesome中的图标非常多，所以字体文件会比较大，而其中大部分图标是用不到的。较大的字体文件会拖慢网页在用户设备上的加载速度。

5.  **图像优化**

    WHB中自带对/images下的图片进行有损压缩的功能，但我仍然建议在你将图片扔进/images文件夹前，对图片进行必要的手动优化，例如将图片调整为合适的尺寸，将部分小图片整合成精灵图等。

    分享一些好用的图片优化处理网站：

    *   图片压缩：[TinyPNG](https://tinypng.com/)
    *   精灵图生成器（包括生成图片和CSS代码）：[CSS Sprite Generator](http://spritegen.website-performance.org/)
    *   精灵图CSS代码生成器（自动识别精灵图中的元素并生成CSS代码）：[Sprite Cow](http://www.spritecow.com/)
6.  **背景音乐**

    建议背景音乐的文件格式为mp3，且大小尽量不要超过1MB。可使用[Adobe Audition](http://www.adobe.com/products/audition.html)等专业音频编辑软件对背景音乐进行截取和压缩。

    如非必要，请不要设置背景音乐来打扰用户。

7.  **移动端调试**

    首先，运行`gulp dev`任务，在控制台的输出信息中找到下面这段：

    ```
     [BS] Access URLs:
      ----------------------------------------
            Local: http://localhost:3000
         External: http://自己的IP:3000
      ----------------------------------------
               UI: http://localhost:3001
      UI External: http://自己的IP:3001
      ----------------------------------------

    ```

    然后，确保你的移动设备（手机、平板等）和电脑处于同一局域网内（最简单的方式就是让电脑、手机和平板连接同一个WIFI；或者电脑用网线连接路由器，手机和平板连接同是这个路由器发出的WIFI）。

    最后，在你的移动设备上打开浏览器，访问上面第三行中External对应的URL（注意你的URL可能跟我上面写的不一样，以你自己的控制台中显示的External URL为准）。

    现在只要你修改app/src下的文件，所有访问这个URL的移动设备和电脑都会自动刷新浏览器页面。你在其中一个设备上进行的操作也会实时同步到其他设备（比如用手指向上划动页面）。

8.  **响应式设计**

    建议使用rem替代px来设置元素的尺寸、边距和字体大小。

    在WHB中，1rem对应的px数值会随着设备屏幕尺寸的不同而变化。

    在屏幕宽度小于400px的设备上，1rem = 16px；

    在屏幕宽度大于400px且小于600px的设备上，1rem = 22px；

    在屏幕宽度大于600px的设备上，1rem = 32px；

    本项目中，3.75rem = 375px;


## 待办事项

1、完善开发文档

2、优化动画效果

3、优化元素定位方式

4、增加更多Slide切换效果

5、实现可视化编辑

6、实现一键发布
