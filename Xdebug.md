### Xdebu配置过程——李不知

> 2018年9月3日Update:增加虚拟机Xdebug的安装方式
>
> vagrant 远程调试 配置，直接跳到下方，windows

---

#### 【Windows】本地集成环境等

#### 下载安装对应版本

1.`http://www.xdebug.org/find-binary.php`复制phpinfo提交后得到对应版本下载地址

2.按其说明放入对应ext目录

3.php.ini中

```ini
zend_extension = "C:\phpStudy\PHPTutorial\php\php-7.0.12-nts\ext\php_xdebug-2.6.0-7.0-vc14-nts.dll"
xdebug.remote_enable =1
xdebug.remote_handler = "dbgp"
xdebug.remote_host = "localhost"
xdebug.remote_mode = "req"
xdebug.remote_port = 9001
xdebug.idekey="PHPSTORM"
```

4.phpinfo 验证是否安装成功

#### PHPStorm配置

File → Default Setting → Languages & Frameworks → PHP

![1525270877480](https://wt-box.worktile.com/public/467eee3c-2b08-405b-b202-589f846d7862)

![1525270922295](https://wt-box.worktile.com/public/467eee3c-2b08-405b-b202-589f846d7862)



Debug

![1525270953215](https://wt-box.worktile.com/public/4e5fecef-72ca-4fa1-9e0c-9475095148ba)

DBGp Proxy

![1525271000598](https://wt-box.worktile.com/public/86162480-fd6f-4355-a1ce-f1228efa0949)

### 使用

1.chrome安装对应插件（Xdebug helper）

![image.png](https://wt-box.worktile.com/public/b24d9a93-fd87-4c2f-b8a0-e8ed032df6c9)

2.启用插件，启用phpstorm的监听（电话图标）

chrome中右击Xdebug helper图标，选项，进行配置

开启插件的监听，点击debug，等其变成原谅色

phpstorm开启监听

![image.png](https://wt-box.worktile.com/public/fd519e8c-2744-470e-9111-0397460f113d)

3.打断点，浏览器中访问，即可看到效果，F9下一步



---



#### 【虚拟机】vagrant docker等

相对于windows本地环境的配置，略增加了一些细节的修改，整个步骤大体分为

1. php安装xdebug扩展，php.ini配置
2. phpstorm监听，共享目录等设置
3. 浏览器xdebug扩展安装



一、 根据php版本wget对应的xdebug包 `这里提供php5.4对应的包地址`

```bash
wget https://xdebug.org/files/xdebug-2.4.1.tgz//下载
```

二、使用phpize安装扩展

```bash
wget https://xdebug.org/files/xdebug-2.4.1.tgz//下载
tar xvzf xdebug-2.4.1.tgz//解压
cd xdebug-2.4.1
phpize
./configure --enable-xdebug --with-php-config=/usr/local/php/bin/php-config
make
make install
```

此时应能在php扩展目录看到xdebug.so

三、 phpinfo查看xdebug安装是否正常（部分环境因为安全需要禁用了phpinfo，需要修改php.ini开启）

![image](https://ws1.sinaimg.cn/large/006tNbRwgy1fuwdsh0popj30o90fs409.jpg)

四、 修改php.ini 添加xdebug相关配置

```
[Xdebug]
zend_extension = /usr/local/server/php/lib/php/extensions/no-debug-non-zts-20100525/xdebug.so
xdebug.remote_enable =1
xdebug.remote_handler = dbgp
xdebug.remote_host = 10.0.2.2 
xdebug.remote_mode = req
xdebug.remote_port = 9001
xdebug.idekey = PHPSTORM
xdebug.remote_autostart = 1
xdebug.remote_log = /tmp/xdebug.log
```

xdebug.remote_host 为**客户端ip**，此处客户端的概念指phpstorm所在的机器

![image](https://ws1.sinaimg.cn/large/006tNbRwgy1fuwdx9b7qsj30ft05rwex.jpg)

一般多数服务是我们本机通过对应的端口去请求它，xdebug却相反，是服务器端来请求客户端，phpstorm配置对应的端口来进行监听，phpstorm所在的机器即为客户端，所以此处xdebug.remote_host 所填的地址可通过`$_SERVER['REMOTE_ADDR']`来获取，这里划重点，网上众说纷纭，此处**请填客户端ip**，勿填成了虚拟机ip

xdebug.remote_port 为约定的端口，默认为9000，有人说fastcgi会占用这个端口，所以我换成了9001

xdebug.remote_log 为日志选项，调试正常，可以使用之后，可以将其去掉

此处再提一点：**约定的端口（9001）不用转发**，本人便吃了自作聪明的亏

五、修改phpstorm相关配置

5.1 解释器修改为远程解释器，例如配置为vagrant 虚拟机中的php

![image](https://ws3.sinaimg.cn/large/006tNbRwgy1fuweb7l98uj31kw0y1453.jpg)

![image](https://ws2.sinaimg.cn/large/006tNbRwgy1fuwecykg58j319s11kwjb.jpg)

5.2 修改为约定的端口

![image](https://ws3.sinaimg.cn/large/006tNbRwgy1fuwedwawk0j316g0rgq9j.jpg)

5.3 配置DBGp

![image](https://ws2.sinaimg.cn/large/006tNbRwgy1fuweffj694j316o0mu77i.jpg)

按理来说，配置到此处PHPStorm的配置就告一段落了，但网上很多文章提到需要配置这个

![image](/var/folders/gn/f1q1mvl10gl4xlwtgcsljzs80000gn/T/abnerworks.Typora/image-20180903155316261.png)

个人实测，是不用配置的，当开始调试，服务端与客户端正常通信后会自动创建（你看着办吧）

配置好后，开启phpstorm的监听

![image](/var/folders/gn/f1q1mvl10gl4xlwtgcsljzs80000gn/T/abnerworks.Typora/image-20180903160415573.png)

六、 chrome安装对应扩展

https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc

当然如果你没梯子，就这里下吧

https://www.crx4chrome.com/extensions/eadndfjplgieldjbigjakmdgkmoaaaoc/

装好后，右击->选项，配置key

![image](https://ws3.sinaimg.cn/large/006tNbRwgy1fuwety8estj30fq03a74d.jpg)

接着在需要调试的页面，将他点成原谅色即启用啦

![image](https://ws3.sinaimg.cn/large/006tNbRwgy1fuweuoxofgj308502x0st.jpg)



写在最后

大体上就是这样，有问题就根据xdebug.log来google一下