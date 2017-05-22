# upsource
官方安装部署文档
https://www.jetbrains.com/help/upsource/2017.1/zip-installation.html



1、安装前环境配置

编辑 /etc/security/limits.conf 文件，添加如下内容：
* - memlock unlimited
* - nofile 100000
* - nproc 32768
* - as unlimited
2、下载安装包

官方下载地址：下载地址
3、安装

解压下载的zip安装包，运行如下命令：
<upsource_home>/bin/upsource.sh start
4、配置

4.1、配置验证模式。进入HUB，进入配置→Auth Modules页，设置基于Jira的验证方式。

 

使用说明：http://wiki.rd.chanjet.com/pages/viewpage.action?pageId=76678120
backup:

 
1
2
3
4
	
cp -rf ${install_dir}/upsource-3.5.3597/data ${backup_dir}/
cp -rf ${install_dir}/upsource-3.5.3597/conf ${backup_dir}/
tar czf upsource.bak ${backup_dir}/
rsync -a upsource.bak ${bak_server}::upsource/${DAY}/

 
restore:

 
1
2
3
4
5
6
7
8
	
rsync -a ${bak_server}::upsource/${DAY}/ upsource.bak
mkdir back_tmp && cd back_tmp && tar xvzf ../upsource.bak && cd -
cp upsource-3.5.3597.zip ./
unzip upsource-3.5.3597.zip
cd upsource-3.5.3597
cp -rf back_tmp/data ./
cp -rf back_tmp/conf ./
./bin/upsource.sh configure --base-url http://${server_ip}:8081

 

 
reference:


https://www.jetbrains.com/help/upsource/2017.1/backing-up-and-restoring-data.html
https://www.jetbrains.com/help/upsource/2017.1/moving-your-upsource-installation-to-another-server.html
