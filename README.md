## Pixiv每日排行榜Top50小部件
![Pixiv每日排行榜Top50小部件效果图](https://ww1.sinaimg.cn/large/647b8589gy1fd6meqio1vj20720cbdma)
## 简介
骚年，你是`ACG`或绘画爱好者吗？你希望在你的博客或网站中添加一个 **`Pixiv`每日排行榜Top50** 的展示功能吗？现在，无需在茫茫互联网中寻找适合自己站点的插件了，只需要几个文件或是一行代码即可实现！

## 特色
- 一行`HTML`代码即可调用，方便快捷
- 适合放在大部分博客或网站的侧边栏
- 自适应宽高。推荐宽度`240px`、高度`380px`
- 点击图片可跳转到对应作品详情页
- 每日自动更新，无需人工干预
- 内置多图床支持、按需加载图片，极低资源消耗
- 提供API服务，含有更新日期、缩略图url及详情页url

## 开源地址
[Github](https://github.com/mokeyjay/Pixiv-daily-top50-widget)

## 如何部署
### 方案一：使用[超能小紫](https://www.mokeyjay.com)提供的服务
该方案适用于动手能力较差或较懒或没有特殊需求的用户。且已配置数个图床，访问速度较快  
服务地址：[https://cloud.mokeyjay.com/pixiv](https://cloud.mokeyjay.com/pixiv)  
以`Wordpress`为例，首先进入 后台 -> 外观 -> 小工具  
向右边适当的位置添加一个 **文本** 或 **自定义HTML** 小工具，标题随意，内容为  
```html
<iframe src="https://cloud.mokeyjay.com/pixiv" frameborder="0"  style="width:240px; height:380px;"></iframe>
```
点击保存按钮即可回到博客首页预览效果咯~  
如果你了解`CSS`的话，还可以随意修改`iframe`的`style`属性  
推荐宽度`240px`、高度`380px` （因为P站缩略图最大就是这个尺寸）  

#### 自定义背景颜色
默认的背景颜色是`#fff`（纯白色），如果你的页面背景颜色与之不符，你可以传参来改变它  
例如将上面`iframe`的`src`属性的值改为`https://cloud.mokeyjay.com/pixiv/?color=f00`试试看？  
正常情况下背景颜色会变成**红色**，即`#f00`。如果颜色没有改变，可能是缓存问题，刷新几次即可  
`color`的值就是CSS内使用的颜色值，可为3或6位16进制字符。无需 **#** 号  
#### 自定义Top数量
你还可以通过`limit`参数限制图片数量  
例如`https://cloud.mokeyjay.com/pixiv/?color=f00&limit=10`  
则可以得到背景为红色的Top10画册  
**请注意：** `limit`参数的范围为`1-50`  
#### API服务
[图床缩略图URL+详情页URL](https://cloud.mokeyjay.com/pixiv/storage/app/pixiv.json)（推荐）  
[Pixiv原始缩略图URL+详情页URL](https://cloud.mokeyjay.com/pixiv/storage/app/source.json)  
内容很简单，相信大家看了就知道可以怎么用了，不再赘述  

---
### 方案二：自行架设服务
适用于动手能力较强或需要深度自定义的用户  
> 需要PHP版本 >= 5.4

首先[下载源代码](https://github.com/mokeyjay/Pixiv-daily-top50-widget/archive/master.zip)，解压  
使用专业编辑器（例如`Sublime`、`Notepad++`等，切忌使用记事本）编辑`config.php`，根据实际情况修改相应配置  
> 由于Pixiv已经被墙，如果你想要将此项目部署在国内，请务必配置 `proxy` 配置项   

> 每个配置项的说明都以注释的形式标注在文件内。如果你看不懂，那就说明你比较适合**方案一**    

最后一步，给予`storage`目录读写权限

> 为了更好的用户体验，你还可以设定一个如下的定时任务来主动触发刷新任务  
> `1 0 * * * php [本项目路径]/index.php -j refresh`  
> 如果你这么做了，而且还使用了 `local` 图床，则务必设置 `url` 配置项。因为 cli 模式下无法获得当前url，如果 url 配置项依旧留空，则生成的图片url地址可能会有问题

### 注意事项
- 推荐使用方案一，由我本人维护，如有问题第一时间更新
- 方案二反馈问题之前，请先将 `log_level` 设为 `['ERROR', 'DEBUG']` ，并再次重现问题后，带着 `logs` 来反馈
- 本项目免费开源，仅供学习交流。请勿用于任何商业用途，作者不承担任何责任  

## 更新日志
### 4.0 🎉
- 几乎重写了所有代码的船新版本，更多新特性与bug等你来发掘！
- 由于pixiv全面开启反盗链，为了迎合此变化。已将`download`和`url_cache`这两个不再有存在意义的开关去除。现在会强制下载缩略图，然后再根据配置上传到各个图床或存储在服务器本地
> 碎碎念：原本这个项目只是随便搞搞，没想到后面功能越堆越多，代码也越来越丑。作为本辣鸡github上最高star的项目实在是丢人。好在我花了几天时间撸了这个4.0，总算是不那么丢人了  
> 还有就是添加了多图床的支持，每个月能节省几百G的流量了嘤

### 3.0
- 添加`$download_proxy`配置项
- 由于Pixiv的图片url添加了防盗链无法被直接显示，因此`$download`配置项默认开启
  为了更好的显示效果，自行部署的用户建议配置一个定时任务，每天0点触发`download.php`

### 2.9
- 修复因Pixiv改动导致挂掉的问题

### 2.8
- 尝试优化更新锁，防止高并发下重复更新
- 从 Conf::$download 中独立出配置项 Conf::$url_cache，现在可以仅缓存图片url而不缓存缩略图了
- 添加贴图库图床支持

> 贴图库免费版并不是很好用且不支持https，建议优先使用sm.ms，贴图库仅作为备用
> 由于之前更新锁在高并发下有些问题无法很好的发挥作用，导致我的服务器IP因重复上传被sm.ms图床封了。而我个人也无力支撑高昂的CDN费用。<del>因此即日起**方案一**不再提供CDN加速，改为直接从P站获取图片</del>  
> 方案一目前由360网站卫士提供CDN支持

### 2.7
- 添加图片压缩功能，降低服务器带宽压力（需要GD库）
- 修复sm.ms图床支持，降低失败概率
- 添加sm.ms图床上传日志

> 如果开启`$enable_smms`出现问题，反馈时请带上日志文件

### 2.6
- 添加sm.ms图床支持。一键启用即可大幅降低服务器带宽压力、节省流量。感谢[@Showfom](https://sb.sb/)提供图床  

> 我才不告诉你是因为方案一每天跑掉我几G流量，心疼不已才加的这个功能呢
> 如果连续3次上传失败，则从服务器本地读取图片，确保访问正常

### 2.5
- 修复因Pixiv改版导致挂掉的问题
- Pixiv原生支持https啦！可喜可贺

### 2.4
- 修复特定情况下URL的`limit`参数无效的问题
- 修复**方案一**缓存问题
- 修复上面效果图SSL证书问题

### 2.3
- 更换了前端库引用地址，修复移动宽带下加载慢的问题
- 添加协议自适应，修复在关闭缓存或缓存还没全部完成时影响小绿锁的问题
- 以上更新来自@灵乌路空 的友情PR，我们一起对她PRPR以示感激吧
- 超能小紫的方案一服务现已支持HTTPS。咬牙忍痛上了收费CDN，请大家且用且珍惜
- 要是被滥用到我吃不消费用的话可能会暂停服务噢~
- 如果访问量较高的话建议还是自行搭建服务，谢谢各位的支持与谅解

### 2.2
- 优化下载线程以支持自行部署HTTPS

### 2.1
- 规划2.0时脑子抽了，非要把所有逻辑都局限在一个文件里。虽然各方面确实有所提升，但在一些情况下照样会出现那些老问题。例如缩略图下载失败啊、PHP超时导致下载中断之类。因此在我测试并意识到这一点时，赶紧开始了新版本的开发 <del>光速打脸</del>
- 去除自动更新锁机制，缩略图已存在并且有效时不再重复下载。防止因网络波动或超时导致的缩略图下载失败

### 2.0
- 整体重构，各机制大幅优化
- 添加自动更新锁机制，避免高访问量时并发更新浪费资源
- 全新的伪多线程自动更新机制，后台更新不影响使用
- 更新失败重试，避免因为网络问题导致的部分图片获取失败

## 初衷
前几天跟朋友聊天，朋友说希望能在自己博客侧边栏中显示[Pixiv](http://www.pixiv.net/)的每日排行榜。我自己也是个`ACG`爱好者，被他这么一说也想弄一个。昨晚终于有空，花了半个多小时写完。[自己博客](https://www.mokeyjay.com)用上了感觉不错，完善了一下加了点功能开源出来福利各位

## 关于作者
[超能小紫](https://www.mokeyjay.com)，常用ID`mokeyjay`。热爱IT与ACG的学渣