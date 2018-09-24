###Package Control
##插件管理器
	1)在Sublime中打开View –> Show Console，将以下代码复制到输入框中后按回车键
	import urllib.request,os;pf=’Package Control.sublime-package’;ipp=sublime.installed_packages_path();urllib.request.install_opener(urllib.request.build_opener(urllib.request.ProxyHandler()));open(os.path.join(ipp,pf),’wb’).write(urllib.request.urlopen(‘http://sublime.wbond.net/‘+pf.replace(’ ‘,’%20’)).read())
	2)验证是否安装成功
	打开Preferences –> Package Control，如果能看到此菜单，则表示安装成功

##sublime相关实用插件的安装
#一、DocBlockr :
	作用：注释插件
		setting-user配置
		{
		    "jsdocs_extra_tags":["@Author	Crazy、Ly","@DateTime {{datetime}}"]
		}

#二、sublimeLinter 与 sublimeLiinter-php：
	作用：语法错误提示
		setter-user配置
		复制一份默认的配置文件到user，然后将path中的地址指向php.exe即可

#三、CodeFormatter：
	作用：格式化代码
	快捷键：ctrl+alt+f

#四、CodeInter:
	作用：代码自动补全
	配置：修改path中php路径的指向地址即可

#五、MarkDown 编辑+实时预览
	MarkdownEditing 编辑插件
	配置：
		进入 Preferences -> Package Settings -> Markdown Editting ->  Markdow GFM Settings - Default & Markdow GFM Settings - User ，将 Markdow GFM Settings - Default 中的内容拷贝至 Markdow GFM Settings - User 并保存，然后修改如下内容：
		1. 修改主题：
		修改 "color_scheme": 所在行为你喜欢的主题，笔者sublime默认主题为Monokai，这里修改如下，那个默认灰白色的主题就是第一个。
		    //"color_scheme": "Packages/MarkdownEditing/MarkdownEditor.tmTheme",
		    // "color_scheme": "Packages/MarkdownEditing/MarkdownEditor-Dark.tmTheme",
		    // "color_scheme": "Packages/MarkdownEditing/MarkdownEditor-Yellow.tmTheme",
		        "color_scheme": "Packages/Color Scheme - Default/Monokai.tmTheme",
		2. 去除空白：
		    // Layout
		    "draw_centered": false,  //决定两侧是否留白，默认为true，修改为false去除左侧空白
		    "word_wrap": true,
		    "wrap_width": 120, //决定每行最大字数，这里设定为120
		    "rulers": [],
		3. 显示行号：
		    // Line
		    "line_numbers": true, //显示行号，默认为false
		    "highlight_line": false,
		    "line_padding_top": 2,
		    "line_padding_bottom": 2,

	oMniMarkupPreviewer 实时预览  （setting {"mathjax_enabled":true}）安装完成后可以crtl+alt+O在浏览器实时预览
	补充插件 Monokai Extended & Markdown Extended  主题插件
	补充插件 MarkdownTOC 一键生成目录 (setting {"default_autolink":true,#目录以链接形式呈现 "default_barcket":"round",#目录以链接形式呈现 "default_depth":0 #无限目录深度})
	补充插件 Table Editor
	作用 :MarkDown 编辑+实时预览
	配置 ：


##注意


#其他插件安装
	参考：https://blog.csdn.net/zbwroom/article/details/72473851
#问题1、安装完成插件后系统报错
		sublime error loading syntax file
	解决方案
		找到AppData\Roaming\Sublime Text3\Local ，删除里面的两个文件
		Session.sublime_session、以及Auto Save Session.sublime_session 重新打开编辑器即可

#问题二、sublime text 有个bug 那就是不支持中午的鼠标跟随（输入法不能显示在光标的下方）
	解决方案
		安装IMESupport插件即可

