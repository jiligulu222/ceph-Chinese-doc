====
编译
====

编译环境的配置比较麻烦，您不想折腾的话可以直接读编译好的。编译好的\
文档位于：

https://github.com/drunkard/ceph-readable-doc/tree/master/output/html

Java 虚拟机应该用 oracle-jdk-bin-1.8 或 oracle-jdk-bin-1.7 ， jre \
缺少必要的库文件。


问题
====

#. 编译系统是基于 python2 的，还不支持 python3 ，会遇到语法错误。在 \
   Gentoo/Funtoo 下如果环境不对，可以这样临时地切换到 python2.7 ： ::

	eselect python set python2.7
	ln -sf /usr/bin/python2.7 /usr/bin/python

#. ditaa 图还不能翻译为中文，因为渲染时的字体问题还未解决；


编译步骤
========

这些文档从 ceph 源码中的 doc/ 目录翻译而来，结构未变，所以您仍然可\
以用原文档的构建方法构建此文档。只需用此库的 ceph-doc 目录替换 ceph \
库的 doc 目录，具体步骤如下：

#. 你得克隆本文档库，并克隆 Ceph 源码，如： ::

	mkdir /git && cd /git
	git clone https://github.com/ceph/ceph.git
	git clone https://github.com/drunkard/ceph-Chinese-doc.git

#. 把源码树里的 doc 目录备份为 doc-en，然后把中文文档库的 \
   ceph-Chinese-doc 目录链接为原 ceph 源码库的 doc ； ::

	cd /git
	ln -s /git/ceph-Chinese-doc /git/ceph/doc

#. 执行 ceph 库内 admin 目录下的 build-doc 开始构建文档； ::

	cd /git/ceph
	./admin/build-doc

#. 启动文档服务器，这样就可以通过 http://localhost:8080/ 阅读文档了。 ::

	cd /git/ceph
	./admin/serve-doc


========
文档风格
========

本项目的更新是对照着 Ceph 项目原文和 doc/ 目录相关的 commit 历史进\
行的，这样就无需挨篇对照。

仍然要尽量遵守原文档的书写风格，如缩进、不超过 80 列宽、等。

有些风格是中文版特有的，如：

- 中文和非中文用空格分隔；
- 插入命令，前一段行尾加空格和双引号（" ::"）；
- 引用和正文间要加反斜线和空格，如（"\\ "），这样既不影响编译又不会额外增加空格；
- 用反斜线（"\\"）换行，这样不会额外增加空格；
- 原文中用双引号引用的词语在中文文档里可去掉引号，因为原文引用它已\
  经很显眼了；
- 由于字体和程序的问题，在"终端下”能更好地对齐到 80 列，比如在 \
  gnome-terminal + vim 下；
- 为防止中文版和英文版文档的行数差得太多，不利于后续更新，中文版断\
  行要提前，比如在 66 列左右断行；


========
更新步骤
========

以下只是大致步骤，路径不同时还需修改脚本： ::

	mkdir /git && cd /git
	git clone https://github.com/ceph/ceph.git
	git clone https://github.com/{你的github用户名}/ceph-Chinese-doc.git
	cd /git/ceph-Chinese-doc/ && ./update-doc.sh
	# update-doc.sh 脚本用了 git 和 gitview 命令，最好先检查下\
	# 安装了没。
	# 对照着 gitview 里的 commit 历史开始更新中文文档！
	# 从最下面的 commit 开始翻译！！！

	# 更新一或多个 commit 后提交到 git 库：
	./commit-updated.sh
	git push origin
	vi update-doc.sh	# 更新 CUR 变量

然后可以在 github 上向我反馈您的更新 :-)
