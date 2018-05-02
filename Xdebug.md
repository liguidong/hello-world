### Xdebu安装使用过程——李不知

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

phpstorm开启监听

![image.png](https://wt-box.worktile.com/public/fd519e8c-2744-470e-9111-0397460f113d)

3.打断点，浏览器中访问，即可看到效果，F9下一步