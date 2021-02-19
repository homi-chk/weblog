# 实现zabbix邮件，企业微信告警


>邮件告警：

添加服务器
添加item
添加触发器
配置action（动作）
配置用户媒介


* 邮件监控报警流程：

       使用外部邮箱作为zabbix发送邮件邮箱：

       安装mailx并配置smtp服务器：

       vi /etc/mail.rc

       添加案例如下：

              set  from=11223344@qq.com          #qq注册的个人邮箱，用于zabbix服务端转发邮件到指定邮箱

              set  smtp=smtp.qq.com       #填写发送邮箱服务器地址smtp

              set  smtp-auth-user=11223344@qq.com      #收件人邮箱用户           

              set  smtp-auth-password=w****rfg*******h**d            #qq邮箱pop/smtp授权码（登录个人qq邮箱，账号设置中获取授权码）   

              set  smtp-auth=login                  #登录  

保存退出并进行测试：echo "zabbix报警事项"|mailx -v -s "zabbix" xxxxxx@qq.com               

以上操作ok,进行zabbix_web操作：

创建主机组
创建主机
创建监控项
创建报警媒介类型（端口465或587，新建好测试）:message templates部分：
 

主题：故障{TRIGGER.STATUS},服务器:{HOSTNAME1}发生: {TRIGGER.NAME}故障!

消息：

告警主机:{HOSTNAME1}

告警主机IP地址:{HOST.CONN}

告警时间:{EVENT.DATE} {EVENT.TIME}

告警等级:{TRIGGER.SEVERITY}

告警信息: {TRIGGER.NAME}

告警项目:{TRIGGER.KEY1}

问题详情:{ITEM.NAME}:{ITEM.VALUE}

当前状态:{TRIGGER.STATUS}:{ITEM.VALUE1}

事件ID:{EVENT.ID}

设置接收用户
进入动作选项，创建触发器
至此，邮件告警结束，进行测试

>微信告警


1.企业微信号：注册，配置 \
Corpid：wwf6ce6cc203abadf1 \
AgentId：1000002 \
Secret：qS7_RyoxGJOou37UmEDN6js56VOwcdgSZhSyp7gH3n4 \
用户账号：ChenHongKang \
2.zabbix_server配置：zabbix_server.conf \
vi zabbix_server.conf \
找到AlertScriptsPath并配置 \
例如： AlertScriptsPath=/usr/local/chen/zabbix/alertscripts \
为文件夹添加用户：\
chown -R zabbix:zabbix /usr/local/chen/zabbix/alertscripts 

3.下载python脚本 \
安装simple.json \
wget https://pypi.python.org/packages/f0/07/26b519e6ebb03c2a74989f7571e6ae6b82e9d7d81b8de6fcdbfc643c7b58/simplejson-3.8.2.tar.gz \
python setup.py build \
python setup.py install

下载wechat.py脚本
yum install git -y
git clone https://github.com/X-Mars/Zabbix-Alert-WeChat.git \
修改wechat.py脚本——自行查找
测试：http://qydev.weixin.qq.com/debug

安装模块：\
pip install requests \
需先安装以下：\
wget https://pypi.python.org/packages/source/s/setuptools/setuptools-12.0.3.tar.gz

python setup.py install

wget https://files.pythonhosted.org/packages/ca/1e/d91d7aae44d00cd5001957a1473e4e4b7d1d0f072d1af7c34b5899c9ccdf/pip-20.3.3.tar.gz \
解压并进入：\
      执行：python setup.py install

测试：\
/usr/local/chen/zabbix/alertscripts/wechat.py ChenHongKang zabbix_test "123456 from chen"
zabbix_server \
配置企业微信报警web端：\
添加报警媒介类型：\
名称：wechat \
类型：脚本 \
脚本名称：wechat.py \
脚本参数：\
      {ALERT.SENDTO} \
      {ALERT.SUBJECT} \
      {ALERT.MESSAGE} 

添加用户：wechat\
群组：Zabbix Adminstrators \
报警媒介类型：wechat \
收件人：chk \
权限：超级管理员

创建动作：
名称：80端口down报警

测试结束\
https://www.manageengine.cn/demo.html

Snmp服务：\
      团体名：\
      读写模式：\
      snmp版本：\
      服务IP：\
       代理IP

开启snmp的trap功能：
参考：\
       https://blog.csdn.net/liang_baikai/article/details/53522293 \
       https://www.runoob.com/w3cnote/zabbix-monitor-snmptrap.html



* 扩展 \
安装snmp：
      yum install -y net-snmp net-snmp-utils net-snmp-python

