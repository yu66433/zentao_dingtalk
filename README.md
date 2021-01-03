## 功能说明：为禅道开源码版12.4.3 添加钉钉第三方登录插件。
### 使用方式：导入数据库文件，然后将文件直接复制覆盖到禅道源码版里并即可，如果版本原因不能使用，请按第四点方法更改代码。注意复盖前请备份好环境代码。
### 原改改动：钉钉注册及登录方式设置,在my.php里的logintype参数可以设置为【0仅允许绑定过钉钉的账号扫码登录, 1允许钉钉扫码注册并登录(原版模式,推荐新平台搭建注册人员使用方便)】
### 最新改动：增加了同步钉钉部门信息，同时禁止外部员工登录。

### 钉钉配置说明
钉钉上需要开通2个应用 ，首先需要拿到钉钉管理员账号，登入到https://open-dev.dingtalk.com

## 创建H5微应用
应用开发-》H5微应用-》创建应用，应用类型选择H5微应用，填应用名称和应用描述，开发方式选择企业自助开发。创建好后记录下AppKey和AppSecret，供my.php配置参数使用。
进入刚创建的H5微应用-》开发管理-》服务器出口IP填写禅道公网出口IP，服务器查询公网IP自己百度，应用首页地址填禅道部署访问域名或者IP。
授权读取通讯录功能-》权限管理-》添加接口权限-》通讯录只读权限，手机号码信息，邮箱等个人信息进行授权。

## 创建扫码登录
应用开发-》登录-》创建扫码登录应用受权
名称，描述随便填，授权LOGO地址和调域名直接填禅道部署访问域名或者IP。

### 安装说明：

#### 一、数据库更改：
* 数据库执行zentao_dt_mysql.sql文件，为数据库用户表zt_user添加钉钉用户数据字段


#### 二、安装方法：
* 将所有文件复制到禅道的安装目录下,假如禅道的安装目录为```/opt/zentaopms```，使用命令如下：
```
cd zentao_dingtalk 
cp -R * /optzentaopms
```

#### 三、配置增加：
* /config/my.php 最后增加了钉钉参数配置, 请将配置里的钉钉参数修改为你的钉钉参数
```
/* 钉钉登录配置 */
$config->ding->ddturnon = true;/* 是否开启钉钉登录 */
$config->ding->logintype = 1;/* 钉钉登录方式,0仅允许绑定登录,1允许自动注册登录(建议新平台使用此方法,方便人员自行添加) */
$config->ding->appid = '';/* 钉钉扫码登录appId */
$config->ding->appsecret = '';/* 钉钉扫码登录appSecret */
$config->ding->redirect = '';/* 回调地址域名,与钉钉管理后台保持一致 */
$config->ding->inter_appkey = '';/* 钉钉H5微应用appkey */
$config->ding->inter_appsecret = '';/* 钉钉H5微应用AppSecret */
```


### 效果图如下

#### 账号密码登录
![image](img/lonig1.png)
#### 钉钉扫码登录
![image](img/lonig2.png)
#### 同步组织结构
![image](img/dept.png)
#### 绑定钉钉扫码登录
![image](img/bind.png)
