Package Control
插件管理器

1)在Sublime中打开View –> Show Console，将以下代码复制到输入框中后按回车键
import urllib.request,os;pf=’Package Control.sublime-package’;ipp=sublime.installed_packages_path();urllib.request.install_opener(urllib.request.build_opener(urllib.request.ProxyHandler()));open(os.path.join(ipp,pf),’wb’).write(urllib.request.urlopen(‘http://sublime.wbond.net/‘+pf.replace(’ ‘,’%20’)).read())
2)验证是否安装成功
打开Preferences –> Package Control，如果能看到此菜单，则表示安装成功

sublime相关实用插件的安装
DocBlockr :
	作用：注释插件
		setting-user配置
		{
		    "jsdocs_extra_tags":["@Author	Crazy、Ly","@DateTime {{datetime}}"]
		}

sublimeLinter：
	作用：语法错误提示
		setter-user配置
		复制一份默认的配置文件到user，然后将path中的地址指向php.exe即可

CodeFormatter：
	作用：格式化代码
	快捷键：ctrl+alt+f

CodeInter:
	作用：代码自动补全
	配置：修改path中php路径的指向地址即可

MarkDown 编辑+实时预览
	作用 :MarkDown 编辑+实时预览
	配置 ：

其他插件安装
	参考：https://blog.csdn.net/zbwroom/article/details/72473851

