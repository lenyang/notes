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

##sublime的快捷键
>选择类
>>Ctrl+D 选中光标所占的文本，继续操作则会选中下一个相同的文本。

>>Alt+F3 选中文本按下快捷键，即可一次性选择全部的相同文本进行同时编辑。举个栗子：快速选中并更改所有相同的变量名、函数名等。

>>Ctrl+L 选中整行，继续操作则继续选择下一行，效果和 Shift+↓ 效果一样。

>>Ctrl+Shift+L 先选中多行，再按下快捷键，会在每行行尾插入光标，即可同时编辑这些行。


>>Ctrl+Shift+M 选择括号内的内容（继续选择父括号）。举个栗子：快速选中删除函数中的代码，重写函数体代码或重写括号内里的内容。

>>Ctrl+M 光标移动至括号内结束或开始的位置。

>>Ctrl+Enter 在下一行插入新行。举个栗子：即使光标不在行尾，也能快速向下插入一行。

>>Ctrl+Shift+Enter 在上一行插入新行。举个栗子：即使光标不在行首，也能快速向上插入一行。

>>Ctrl+Shift+[ 选中代码，按下快捷键，折叠代码。

>>Ctrl+Shift+] 选中代码，按下快捷键，展开代码。

>>Ctrl+K+0 展开所有折叠代码。

>>Ctrl+← 向左单位性地移动光标，快速移动光标。

>>Ctrl+→ 向右单位性地移动光标，快速移动光标。

>>shift+↑ 向上选中多行。

>>Shift+→ 向右选中文本。

>>Ctrl+Shift+← 向左单位性地选中文本。

>>Ctrl+Shift+→ 向右单位性地选中文本。

>>Ctrl+Shift+↑ 将光标所在行和上一行代码互换（将光标所在行插入到上一行之前）。

>>Ctrl+Shift+↓ 将光标所在行和下一行代码互换（将光标所在行插入到下一行之后）。

>>Ctrl+Alt+↑ 向上添加多行光标，可同时编辑多行。

>>Ctrl+Alt+↓ 向下添加多行光标，可同时编辑多行。

>编辑类

>>Ctrl+J 合并选中的多行代码为一行。举个栗子：将多行格式的CSS属性合并为一行。

>>Ctrl+Shift+D 复制光标所在整行，插入到下一行。

>>Tab 向右缩进。

>>Shift+Tab 向左缩进。

>>Ctrl+K+K 从光标处开始删除代码至行尾。

>>Ctrl+Shift+K 删除整行。

>>Ctrl+/ 注释单行。

>>Ctrl+Shift+/ 注释多行。

>>Ctrl+K+U 转换大写。

>>Ctrl+K+L 转换小写。

>>Ctrl+Z 撤销。

>>Ctrl+Y 恢复撤销。

>>Ctrl+U 软撤销，感觉和 Gtrl+Z 一样。

>>Ctrl+F2 设置书签

>>Ctrl+T 左右字母互换。

>>F6 单词检测拼写

>搜索类

>>Ctrl+F 打开底部搜索框，查找关键字。

>>Ctrl+shift+F 在文件夹内查找，与普通编辑器不同的地方是sublime允许添加多个文件夹进行查找，略高端，未研究。

>>Ctrl+P 打开搜索框。举个栗子：1、输入当前项目中的文件名，快速搜索文件，2、输入@和关键字，查找文件中函数名，3、输入：和数字，跳转到文件中该行代码，4、输入#和关键字，查找变量名。

>>Ctrl+G 打开搜索框，自动带：，输入数字跳转到该行代码。举个栗子：在页面代码比较长的文件中快速定位。

>>Ctrl+R 打开搜索框，自动带@，输入关键字，查找文件中的函数名。举个栗子：在函数较多的页面快速查找某个函数。

>>Ctrl+： 打开搜索框，自动带#，输入关键字，查找文件中的变量名、属性名等。

>>Ctrl+Shift+P 打开命令框。场景栗子：打开命名框，输入关键字，调用sublime text或插件的功能，例如使用package安装插件。
Esc 退出光标多行选择，退出搜索框，命令框等。

>显示类

>>Ctrl+Tab 按文件浏览过的顺序，切换当前窗口的标签页。

>>Ctrl+PageDown 向左切换当前窗口的标签页。

>>Ctrl+PageUp 向右切换当前窗口的标签页。

>>Alt+Shift+1 窗口分屏，恢复默认1屏（非小键盘的数字）

>>Alt+Shift+2 左右分屏-2列

>>Alt+Shift+3 左右分屏-3列

>>Alt+Shift+4 左右分屏-4列

>>Alt+Shift+5 等分4屏

>>Alt+Shift+8 垂直分屏-2屏

>>Alt+Shift+9 垂直分屏-3屏

>>Ctrl+K+B 开启/关闭侧边栏。

>>F11 全屏模式

>>Shift+F11 免打扰模式


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

