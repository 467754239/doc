# doc

## 上传本地ami到aws
```
1. 利用VMware Workstation 导出 ovf 或ova.(windows系统操作)
2. 命令上传.(AWS任意一台ec2上操作)


C:\Program Files (x86)\VMware\VMware Workstation\OVFTool>"C:\Program Files (x86)\VMware\VMware Workstation\OVFTool\ovftool.exe" "D:\vm\virtual machines\CentOS 64 位.vmx" D:\vm\Centos7.3.ovf
Opening VMX source: D:\vm\virtual machines\CentOS 64 位.vmx
Opening OVF target: D:\vm\Centos7.3.ovf
Writing OVF package: D:\vm\Centos7.3.ovf
Transfer Completed
Completed successfully


中区(无需手动上传s3)
ec2-import-instance ./AMI-centos7-disk1.vmdk -f vmdk -t m3.xlarge -a x86_64 -b agent -o AKIxxxxx -w A1Hxxx  -O AKIxxx -W A1Hxxx --region cn-north-1 --subnet subnet-8f378eea  -p linux

美区(需要手动上传s3)
aws ec2 import-image --cli-input-json "{  \"Description\": \"linux\", \"DiskContainers\": [ { \"Description\": \"First CLI task\", \"Format\": \"ova\",\"UserBucket\": { \"S3Bucket\": \"sengled-ami\", \"S3Key\" : \"AMI-platform.ova\" } } ]}" --platform linux

问题
使用vmimport上传过一个镜像，后来上传终止了，但是产生的实例i-0cf0ebb63e9fa4300 终止不了。
1. 如果您是通过ec2-import-instance 命令导入的实例，可以使用以下方式取消：
使用aws ec2 describe-conversion-tasks 列出所有导入过的实例任务；
然后使用aws ec2 cancel-conversion-task --conversion-task-id import-i-fg0hd3oy，取消这个导入任务。

2. 如果是使用aws ec2 import-image 命令导入的镜像，可以使用以下方式取消：
使用aws ec2 describe-import-image-tasks 列出所有的导入镜像任务；
然后使用aws ec2 cancel-import-task --import-task-id import-ami-abcd1234，取消这个导入任务。
``` 
![Alt text](/images/upload_ami.png)


## CentOS 7.x rc.local服务
```
systemctl status | start | enable | stop rc-local.service
/etc/rc.local 不等于 /etc/rc.d/rc.local

rc.local服务可参考
https://www.centos.org/forums/viewtopic.php?t=52660
```


## vim支持golang语法高亮
```

```

## django ajax跨域
```
#proxy_set_header   Access-Control-Allow-Method "POST,GET";
add_header   'Access-Control-Allow-Origin' '*';
```
