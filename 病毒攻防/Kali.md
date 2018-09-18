####kali使用:<br>
 - #####添加更新源<br>
 	`leafpad /etc/apt/sources.list`<br>
	打开更新源配置文件,将下面的更新源复制到原内容的前面:
	```
		#163网易 Kali源
	deb http://mirrors.163.com/debian wheezy main non-free contrib 
	deb-src http://mirrors.163.com/debian wheezy main non-free contrib 
	deb http://mirrors.163.com/debian wheezy-proposed-updates main non-free contrib 
	deb-src http://mirrors.163.com/debian wheezy-proposed-updates main non-free contrib 
	deb-src http://mirrors.163.com/debian-security wheezy/updates main non-free contrib 
	deb http://mirrors.163.com/debian-security wheezy/updates main non-free contrib
	
	#阿里云 Kali源
	deb http://mirrors.aliyun.com/kali kali main non-free contrib
	deb-src http://mirrors.aliyun.com/kali kali main non-free contrib
	deb http://mirrors.aliyun.com/kali-security kali/updates main contrib non-free
	
	#中科大 Kali源
	deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
	deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
	
	#浙江大学 Kali源
	deb http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
	deb-src http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
	
	#东软大学 Kali源
	deb http://mirrors.neusoft.edu.cn/kali kali-rolling/main non-free contrib
	deb-src http://mirrors.neusoft.edu.cn/kali kali-rolling/main non-free contrib
	
	#重庆大学 Kali源
	deb http://http.kali.org/kali kali-rolling main non-free contrib
	deb-src http://http.kali.org/kali kali-rolling main non-free contrib
	
	#官方Kali源
	#deb http://http.kali.org/kali kali-rolling main non-free contrib
	#deb-src http://http.kali.org/kali kali-rolling main non-free contrib
	```	
 - 更新系统
 	- `apt-get update`
 - 安装fcitx
	- apt-get install fcitx
 - 安装Google拼音输入法
   - apt-get install fcitx-googlepinyin
 - 重启系统 
   - `reboot	`	


- 解决Kali“没有Release文件”，“下列签名无效”等问题:
  - 原因：Kali Linux由于太长时间未更新，密钥过期了，更新密钥即可。`apt-key adv --keyserver hkp://keys.gnupg.net --recv-keys 7D8D0BF6`
  - `apt-get update` && `apt-get dist-upgrade`

- 远程登录 `ssh username@域名`
- 开启ssh服务`service ssh start`
- 查看ssh状态`/etc/init.d/ssh status`
- 修改配置文件 允许账号登录 `vi /etc/ssh/sshd_config`
	- 将PermitRootLogin 改为yes 
- 重启`service ssh restart`
- 新增普通用户
- kali
	- useradd -m userName
	- passwd userName
	- su userName 切换账号
	- chsh -s /bin/bash userName  
	- su root 提权
	- reboot 重启
- ubuntu
	- `sudo adduser username `

- 开通ftp
	-  `apt-get install vsftpd`
	-  `service vsftpd start`
	-  `vim /etc/ftpusers`
	-  `service vsftpd restart`