# linux常用命令



### 压缩,解压

	tar -zxvf xxx.tar.gz -C xxx 将xxx.tar.gz解压到xxx
	tar -zcvf xxx.tar.gz xxx 将xxx压缩成xxx.tar.gz
	unrar x xxx.rar xxx 将xxx.rar解压到xxx
	unzip xxx.zip -d xxx 将xxx.zip解压到xxx
 

### xargs

	ls | xargs -I {} cp -rf {} {}.bak



### awk 用法：awk 'pattern {action}'

	∘ pattern可以是以下任意一个：
	‣ /正则表达式/：使用通配符的扩展集。
	‣ 关系表达式：可以用下面运算符表中的关系运算符进行操作，可以是字符串或数字的比较，如$2>%1选择第二个字段比第一个字段长的行。
	‣ 模式匹配表达式：用运算符~(匹配)和~!(不匹配)。
	‣ 模式，模式：指定一个行的范围。该语法不能包括BEGIN和END模式。
	‣ BEGIN：让用户指定在第一条输入记录被处理之前所发生的动作，通常可在这里设置全局变量。
	‣ END：让用户在最后一条输入记录被读取之后发生的动作。

	∘ 操作
	‣ 操作由一人或多个命令、函数、表达式组成，之间由换行符或分号隔开，并位于大括号内。主要有四部份：
	‣ 变量或数组赋值
	‣ 输出命令
	‣ 内置函数
	‣ 控制流命令
	• ls -l | awk '/4c/ {print $1,$2,$8}'
	• echo "aaa bb|cc" | awk 'BEGIN {FS="[ \t|]";OFS="%"}{if($1~/aaa/){print $1,$2,$3}else{print $0" is not aaa!"}}'
	• echo "aaa bb|cc" | awk 'BEGIN {FS="[ \t|]";OFS="%"}{if($1~/aaa/){print $1OFS$2OFS$3}else{print $0" is not aaa!"}}'
	• echo "aaa bb|cc" | awk 'BEGIN {FS="[ \t|]";OFS="%"}{if($1~/aaa/){print NR,NF,$1,$NF}else{print $0" is not aaa!"}}'
	∘ 当前记录号、域数和每一行的第一个和最后一个域
	∘ 用运算符~(匹配)和~!(不匹配)
	• 变量名 含义
	∘ ARGC 命令行变元个数
	∘ ARGV 命令行变元数组
	∘ FILENAME 当前输入文件名
	∘ FNR 当前文件中的记录号
	∘ FS 输入域分隔符，默认为一个空格
	∘ RS 输入记录分隔符
	∘ NF 当前记录里域个数
	∘ NR 到目前为止记录数
	∘ OFS 输出域分隔符
	∘ ORS 输出记录分隔符

### 查看文件大小

	du -sh xxx



### ps
	ps -ef | grep -i 'php' | grep -v 'grep'

## SSH 公钥登录

	ssh-keygen -t rsa
	ssh-copy-id -i ~/.ssh/id_rsa.pub root@192.168.0.3
	ssh root@192.168.0.3


### 搜索

	locate 更新 sudo updatedb
	find / -name xxxx

### 软链接

	ln -s /mnt/hgfs/E/www /wwwroot

### 编译安装

	./configure
	make
	make install



### 添加用户组

	/usr/sbin/groupadd www
	/usr/sbin/useradd -g www www



### 变更为其它使用者的身份

	su root



### netstat使用

	netstat -lntp # 查看所有监听端口
	netstat -antp # 查看所有已经建立的连接



### 改变所属群组

	chgrp [ -R ] 群组名称档案或目录（chgrp root XXX ）
	[-R] 递归操作文件和目录
	改变档案拥有者：
	chown [ -R ] 账号名称 档案或目录 （chown root XXX）
	chown [ -R ] 账号名称:群组名称 档案或目录 （chown -R root:root XXX）
	[-R] 递归操作文件和目录
	改变档案权限：
	chmod [-R] xyz 档案或目录（chmod 770 XXX）
	[-R] 递归操作文件和目录
	可读 r:4、写 w:2、执行 x:1
	owner = rwx = 4+2+1 = 7
	group = rwx = 4+2+1 = 7
	others = --- = 0+0+0 = 0
	[4+2+1][4+2+1][0+0+0]=770



### vmware-tool自动选择默认

	./vmware-install.pl -d



### 查看编码
	locale



### 复制,删除

	cp -rf
	rm -rf
	
	
	
### 挂载光驱,卸载光驱

	mkdir -p /mnt/cdrom
	mount /dev/cdrom /mnt/cdrom
	umout /mnt/cdrom
	
	
	
### 关机,重启,注销

	shutdown -h now
	reboot
	logout



### 时间转换

	date -d'@1329893668' +'%Y-%m-%d %H:%M:%S' #秒数转时间:
	date -d'2011-10-10' +%s #时间转秒数



### find backup

	find . -type f -name "*.java" | xargs tar rvf myfile.tar



### rsync 同步

	-k, --copy-dirlinks transform symlink to a dir into referent dir
	-K, --keep-dirlinks treat symlinked dir on receiver as dir

	sudo rsync -zrptogv --delete --exclude=.buildpath --exclude=.project --exclude=.settings /home/bhuang/www/YII /home/bhuang/share/site

	OR

	sudo rsync -zrptogv --delete --exclude={.buildpath,.project,.settings} /home/bhuang/www/YII /home/bhuang/share/site
