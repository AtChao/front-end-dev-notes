# 前端优化指南
## 1 工作效率
### 1.1 时间管理

+ 正确的时间点做正确的事，比如早上比较精神，可选择比较难的项目展开，可容易达到高效率
+ 专注一件事情，尽量不要被琐碎或其他事情影响，而且不要频繁去看计划表，最好是做完一件事情再去看，否则容易焦虑导致无法专心

### 1.2 利用工具
利用工具的好处在于：

+ 减少复杂性工作
+ 减少繁琐工作流程，一键化

#### 1.2.1 编辑器
目前比较不错的有：

+ sublime text
+ visual studio code
+ webstrom等

#### 1.2.2 浏览器开发者工具
作为前端人员，首选浏览器当然是Chrome。推荐阅读[Chrome开发者工具不完全指南](http://web.jobbole.com/82558/ "Chrome开发者工具不完全指南")。
#### 1.2.3 其他常用工具
+ 切图工具：photoshop cc 切图之智能切图、cutter man
+ 量色、测距工具：FastStone Capture、马克鳗-设计稿标注
+ 图片压缩：tinning、智图
+ 生成雪碧图：spritebox、css sprite generator、cssgaga
+ 调试工具：Fiddler、weinre、微信调试工具

#### 1.2.4 前端工程化
_凡是重复的，必须使用工具自动完成_
前端工程化工具能帮我们完成自动生成雪碧图、css压缩、图片压缩等等，一般分为5个步骤：

1. 初始，生成基础目录结构和样式库
2. 开发，实时预览、预编译
3. 构建，预编译、合并、压缩
4. 发布，将构建后静态文件发布上线
5. 打包，资源路径转换，源码大包
推荐：fis，解决前端开发中自动化工具、性能优化、模块化框架、开发规范、代码部署、开发流程等问题。

### 1.3 阅历和经验
我所理解的程序员兼并聪明以及“懒惰”精神，推崇懒惰式开发，即把问题理解清楚，确保将要写的代码能真正的解决问题，这将会避免之后写出大量无用的代码，正所谓“懒”出效率。

我们的阅历和经验可以大大提高开发效率，思考代码的时间增加从而选出最优方案，因此写代码速度更快以及代码长度更短，对问题的透彻理解使调试代码的速度也更快。

根据阅历和经验，或借助其他人的，我们进行整理从而形成自己或团队的规范，这可大大提高我们的写码速度。

### 1.4 使用新技术
使用新技术如何提高我们的工作效率。一贯我们都使用我们熟悉的技术去开发一个技术处理方案，毕竟学习新技术的时间成本还是存在的。但是还是不能忽略一些新技术的存在，一般新技术包含了一些很棒的新特性，可以更加方便的实现很多复杂的操作，提高开发人员的效率，比如ES6。用你的慧眼去积累新技术，会派上用场的。

## 2 性能
 对于性能优化，首先需要确定页面的性能指标，可量化的目标以及可持续跟踪的优化数据是性能优化工作得以持续进行的保障，同时也是源动力。比如：

+ 首屏加载时长
+ DOM加载时长
+ 页面白屏时长

一般通过三个方式来检验页面性能：

+ 通过浏览器开发者工具或浏览器插件、Fiddler、Charles等查看页面加载情况。原理是通过追踪HTTP请求与响应时间，以图形的方式列出所有资源的下载情况。缺点是人为操作，难以实现批量测试与统计。
+ 在页面中引入额外的代码钩子来记录时间等相关数据。缺点是加重了开发者与测试人员的负担，还有可能因为测试代码自身的潜在问题影响页面的性能。如果还一点的话，会接入一个性能数据收集系统，采取并分析数据。
+ 使用第三发的工具如_Page Speed_、_YSlow_和_WebPagetest_，能够选择在不同浏览器和不同地域进行测试，并且给出各个方面的测评以及提供一些优化建议。但某些服务需要排队等待，并且难以实现批量测试与统计

可喜可贺，W3C推出了一套_性能API标准_,目的是简化开发者对网址性能进行精确分析与控制的过程，最终实现性能的提高。

```javascript
	var timing = window.performance.timing
	timing.domLoading //浏览器开始解析HTML文档第一批接收的字节
	timing.domInteractive //浏览器完成解析并且所有 HTML 和 DOM 构建完毕
	timing.domContentLoadedEventStart //DOM 解析完成后，网页内资源加载开始的时间
	timing.domContentLoadedEventEnd // DOM 解析完成后，网页内资源加载完成的时间（如 JS 脚本加载执行完毕）
	timing.domComplete //网页上所有资源（图片等）下载完成,且准备就绪的时间
```
__持续追踪性能数据，要选择合适的页面性能测量工具或API，一旦选定后，不再更换，以保证历史数据的可参照性。__

还要形成一种意识，达成性能联盟小组，对于重要的业务或页面，一定要从性能的角度考虑问题，有理有据地拒绝有损于前端性能的业务需求或改动。

[雅虎军规](http://www.cnblogs.com/lei2007/archive/2013/08/16/3262897.html "雅虎军规")

## 2.1 服务端
### 2.1.1 避免404
1. 更改404错误响应页面可以改进用户体验，但是同样也会浪费服务器资源
2. 指向外部JS连接出现问题并返回404代码
	+ 这种加载会破坏并行加载
	+ 其次浏览器会试图在返回的404响应内容中找到可能有用的部分当成JS代码执行

### 2.1.2 使用内容分发网络（Content Delivery Network，CDN）
通过在现有的Internet中增加一层新的网络架构，将网址的内容发布到最接近用户的cache服务器内，通过DNS负载均衡的技术，判断用户来源就近访问cache服务器取得所需的内容。深圳用户访问遥远的美国服务器当然不理想。把静态内容分布到CDN可以减少用户响应时间20%或更多。

### 2.1.3 把静态资源缓存，移动端离线缓存
如果可以减少服务器端的负担，在应用离线时可使用资源或加载资源更快。岂不乐哉？缓存利用可包括：添加Expires头、配置ETag、使用Ajax可缓存等。其实，恰当的缓存设置可以大大的减少HTTP请求，也可以节省带宽。

1. 配置ETag

	即If-None-Match，上次ETag的内容。浏览器会发出请求询问服务端，资源是否过期；服务端发现没有过期，直接返回一个状态码为304、正文为空的响应，告知浏览器使用本地缓存；如果资源有更新，服务端返回状态码200、ETag和正文。这个过程被称之为HTTP的协商缓存，通常也叫做弱缓存。
2. 添加Expires头

	服务端通过响应头告诉浏览器，在什么时间之前（Expires）或在多长时间之内（Cache-Control:Max-age=xxx），不要再请求服务器了。这个机制我们通常称之为HTTP的强缓存。一般会对CSS、JS、图片等资源使用强缓存，而入口文件 （HTML）一般使用协商缓存或不缓存。
3. AppCache

	主要利用manifest文本文件，告知浏览器被缓存的内容以及不缓存的内容。manifest文件可分为三个部分：
	+ CACHE MANIFEST － 在此标题下列出的文件将在首次下载后进行缓存，等价于CACHE
	+ NETWORK － 在此标题下列出的文件需要于服务器的连接，且不会被缓存
	+ FALLBACK － 在此标题下列出的文件规定当页面无法访问时的回退页面
	使用AppCache方案的步骤：
    
	+ 整理出需要缓存的静态文件列表，如jquery.js和gb.css
	+ 配置服务器支持
	+ 确定内容更新机制和浏览器兼容方案
	
## 2.2 网络
### 2.2.1 减少请求数
可以通过以下方式减少请求数：

+ 小图片合并雪碧图；
+ JS、CSS文件选择性合并；
+ 避免重复的资源请求。

减少请求数对速度优化来说最重要最有效的，特别时网络差的用户。一个完整的请求需要经过域名解析以及DNS寻址、与服务器建立连接、发送数据、等待服务器响应、接收数据的过程；每个请求都需要携带数据，因此每个请求都需要占用带宽；浏览器进行并发请求数是有上限的。请求多了的情况，明显增加了网页的响应时间。一个页面由多个模块拼接而成，几个模块中请求了同样的资源时，就会导致资源的重复请求。

### 2.2.2 减少文件大小（减少请求带宽）
1. 压缩CSS、JS、图片
2. 尽可能控制DOM节点数
3. 精简css、js，移除注释、空格、重复css和脚本
4. 开启Gzip，Gzip的思想就是把文件先在服务器端进行压缩，且压缩率达到85%，然后再传输，传输完毕后浏览器会重新对压缩过的内容进行解压缩，并执行。好处在于Gzip的支持已经很好，并且爬虫可识别，压缩率达到66％－85％明显减少了文件传输的大小。另外，Gzip对pdf文件的压缩效果不大，而且会浪费CPU。Gzip工作流程：
	+ 客户端请求Accept-Encoding中声明可以支持Gzip
	+ 服务器将请求文档压缩，并在Content-Encoding中声明该回复为Gzip格式
	+ 客户端收到之后按照Gzip解压缩
	
### 2.2.3 通过Keep-alive机制减少TCP连接
### 2.2.4 减少重定向（HTTP 301 和40X / 50X )
### 2.2.5 AJAX

1. 缓存AJAX

  异步不等于即时。
  
2. 请求使用GET

  当使用XMLHttpRequest时，而URL长度不到2k，可以使用GET请求数据，GET相对POST更快
  
  + POST类型请求要发送两个TCP数据包

    先发送文件头，再发送数据
    
  + GET类型请求只需要请求一个TCP数据包

    取决于COOKIE数量
    
### 2.2.6 合理使用静态资源域名
__域名的要求是短小且独立。__

短小可以减少头部开销，因为域名越短小请求头起始行的URL就越短。之所以要求独立，因为独立域名不会共享主域的COOKIE，可以有效减少请求头大小，这个策略一般称之为Cookie-Free Domain;另外一个原因是浏览器对相同域名的并发连接数限制，一般允许同域名并发6～8个连接，域名不是越多越好，每个域名的第一个连接都要经历DNS查询（DNS Lookup），导致会消耗一定的时间，控制域名使用在2-4个之间。另外注意：同一静态资源在不同页面被散列到不同子域下，会导致无法利用HTTP缓存。
### 2.2.7 使用HTTP 2
HTTP 2相对于 HTTP 1.1的更新大部分集中于：

+ 多路复用：多路复用很好地解决了如何让重要资源尽快加载这个问题。同域名下或者不同域但是同时满足同一个IP以及使用同一个证书的这两个条件中的所有通信都在当个连接上完成，此连接上同时打开任意数量的双向数据流（HTTP 1.1有连接数限制）。使用多域名加上相同的IP和证书部署web服务有特殊的意义：让支持HTTP／2的终端只建立一个连接，用上HTTP／2协议带来的各种好处，而只支持HTTP／1.1的终端则会建立多个连接，达到同时更多并发请求的目的。
+ HEAD压缩：HTTP/2请求和响应数据分割为更小的帧，并对他们采用二进制编码（Binary Framing）。在HTTP/1中，HTTP请求和响应都是由_ 状态行、请求／响应头部、消息主题 _三部分组成，状态行和头部却没有经过任何压缩，直接以纯文本传输。在HTTP／2中，每个数据流都以消息的形式发送，而消息又由一个活多个帧组成。多个帧之间可以乱序发送，因为根据帧首部的流标示可以重新组装。
+ 请求优先级：服务器可以根据流的优先级，控制资源分配（CPU、内存、带宽），而在响应数据准备好之后，优先将最高优先级的帧发送给客户端。
+ 服务器推送：启动Server Push，意味着服务端可以在发送页面HTML时主动推送其它资源，有自己独立的URL，可以被浏览器缓存；如果服务器推送的资源可以被浏览器缓存过，浏览器可以通过发送RST\_STREAM帧来拒收。

## 2.3 客户端
### 2.3.1 资源引入
1. 使用外链CSS和JS，CSS放头部，JS放尾部，防止阻塞以减少对并发下载的影响，尽早刷新文档的输出。
2. 尝试使用defer方式加载js脚本
3. 加快js载入速度的工具

  Lab.js：借助LAB.js（装入和阻止js），你就可以并行装入js文件，加快总的装入过程。此外，你还可以为需要装入的脚本设置某个顺序，那样就能确保关系的完整性。
 
4. 异步装入跟踪代码
  
  脚本加载与解析会阻塞HTML渲染，可以通过异步加载方法来避免渲染阻塞，异步加载的方法很多，比较通用的方法：
  
  ```javascript
  var _gaq = _gaq||[];
  _gaq.push(['_setAccount','UA-xxxx-xx']);
  _gaq.push(['_trackPageview']);
  (function(){
    var ga = document.createElement('script');
    ga.type = 'text/javascript';
    ga.async = true;
    ga.src = ('https:'==document.location.protocol?'https://ssl':'http://www')+'.google-analytics.com/ga.js';
    var s = document.getElementByTagName('script')[0];
    s.parentNode.insertBefore(ga,s);
  })()
  ```
  或者
  
  ```javascript
  function loadjs(script_filename){
    var script = document.createElement('script');
    script.setAttribute('type','text/javascript');
    script.setAttribute('src',script_filename);
    script.setAttribute('id',script-id);
    
    scriptElement = document.getElementById('script-id');
    if(scriptElement){
      document.getElementByTagName('head')[0].removeChild(scriptElement);
    }
    document.getElementByTagName('head')[0].appendChild(script);
  }
  var script = 'scripts/alert.js';
  loadjs(script);
  ```
  
5. js打包成png文件

  将js、css数据打包成png文件。之后执行拆包，只要使用画布API的getImageData。可以在不缩小数据的情况下，多压缩35%左右。而且是无损压缩，对比较庞大的脚本来说，在图片指向画布、读取像素的过程中，你会觉得有“一段”装入时间。

### 2.3.2 COOKIE 优化

1. 减少COOKIE的大小
2. 使用无COOKIE的域

    比如图片、CSS等静态文件放在静态资源服务器上并配置独立域名，客户端请求静态文件时，减少COOKIE反复传输对主域名的影响

### 2.3.3 HTML 代码优化
1. 插入HTML，js中使用 document.write生成页面内容会效率较低，可以找一个容器元素，比如只定义个DIV，并使用innerHTML来将HTML代码插入页面
2. 避免空格图片src;
2. 协议自适应，减少HTML文件大小，将https://和http://都替换成//；
3. 重构HTML，把重要内容优先级提高；
4. 利用预加载优化资源；
5. Post-load(次要加载）不是必要的资源；
6. 合理架构，使DOM结构尽量简单；
7. 利用 localStorage合理缓存资源；
8. 新特性： will-change , 把即将发生的改变预想告诉浏览器；
9. 新特性：Beacon，不阻塞队列的异步数据发送
10. 尽量多地缓存文件
11. 使用HTML5 Web Workers来允许多线程工作
12. 为不同的Viewports设置不同大小的Content
13. 使用响应式图片
14. 未来的缓存离线机制：Service Workers
15. 未来资源优化 Resource Hints（reconnect,preload,pretender）
16. 使用Server-sent Events
17. 设置一个Meta Viewport

### 2.3.4 CSS代码优化
1. 建议使用类选择器，访问比较快；
2. 不建议使用很长的base64；
3. 避免CSS表达式；
4. 避免使用Filters。

### 2.3.5 JS代码优化
1. 代码优化原则

  + 第一原则就是只需要为IE6（未打补丁的JScript 5.6或者更早版本）做优化
  + 第二原则就是js优化总是出现在大规模循环的地方
  + 尽量避免过多的引用层级和不必要的多次方法调用
  + 尽量使用语言本身的构造和内建函数
  
2. 避免使用eval
  + 会导致代码看起来更脏
  + 需要消耗大量时间
  + 会逃过大量压缩工具的压缩
3. 避免使用with

	__with会增加语句意外的数据的访问代价。__
    
	with语句将一个新的可变对象推入作用域链的头部，函数的所有局部变量现在处于第二个作用域链对象中，从而使局部变量的访问代价提高。
    
    ```javascript
	var person = 
      name:”nicholas”,
      age:30
	}
    function displayInfo(){
      var count = 5;
      with(person){
        alert(name+'is'+age);
        alert('count is '+count);
      }
    }
	```

4. 传递方法取代方法字符串
  
  一些方法例如setTimeout/setInterval,接受字符串或者方法实例作参数。直接传递方法对象作为参数来避免字符串的二次解析
  
  + 传递方法：`setTimeout(test,1)`
  + 传递方法字符串：`setTimeout('test()',1)`
   
5. 使用原始操作代替方法调用

   方法调用一般封装了原始操作，在性能要求高的逻辑中，可以使用原始操作来代替方法调用提高性能
   
   + 原始方法：`var min = a<b?a:b;`
   + 方法实例：`var min = Math.min(a,b);`
   
6. 定时器

  如果针对的是不断运行的代码，不应该使用`setTimeout`,而应该是`setInterval`。`setTimeout`每次都要重新设置一个定时器。

7. 避免双重解释
  
  当js代码准备解析js代码时，就会存在双重解析惩罚，双重解析一般在使用`eval`函数、`new Function`构造函数和`setTimeout`传入一个字符串时等情况下会遇到。如：
  
  ```javascript
  eval("alert('hello world')");
  var sayHi = new Function("alert('hello world');");
  setTimeout("alert('hello world');",100);
  ```
  上述`alert`语句包含在字符串中，即在js代码运行的同时必须新启动一个解析器来解析新的代码，而实例化一个新的解析器有很大的性能损耗。例如：
  
  ```javascript
  var sum,num1=1,num2=2;
  /**效率低**/
  for(var i=0;i<10000;i++){
    var fun = new Function("sum+=num1;num1+=num2;num2++;");
    fun();
  }
  /**效率高**/
  for(var i=0;i<10000;i++){
    sum+=num1;
    num1+=num2;
    num2++;
  }
  ```
  第一种情况我们是使用了`new Function`来进行双重解析，而第二种是避免了双重解析。
  
8. 原生方法更快

   只要有可能，使用原生方法而不是自己用js重写。原生方法是用诸如c／c++之类的编译型语言写出来的，要比JS快多了。

9. 最小化语句数

    js代码中的语句数量也会影响所执行的操作的速度，完成多个操作的单个语句要比完成单个操作的多语句块快。故要找出可以组合在一起的语句，以减少整体的执行时间。
    
10. 避免使用属性访问方法

    js不需要属性访问方法，因为所有的属性都是外部可见的。添加属性访问方法只是增加了一层重定向，对于访问控制没有意义。
    
11. 减少使用元素位置操作

    一般浏览器都会使用增量reflow的方式将需要reflow的操作积累到一定程度然后再一起触发，但是如果脚本中要获取一下属性，那么积累的reflow将马上执行，已得到准确的位置信息。
    + offsetLeft/Top/Height/Width
    + scrollTop/Left/Width/Height
    + clientTop/Left/Width/Height
    + getComputedStyle
  
12. 复杂if语句使用switch代替

  若有一系列复杂的if-else语句，可以转化成单个switch语句则可以得到更快的代码，还可以通过通过case语句按照最可能的到最不可能的顺序进行组织，来进一步优化

13. 类型转换

  + 数组转换成字符串

    性能上：""+字符串>String()>.toString()>new String()
    
  + 浮点数转换成整型
    
    应该使用Math.floor()或者Math.round()
   
14. 使用事件代理

  + 当存在多个元素需要注册事件时，在每个元素上绑定事件本身就会对性能有一定损耗
  + 对于DOM，level2事件模型中所有事件默认会传播到上层文档对象，可以借助这个机制在上层元素注册一个统一事件对不同子元素进行响应处理。
  
15. 注意数组

  + 当需要使用数组时，可以使用JSON格式的语法

      即直接使用如下语法定义数组：［param1,param2,param3..]，而不是采用`new Array`。使用JSON格式的语法是引擎直接解释的，而后者则需要调用Array的构造器。
   
  + 如果需要遍历数组，应该先缓存数组长度，将数组长度放入局部变量中，避免多次查询数组长度

16. 字符串操作

  + 字符串进行替换、查找等循环操作，使用正则表达式
  + 字符串拼接，我们玩玩直接使用+=的方法，但是效率非常低。建议使用数组的join方法来巧妙替代。
  + 另外通常认为需要使用Array.join方式，而由于spiderMonkey等引擎对字符串的"+"运算做了优化，结果使用Array.join的效率反而不如直接使用"+"。

17. 运算符使用

  + 使用运算符时，尽量使用+=、-=、*=、\=等运算符，而不是直接赋值运算
  + 位运算

      当进行数学运算时位运算较快，位运算操作要比任何布尔运算或算数运算快，如取模、逻辑与和逻辑或都可以考虑用位运算来代替。

18. 原型优化

  + 如果一定方法类型将被频繁构造，通过方法原型从外面定义附加方法，从而避免方法的重复定义
  + 可以通过外部原型的构造方法初始化值类型的变量定义。（这里强调值类型的原因是，引用类型如果在原型中定义，一个实例对引用类型的更改就会影响到其它实例。）

    这条规则涉及js中原型的概念，构造函数都有一个prototype属性，指向另一个对象。这个对象的所有方法和属性，都会被构造函数的实例继承。可以把那些不变的属性和方法，直接定义在prototype对象上
    
    - 可以通过对象实例访问保存在原型中的值
    - 不能通过对象实例重写原型中的值
    - 在实例中添加一个与实例原型同名属性，那该属性就会屏蔽原型中的属性
    - 通过delete操作符可以删除实例中的属性

### 2.3.6 图片格式选择

  1. 颜色较为丰富的图片而且文件比较大的（40KB－200KB）或者有内容的图片优先考虑JPG；图标等颜色比较简单、文件体积不大、起装饰作用的图片，优先考虑使用PNG8格式；图像颜色丰富而且图片文件不太大（40KB以下）或有半透明效果的优先考虑PNG24格式。
  2. 条件允许的，使用新格式WEBP和BPG。
  3. 用SVG和ICONFONT代替简单的图标。
  4. 用自蛛来代替艺术字体切图，它可剔除没有使用的字符，从而解决中文字体过大的问题，并编码成跨平台兼容的格式
 
### 2.3.7 合理分配资源加载时间，按需加载，包括CSS、JS文件以及图片、业务模块等
  
  根据我们网页最初加载需要的最小内容集推断其它内容延迟加载；无条件提前加载公共内容或根据用户行为推断提前加载某些内容，如根据搜索框输入的文字来判断加载的内容。加载机制如下：

+ 预加载
+ Dom Ready 后加载
+ onLoad后加载
+ 滚动加载
 
### 2.3.8 动画优化
  动画效果在缺少硬件加速支持的情况下反应缓慢，例如手机客户端。

1. 特效应该只在确实能改善用户体验时才使用，而不应该于炫耀或者弥补功能在可用性上的缺陷
2. 至少要给用户一个选择可以禁用动画效果
3. 设置动画元素位absolute或fixed
  + `position:statice` 或 `position:relative`元素应用动画效果会造成频繁的reflow
  + `position:absolute`或`position:fixed`元素应用动画效果只需要repaint
4. 使用一个timer完成多个元素动画
  
    `setInterval`或`setTimeout`是两个常用的实现动画的接口，用以间接更新元素的风格和布局
5. 动画效果的帧率最优化的情况是使用一个timer完成多个对象的动画效果，其原因在于多个timer的调用本身就会损耗一定性能

## 2.4 DOM优化

### 2.4.1 优化DOM交互

  在JS中，DOM操作和交互要消耗大量时间，因为她们往往需要重新渲染整个页面或者某一个部分
  
1. 最小化现场更新

  + 当需要访问的DOM部分已经被渲染为页面的一部分，那么DOM操作和交互的过程就是再进行一次现场更新。
  + 现场更新是需要针对现场（相关显示页面的部分结构）立即进行更新，每一个更改（不管是插入单个字符还是移除整个片段），都有一个性能损耗。
  + 现场更新进行的越多，代码完成执行所花的时间也越长
  
2. 多使用innerHTML

  有两种在页面创建DOM节点的方法，对于小的DOM修改，两者效率差不多，但是对于大的DOM修改，innerHTML要比标准的DOM方法创建同样的DOM结构要快得多。
  
+ 使用诸如 `createElement`和`appendChild`之类的DOM方法
+ 使用innerHTML

  当使用innerHTML设置为某个值时，后台会创建一个HTML解析器，然后使用内部的DOM调用来创建DOM结构，而非基于JS的DOM调用。由于内部方法是编译好的而非解释执行，故执行更快
  
### 2.4.2 优化DOM操作

1. DOM操作性能主要有以下问题

  + DOM元素过多元素定位缓慢
  + 大量DOM接口调用

    JS和DOM之间的交互需要通过函数API接口来完成，造成延迟，尤其是在循环语句中
    
  + DOM操作触发频繁的reflow（layout）和repaint
  + layout发生在repaint之前，所以layout相对来说造成更多性能损耗。reflow(layout)就是计算页面元素的几何信息；repaint就是绘制页面元素。
  + 对DOM进行操作会导致浏览器执行回流reflow

2. 解决方案

  + 纯JS执行时间是很短的
  + 最小化DOM访问次数，尽可能在js端执行
  + 如果需要多次访问某个DOM节点，请使用局部变量存储对它的引用
  + 慎重处理HTML集合（HTML集合实时联系底层文档），把集合的长度缓存到一个变量中，并在迭代中使用它，如果需要经常操作集合，建议把它拷贝到数组中。
  + 如果可能的话，私用数组更快的API，比如querySelelctorAll 和 firstElementChild.
  + 要留意重绘和重排
  + 批量修改样式时，离线操作DOM树（何为离线操作）
  + 使用缓存并减少访问布局的次数
  + 动画中使用绝对定位，使用拖放代理（何为拖放代理）
  + 使用事件委托来减少事件处理器的数量

3. 减少DOM元素

  + 在console中执行命令查看DOM元素数量

    `document.getElementsByTagName('*').length`
    
  + 正常页面的DOM元素数量一般不应该超过1000
  + DOM元素过多会导致DOM元素查询效率，样式表匹配效率降低，是页面性能最主要的瓶颈之一。

4. 优化CSS样式转换

  如以下代码逐条更新元素的几何属性，理论上会发生多次reflow
  
  ```javascript
  element.style.fontWeight="bold";
  element.style.marginLeft="30px";
  element.style.marginRight="30px";
  ```
  可以通过直接设置元素className，触发一次reflow。
  
5. 优化的方法是创建DocumentFragment,在其中插入节点后再添加到页面

  如jQuery中所有节点操作如append，都是最终调用documentFragment来实现的
  ```javascript
  createSafeFragment(document){
    var list = nodeNames.split("|"),
   safeFrag = document.createDocumentFragment();
    if(safeFrag.createElement){
      while(list.length){
        safeFrag.createElement(
          list.pop();
        );
      }
    }
  }
  ```
  
6. 优化节点修改

  使用cloneNode在外部更新节点，然后在通过replace与原始节点交换。
  
  ```javacript
  var orig = document.getElementById('container');
  var clone =orig.cloneNode(true);
  var content;
  for(var i-0;i<list.lenght;i++){
    content =document.createTextNode(list[i]);
    clone.appendChild(content);
  }
  orig.parentNode.replaceChild(clone,orgi);
  ```
  
7. 优化节点添加

  多个节点插入操作，即使在外面设置节点的元素和风格再插入，由于多个节点还是会引发多次reflow
  
8. 回流reflow

  + 发生场景

    - 改变窗口大小
    - 改变字体
    - 添加一出stylesheet块
    - 内容改变，哪怕是输入框输入文字 
    - CSS虚类被触发，如:hover
    - 修改元素的className
    - 当对DOM节点执行新增或删除操作或内容更新时
    - 动态设置一个style样式时
    - 当获取一个必须经过计算的尺寸值时
    
  + 解决问题的关键：限制通过DOM操作引起回流的次数
    
    - 对当前DOM进行操作之前，尽可能多的做一些准备工作，保证N次创建，1次写入
    - 对DOM操作之前，把药操作的元素先从当前DOM结构中删除：通过removeChild或replaceChild实现真正意义上的删除；设置该元素的display样式为“none”。

  + 每次修改元素style属性都要触发回流操作

    - 使用更改className的方法代替style.xx的方法
    - 使用 style.cssText = '';一次性写入样式
    - 避免设置过多的行内样式
    - 添加结构外元素，尽量设置她们的位置为fixed或absolute
    - 避免使用表格来布局
    - 避免在CSS中使用JS expressions(IE only)

  + 将获取DOM数据缓存起来。这种方法，对获取那些会触发回流操作的属性（比如offsetWidth等）尤其重要
  + 对HTMLCollection对象进行操作时，应该将访问的次数尽可能的降低，最简单地，你可以将length属性缓存在一个本地变量中，这样就能大幅度地提高循环的效率

9. 重绘

  + 减少页面重绘虽然本质不是js优化，但重绘往往是由js引起的，而重绘的情况直接影响页面性能
  + 一般影响页面重绘的不仅仅是innerHTML，如果改变元素的样式、位置等情况都会触发页面重绘，所以在平时一定要注意这点。
  + 使用HTML5和CSS3的一些新特性
  + 避免在HTML里面缩放图片
  + 避免使用插件
  + 确保使用正确的字体大小
  + 决定当前页面是不是能被访问

## 2.5 变量专题

1. 全局变量

当一个变量被定义在全局作用域中，默认情况下JS引擎就不会将其回收销毁。如此该变量就会一直存在于老生代堆内存中，直到页面被关闭。所以可以通过包装函数来处理全局变量，全局变量的缺点有：

+ 使变量不易被回收
+ 多人协作时容易产生混淆
+ 在作用域链中容易被干扰

2. 局部变量

+ 尽量选用局部变量而不是全局变量
+ 局部变量的访问速度要比全局变量的访问速度更快，因为全局变量其实是window对象的成员，而局部变量是放在函数的栈内的

3. 手工解除变量使用

在业务代码中，一个变量已经确定不再需要，那么就可以手工解除变量引用，以使其被回收。

```javascript
var data = {/**some big data**/}
//...
data = null;
```

4. 变量查找优化

+ 变量声明带上`var`，如果声明变量忘记var，那么js引擎将会遍历整个作用域查找这个变量，结果不管找到与否，都会造成性能损耗。
  - 如果在上级作用域找到了这个变量，上级作用域变量的内容将被无声的修改，导致莫名其妙的错误发生
  - 如果在上级作用域没有找到该变量，这个变量将自动被声明为全局变量，然而却找不到这个全局变量的声明

+ 慎用全局变量
  - 全局变量需要搜索更长的作用域链
  - 全局变量的生命周期比全局变量长，不利用内存释放
  - 过多的全局变量容易造成混淆，增大产生bug的可能
  
+ 具有相同作用域的变量通过一个var声明

```javascript
jQuery.extend = jQuery.n.extend = function(){
	var options，
		name,
		src,
		copy,
		copyIsArray,
		clone,target = arguments[0] || {},
		i = 1,
		length = arguments.length,
		deep = false;
}
```

+ 缓存重复使用的全局变量
  - 全局变量要比局部变量需要搜索的作用域长
  - 重复调用的方法也可以通过局部缓存来提速
  - 该优化在IE上体现比较明显

5. 善用回调

除了使用闭包进行内部变量访问，我们还可以使用现在流行的回调函数来进行业务处理

```javascript
function getData(callback){
  var data='some big data';
  callback(null,data);
}
getData(function(err,data){
  console.log(data);
})
```
回调函数是一种后续传递风格（Continuation Passing Style,CPS) 的技术，这种风格的程序编写将函数的业务重点从返回值转移到回调函数中去，而且其相比闭包的好处也有很多。

+ 如果传入的参数是基本类型（如字符串、数值），回调函数中传入的形参就会是复制值，业务代码使用完以后，就更容易被回收
+ 通过回调，除了可以完成同步的请求外，还可以用在异步编程中，这也就是现在非常流行的编程格式
+ 回调函数自身通常也是临时的匿名函数，一旦请求函数执行完毕，回调函数自身的引用就会被解除，自身也得到回收

## 2.6 对象专题

1. 减少不必要的对象创建

+ 创建对象本身对性能影响并不大，但是js的垃圾回收调度算法，导致随着对象个数的增加，性能会开始严重下降（复杂度o(n^2))。

如常见的字符串拼接问题，单纯的多次创建字符串对象其实根本不会是降低性能的主要原因，而是在对象创建期间的所谓的垃圾回收的开销。而Array.join的方式，不会创建中间字符串对象，因此就减少了垃圾回收的开销

+ 复杂的js对象，其创建时间和空间的开销都很大，应该尽量考虑使用缓存
+ 尽量使用json格式来创建对象，而不是var obj = new Object().前者是直接复制，而后者需要调用构造器。

2. 对象查找

+ 避免对象的嵌套查询，因为js的解释器，a.b.c.d.e嵌入对象需要进行4次查询，嵌套对象成员会明显影响性能
+ 如果出现嵌套对象，可以利用局部变量，把它放在一个临时的地方进行查询

3. 对象属性

访问对象属性是个消耗性能过程

+ 先从本地变量表中找到对象
+ 然后遍历属性
+ 如果在当前对象的属性列表中没有找到
+ 继续沿着prototype向上查找
+ 且不能直接索引，只能遍历

## 2.7循环优化

1. js提供三种循环
  + for
    - 推荐使用for循环，循环变量递减或递增，不要单独对循环变量赋值，而应该使用嵌套的`++`或`--`运算符
    - 代码可能性对于for循环的优化
    - 使用`-=1`
    - 从大到小的方式循环
  + while

    for和while的性能基本持平

  + for(in)

    在这三个循环中for(in)内部实现是构造一个所有元素的列表，包括array继承的属性，然后再开始循环，并且需要查询`hasOwnProperty`。
    
2. 选择正确的方法

  + 避免不必要的属性查找
    - 访问变量或数组是o(1) 操作
    - 访问对象上的属性是一个o(n)操作
      对象上的任何属性查找都比访问变量或数组花费更长时间，因为必须在原型链中对该名称的属性进行一次搜索，即属性查找越多，执行时间越长。所以针对需要多次用刀对象属性，应该将其存储在局部变量。
  + 优化循环
    - 减值迭代
      大多数循环使用一个从0开始，增大到某个特定值的迭代器。在很多情况下，从最大值开始，在循环中不断减值的迭代器更有效
    - 简化终止条件
      由于每次循环过程都会计算终止条件，故必须保证它尽可能快，即避免属性查找或其它o(n)的操作
    - 简化循环体
      最常用的for和while循环都是前测试循环，而do-while循环可以避免最初终止条件的计算，因此计算更快
  + 展开循环：当循环次数确定时，消除循环并使用多次函数调用往往更快
  + 展开循环：当循环次数不确定时，可以使用Duff装置来优化
    - Duff装置的基本概念时通过计算迭代的次数是否为8的倍数将一个循环展开成一系列语句
      
      ```javascript
      function process(v){ alert(v);}
      var values = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17];
      var iterations = Math.ceil(values.length/8);
      var startAt = values.length%8;
      var i=0;
      do{
        switch(startAt){
          case 0:process(values[i++]);
          case 1:process(values[i++]);
          case 2:process(values[i++]);
          case 3:process(values[i++]);
          case 4:process(values[i++]);
          case 5:process(values[i++]);
          case 6:process(values[i++]);
          case 7:process(values[i++]);
        }
        startAt=0;
      }while(--iterations<0);
      ```
    - 如上展开可以提升大数据集的处理速度。接下来给出更快的Duff装置技术，将do-while循环分成2个单独的循环（这种方式几乎比原始的Duff装置实现快上40%）
      ```javascript
      function process(v){ alert(v);}
      var values = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17];
      var iterations = Math.ceil(values.length/8);
      var leftover = values.length%8;
      var i=0;
      if(leftover>0){
        do{
          process(values[i++]);
        }while(--leftover>0)
      }
      do{
        process(values[i++]);
        process(values[i++]);
        process(values[i++]);
        process(values[i++]);
        process(values[i++]);
        process(values[i++]);
        process(values[i++]);
        process(values[i++]);
      }while(--iterations>0);
      ```
      针对大数据集使用展开循环可以节省很多时间，但对于小数据集额外的开销则可能得不偿失。
3. 避免在循环中使用try-catch,入锅需要异常处理机制，可以将其放在循环外层使用
4. 避免遍历大量元素

## 2.8 内存专题

1. js内存回收机制

   + 以Google的v8引擎为例，其中所有js对象都是通过堆来进行内存分配的。当我们在代码中声明变量并赋值，引擎就会在堆内存中分配一部分给这个变量。如果已申请的内存不足以存储这个变量时，v8引擎就会继续申请内存，直到堆的大小达到了v8引擎的内存上限为止（默认情况下，v8引擎的堆内存大小上限在64位系统中为1464MB，在32位系统中则为732MB）
   + 另外，v8引擎对堆内存中的js对象进行分代管理
     - 新生代：即存活周期较短的js对象，如临时变量、字符串等
     - 老生代：则为多次垃圾回收依然存活，存活周期较长的对象，如主控制器、服务器对象等
     
2. 垃圾回收算法

垃圾回收算法一直都是编程语言研发中重要的一环，而v8引擎所使用的垃圾回收算法主要是以下几种

  + Scavenge算法：通过复制的方法进行内存空间管理，主要用于新生代的内存空间
  + Mark-Sweep算法和Mark-Compact算法：通过标记来对堆内存进行整理和回收，主要用于老生代对象的检查和回收

3. 对象回收

  + 当函数执行完毕时，在函数内部所声明的对象不一定会被销毁
  + 引用是js编程中十分重要的一个机制

    是指代码对对象的访问这个抽象关系，它和C／C++ 的指针类似，但并非同物。引用同时也是js引擎在进行来记回收中最关键的一个机制。
    
    ```javascript
    var val = 'hello world';
    function foo(){
      return function(){
        return val;
      }
    }
    global.bar = foo();
    ```
    
    当代码执行完毕，对象val和bar并没有被回收释放，js代码中，俄米格变量作为单独一行而不做任何操作，js引擎都会认为这是对对象的访问行为，存在对对象的引用。为了保证垃圾回收的行为不影响程序的逻辑行为，js引擎不会把正在使用的对象进行回收。所以判断对象是否在在使用中的标准，就是是否依然存在对该对象的引用。

  + js的引用是可以转移的，那么就有可能出现某些引用被带到了全局作用域，但事实上在业务逻辑里已经不需要对其进行访问了，这个时候就应该被回收，但是js引擎依然认为程序需要它

4. IE下闭包引起跨页面内存泄露
5. js的内存泄漏处理

  + 给DOM对象添加的属性是一个对象的引用

    ```javascript
    var myObject = {};
    document.getElementById("myDiv").myProp = myObject;
    ```
    
    解决方法：在window.onunload事件中写上
    ```javascript
    document.getElementById("myDiv").myProp = null;
    ```

  + DOM对象与JS对象相互引用
  
    ```javascript
    function Encapsulator(element){
      this.elementReference = element;
      element.myProp = this;
    }
    new Encapsulator(document.getElementById("myDiv"))
    ```
    
    解决方法：在onunload事件中写入
    
    ```javascript
    document.getElementById('id').myProp = null;
    ```
  + DOM对象用attachEvent绑定事件
  
    ```javascript
    function doClick(){}
    element.attachEvent("onClick",doClick);
    ```
    
    解决办法：在
    ```javascript
    ```
  + 从外到内执行appendChild，这时即使调用removeChild也无法释放
  + 反复重写同一个属性会造成内存大幅占用（但关闭IE后内存会被释放）