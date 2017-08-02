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
![Alt text](/images/upload_ami.png)

美区(需要手动上传s3)
aws ec2 import-image --cli-input-json "{  \"Description\": \"linux\", \"DiskContainers\": [ { \"Description\": \"First CLI task\", \"Format\": \"ova\",\"UserBucket\": { \"S3Bucket\": \"sengled-ami\", \"S3Key\" : \"AMI-platform.ova\" } } ]}" --platform linux
``` 
