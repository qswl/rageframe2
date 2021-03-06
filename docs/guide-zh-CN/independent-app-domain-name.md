## 应用配置独立域名

##### 1、在群里([加群链接](https://jq.qq.com/?_wv=1027&k=4BeVA2r))下载应用配置独立域名包：

解压后可见有2个文件夹

- environments 目录
- web 目录

##### 2、替换根目录下的 `environments` 为下载内 `environments`

##### 3、将下载好的web目录整个单独放入各种的应用下例如：

```
backend/web
frontend/web
api/web
wechat/web
```

##### 4、将根目录web下各自的resources放入各自的web下例如：

```
web/resources => frontend/web/resources
web/backend/resources => backend/web/resources
web/wechat/resources => wechat/web/resources
```

> 注意: api是没有此目录


##### 5、设置各自的应用的虚拟站点到各自应用的web下例如：

```
127.0.0.1       rageframe.local
127.0.0.1       backend.rageframe.local
127.0.0.1       wechat.rageframe.local
127.0.0.1       api.rageframe.local
127.0.0.1       storage.rageframe.local
```

##### 6、修改 `common/config/bootstrap.php` 下的 `attachment`和`attachurl`：

```
Yii::setAlias('@attachment', dirname(dirname(__DIR__)) . '/storage/web/attachment');
// 注意这里的域名为你的文件存储域名,记得带上http://前缀
Yii::setAlias('@attachurl', 'http://storage.rageframe.local/attachment');
```

##### 7、修改 `common/config/params.php` 

关于 fullPath 变量都设置为false，注意有4处

```
'fullPath' => false, // 是否开启返回完整的文件路径
```

并在 `siteDomain` 里面填写对应的域名信息

```
'siteDomain' => [
    'backend' => 'http://backend.rageframe.local',
    'frontend' => 'http://frontend.rageframe.local',
    'wechat' => 'http://wechat.rageframe.local',
    'api' => 'http://api.rageframe.local',
],
```

##### 8、删除根目录下的`web`目录