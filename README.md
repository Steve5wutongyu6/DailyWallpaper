# Bing.js
下载每天的bing壁纸到阿里云OSS中,通过js进行调用

# 使用方法
你可以在多种环境下运行该程序`青龙面板` `阿里云云函数` `CloudFlare Workers` 都是支持的环境
> 非常推荐通过青龙面板使用此脚本,若你使用阿里云服务器,后期将支持内网上传下载,节约成本
## 安装与部署

### 第一部分:对接bing.js与青龙面板
1. 装好青龙面板,确保你的机器能够访问bing和你的存储桶
2. 进入青龙面板-脚本管理,点击右上角加号,新建名为bing.js的脚本并复制[Bing.js](https://github.com/Steve5wutongyu6/Bing.js/blob/main/bing.js)脚本内容到输入框
3. 进入青龙面板-定时任务-新建任务,输入任务名称.命令为task bing.js(注意根据你保存的路径加以变动),定时规则请参考crontab进行设置,点击确定
4. 进入青龙面板-依赖管理,安装如下依赖`ali-oss` `moment` `axios`
5. 进入青龙面板-环境变量按照下表


| 环境变量        | 内容                       |
| --------------- | -------------------------- |
| region          | 填写OSS地域,注意以oss-开头 |
| bucket          | 存储桶名称                 |
| accesskeyid     | 从阿里云获取               |
| accesskeysecret | 从阿里云获取               |
| folder          | 在OSS中存储图片的文件夹    |

6. 现在进入青龙面板-定时任务,点击运行键测试,出现如下输出即为正常
   ![image](https://github.com/Steve5wutongyu6/Bing.js/assets/77491648/00262856-f34a-405a-9a13-624752a1e139)

### 第二部分:对接Web页面和OSS
1. 下载项目的web文件夹中的内容到你的主机上
2. 按照注释修改/js/bingwallpaper.js
   > (为了安全,建议部署时对js文件进行加密,防止OSS地址暴露;或者部署在OSS同地域云函数上通过内网访问.此为临时措施,后续更新将加入鉴权功能)
3. 访问你的地址,可以看到最新的bing壁纸,URL后加上`?date=你需要的日期如20230716`即可访问对应日期图片(前提是已经缓存在OSS中)

## TODO
1. 加入鉴权功能,你也不希望OSS被刷流量对吧?
2. 对接多种存储(没准做成类似PicGO那种万能图床?)
3. 加入画廊功能
4. 桌面应用(官方的Bing壁纸不太好使,DynamicTheme在我电脑上总是掉,我研究哈子能不能自个搓一个)
