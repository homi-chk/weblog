## Docker安装卸载

>docker-install-delete

* Docker安装：

参考：https://www.liangzl.com/get-article-detail-39839.html

* 安装所需的软件包
      yum install -y yum-utils \
  	device-mapper-persistent-data \
  	lvm2

* 设置稳定的仓库
      yum-config-manager \
        --add-repo \
   	 https://download.docker.com/linux/centos/docker-ce.repo

* 安装 Docker Engine-Community

      yum install docker-ce docker-ce-cli containerd.io

* 启动docker服务

      systemctl start docker

* 设置docker开机自启动

      systemctl enable docker

  安装结束

* 配置daemon.json文件：

  范例：
      #vi /etc/docker/daemon.json
      {"registry-mirrors": 
      ["https://registry.docker-cn.com",
		       "https://kxv08zer.mirror.aliyuncs.com",
		       "https://123abc.mirror.aliyuncs.com"],
        	"insecure-registries": ["10.0.11.44"]}

保存退出

* 重新加载：
      systemctl daemon-reload

* Docker卸载：
        yum list installed | grep docker   //查看版本，查出来的全部删除（推荐）\
        yum -y remove xxxx	//执行删除

* 删除存储目录：
        rm -rf /etc/docker\
        rm -rf /run/docker\
        rm -rf /var/lib/dockershim\
        rm -rf /var/lib/docker

* 卸载旧版本：
       yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine

