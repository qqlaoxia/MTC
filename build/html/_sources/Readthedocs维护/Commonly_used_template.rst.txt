Readthedocs常用模板
============================================

字体设置
------------

-  单星号： *text* 强调 (斜体),
-  双星号： **text** - 重点强调 (粗体)，以及 反引号： ``text``
   代码示例。

**说明**\ ：强调的字体必须与前后字有一个空格

细节设置
------------

外部链接：
~~~~~~~~~~~~~~~~

::

   .. _a link: http://example.com/

插入图片
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

插入代码
~~~~~~~~~~~~~~

::

   .. code:: python

     def my_function():
         "just a test"
         print 8/2

插入数学公式
~~~~~~~~~~~~~~~~~~

::

   .. math::

     α_t(i) = P(O_1, O_2, … O_t, q_t = S_i λ)

插入引文
~~~~~~~~~~~~~~

::

   Lorem ipsum [Ref]_ dolor sit amet.

   .. [Ref] Book or article reference, URL or whatever.

插入视频
~~~~~~~~~~~~~~

**常用模板**

::

   .. raw:: html

       <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
           <iframe src="https://player.bilibili.com/player.html?aid=329031250&bvid=BV1MA411Y7EB&cid=217805774&page=1&high_quality=1&danmaku=0" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
       </div>

文章结构和目录
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
	  

兼容Jupyter Notebook
--------------------------
可以参考官网：https://nbsphinx.readthedocs.io/en/guzzle-theme/

列表
--------------------------
以下为1级标题和2级标题

::

   - 符号列表1
   - 符号列表2

     + 二级符号列表1

     - 二级符号列表2

     * 二级符号列表3

   * 符号列表3

   + 符号列表4

枚举
--------------------------
以下分别用1,2.. (I),(II)...和A),B)...自动编号

::

   1. 枚举列表1
   #. 枚举列表2
   #. 枚举列表3

   (I) 枚举列表1
   (#) 枚举列表2
   (#) 枚举列表3

   A) 枚举列表1
   #) 枚举列表2
   #) 枚举列表3

编号技巧
--------------------------

**需要注意的是：一般只有最高级的toctree中设定numered选项，其他的index和正文均不需要设置为numered或者添加序列号。论文中会自动编号。** 

链接到当地文件
--------------------------

::

   .. raw:: html
   
      <li class="toctree-l1"><a class="reference internal" href="For Read/菌群.html">6. 菌群</a></li>

链接到阿里云服务器
--------------------------

::

   .. raw:: html

   
      <video width="100%" height="100%" controls>
      <source src="https://mtc123.oss-cn-beijing.aliyuncs.com/biopharmacy/tt.mp4" type="video/mp4" />
      </video>
	  

段落两端对齐
--------------------------

::

   .. raw:: html

   
       <p style="text-align:justify; text-justify:inter-ideograph;">文字，需要对齐的文字段落。</p>