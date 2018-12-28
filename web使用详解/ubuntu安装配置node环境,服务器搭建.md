linux:
===
- ####下载git<br>
`sudo yum install git`
 
- ####下载node<br>
 `wget https://nodejs.org/dist/v8.9.1/node-v8.9.1-linux-x64.tar.xz`
- ####配置<br>
	- 创建一个文件夹node<br>`mkdir node` 
	- 解压：<br> `tar xvf node-v8.9.1-linux-x64.tar.xz --strip-components=1 -C ./node`
	- 配置node为全局环境变量，使用npm可以安装node包。 
执行：`mkdir node/etc`
	- 执行：<br>`echo 'prefix=/usr/local' > node/etc/npmrc  `
	- 将node文件移动到opt文件目录下：<br>`sudo mv node /opt/`
	- 给当前用户这个文件的所属权限，就是可以操作这个文件目录下的文件。<br>`sudo chown -R root: /opt/node`
	- 配置node和npm的系统路径，执行：<br>`sudo ln -s /opt/node/bin/node /usr/local/bin/node`<br>`sudo ln -s /opt/node/bin/npm /usr/local/bin/npm`<br>
	- `sudo npm install pm2@latest -g`测试 
	
	
###MongoDB安装配置
- `curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.0.6.tgz`下载
- `tar -zxvf mongodb-linux-x86_64-3.0.6.tgz`解压
- `mv  mongodb-linux-x86_64-3.0.6/ /usr/local/mongodb`移动
- `cd /usr/local/mongodb/bin`移动
- `vi ~/.bash_profile`配置
- 在其中添加`PATH=$PATH:/usr/local/mongodb/bin`(路径)
- `source ~/.bash_profile`配置

###服务器搭建<br>
- `cd /var`进入本地文件夹
- `mkdir mongodb` 
- `cd mongodb`创建并进入mongodb文件夹
- `mkdir db`创建存放的数据库
- 使用ftp将blog文件上传至`/var`
- `mongod --dbpath /var/mongodb/db --fork --logpath /var/mongodb/log/log`启动常驻数据库MongoDB
- `kill {forked process:中的值}`终止MongoDB程序
- 或者
	- `mongo` 
	- `use admin`
	- `db.shutdownServer()`终止mongo程序
- 进入blog , `pm2 start app.js`启动项目
- `pm2 stop id值`终止





####vps的搭建

```
wget --no-check-certificate -O shadowsocks.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh

chmod +x shadowsocks.sh
./shadowsocks.sh 2>&1 | tee shadowsocks.log
```

配置ss以后  通过 shadowsocks 搭建vpn 




####java配置<br>
  - mkdir /usr/local/java/
  - tar -zxvf jdk-8u171-linux-x64.tar.gz -C /usr/local/java/
  - vim /etc/profile
  - export JAVA_HOME=/usr/local/java/jdk1.8.0_171
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
  - source /etc/profile
  - ln -s /usr/local/java/jdk1.8.0_171/bin/java /usr/bin/java

####tomcat配置<br>
  -  echo "export CATALINA_HOME="/usr/local/tomcat9"" >> ~/.bashrc
  -  source ~/.bashrc

####解决linux乱码
  -  jdbc:mysql://localhost:3306/test?&amp;useUnicode=true&amp;characterEncoding=gbk
&amp;autoReconnect=true&amp;failOverReadOnly=false

