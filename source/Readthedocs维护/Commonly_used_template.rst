3.4 Readthedocs常用模板
============================================

1.1 字体设置
------------

-  单星号： *text* 强调 (斜体),
-  双星号： **text** - 重点强调 (粗体)，以及 反引号： ``text``
   代码示例。

**说明**\ ：强调的字体必须与前后字有一个空格

1.2 细节设置
------------

1.2.1 外部链接：
~~~~~~~~~~~~~~~~

::

   .. _a link: http://example.com/

1.2.2 插入图片
~~~~~~~~~~~~~~

-  插入Image

::

   .. image:: picture.jpeg
      :height: 100px
      :width: 200 px
      :scale: 50 %
      :alt: alternate text
      :align: right

**说明**\ ：排列方式包括“top”, “middle”, “bottom”, “left”, “center”, or
“right”

-  插入Fighre

::

   .. figure:: picture.png
      :scale: 50 %
      :alt: map to buried treasure

1.2.3 插入代码
~~~~~~~~~~~~~~

::

   .. code:: python

     def my_function():
         "just a test"
         print 8/2

1.2.4 插入数学公式
~~~~~~~~~~~~~~~~~~

::

   .. math::

     α_t(i) = P(O_1, O_2, … O_t, q_t = S_i λ)

1.2.5 插入引文
~~~~~~~~~~~~~~

::

   Lorem ipsum [Ref]_ dolor sit amet.

   .. [Ref] Book or article reference, URL or whatever.

1.2.6 插入视频
~~~~~~~~~~~~~~

**常用模板**

::

   .. raw:: html

       <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
           <iframe src="https://player.bilibili.com/player.html?aid=329031250&bvid=BV1MA411Y7EB&cid=217805774&page=1&high_quality=1&danmaku=0" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
       </div>

1.3 文章结构和目录
------------------

文章结构和目录由toctree实现。常见参数设定如下：

+-------------------+-------------------------------------------------+
| 参数              | 含义                                            |
+===================+=================================================+
| :maxdepth:        | 树的深度                                        |
+-------------------+-------------------------------------------------+
| All about strings | 由自定义的All about                             |
|                   | string作为题                                    |
|                   | 目，代替默认的string作为题目。本设定为题目设定  |
+-------------------+-------------------------------------------------+
| :numbered:        | 给题目自动编号                                  |
+-------------------+-------------------------------------------------+
| :titlesonly:      | 仅仅显示指定的题目                              |
+-------------------+-------------------------------------------------+
| :global:          | 自动匹配题目，并按照字母顺序排列                |
+-------------------+-------------------------------------------------+

具体的案例如下 - 常规

::

   .. toctree::
      :maxdepth: 2

      intro
      strings
      datatypes
      numeric
      (many more documents listed here)

-  手动指明题目

::

   .. toctree::

      intro
      All about strings <strings>
      datatypes

-  章节编号

::

   .. toctree::
      :numbered:

      foo
      bar

-  附加选项

::

   .. toctree::
      :titlesonly:

      foo
      bar

-  自动匹配

::

   .. toctree::
      :glob:

      intro*
      recipe/*
      *

-  隐藏选项

::

   .. toctree::
      :hidden:

      doc_1
      doc_2
	  

1.4 兼容Jupyter Notebook
--------------------------
可以参考官网：https://nbsphinx.readthedocs.io/en/guzzle-theme/