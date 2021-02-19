## 戴尔NVIDIA显卡驱动安装

参考：http://www.360doc.com/content/14/1217/20/5470123_433706475.shtml

>可选安装：
* yum install epel-release
* yum install kernel
* yum install kernel-headers

> 可选依赖安装：

      yum -y install gcc gcc-c++ autoconf libjpeg 
      libjpeg-devel libpng libpng-devel freetype 
      freetype-devel libxml2 libxml2-devel zlib zlib-devel glibc 
      glibc-devel glib2 glib2-devel bzip2 bzip2-devel ncurses ncurses-devel 
      curl-devel e2fsprogs e2fsprogs-devel krb5 krb5-devel libidn libidn-devel 
      openssl openssl-devel openldap openldap-devel nss_ldap openldap-clients openldap-servers


> 安装nvidia操作流程：

* 第一步：

nouveau禁用：

查看nouveau状态：

lsmod | grep nouveau

若返回结果，则未禁用；没有返回结果，则已禁用

若未禁用，则按以下流程操作：

1.编辑: vi /etc/modprobe.d/blacklist.conf

  添加内容：
  blacklist nouveau
  options nouveau modeset=0

2.备份原有的initramfs nouveau image镜像：
mv /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r)-nouveau.img  

3.创建新的initramfs image镜像
dracut /boot/initramfs-$(uname -r).img $(uname -r) 

执行reboot重启

再次查看nouveau状态：
lsmod | grep nouveau

若无结果返回即已禁用

第二步：

安装nvidia驱动：

赋权：
chmod +x NVIDIA.xxx.xx.run

执行：
./NVIDIA.xxx.xx.run --kernel-source-path=/usr/src/kernels/内核号

内核号获取：tab+2

完成操作后，查看
nvidia-smi

至此nvidia驱动安装结束




