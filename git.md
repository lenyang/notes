git仓库


gitbook的使用

##注意
#1、
问题：
	remote HTTP Basic:Access dneied
	fatal:Authentication failed for "https://...."
原因：
	因为重置了密码或者密码错误导致git远程操作失败
解决：
	输入一行命令删除掉原来输入过的密码
	git config --system --unset credential.helper