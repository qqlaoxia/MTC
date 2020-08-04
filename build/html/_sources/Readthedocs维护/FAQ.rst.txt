3.1 导入readthedocs常见问题
================================

1.1 官方网站
------------

-  https://www.sphinx-doc.org/en/master/usage/configuration.html?highlight=master_doc
-  https://docs.readthedocs.io/en/stable/config-file/v2.html#sphinx

1.2 主文件夹中需要添加一个readthedocs.yml文件
---------------------------------------------

可以如下添加：

::

   version: 2

   sphinx:
     builder: html
     configuration: source/conf.py

参考网址：https://docs.readthedocs.io/en/stable/config-file/v2.html

1.3 在配置过程中，出现WARNING: html_static_path 警告而导致失败
--------------------------------------------------------------

解决方案：将con.py文件中的

::

   html_static_path = ['_static']

改为

::

   html_static_path = []

参考网址：https://github.com/readthedocs/readthedocs.org/issues/1776

1.4配制文件模板
---------------

本网站文件内容：

::

   # Configuration file for the Sphinx documentation builder.
   #
   # This file only contains a selection of the most common options. For a full
   # list see the documentation:
   # https://www.sphinx-doc.org/en/master/usage/configuration.html

   # -- Path setup --------------------------------------------------------------

   # If extensions (or modules to document with autodoc) are in another directory,
   # add these directories to sys.path here. If the directory is relative to the
   # documentation root, use os.path.abspath to make it absolute, like shown here.
   #
   # import os
   # import sys
   # sys.path.insert(0, os.path.abspath('.'))


   # -- Project information -----------------------------------------------------

   project = 'MTC'
   copyright = '2020, MTC Team'
   author = 'MTC Team'

   # The full version, including alpha/beta/rc tags
   release = '1.0'


   # -- General configuration ---------------------------------------------------

   # Add any Sphinx extension module names here, as strings. They can be
   # extensions coming with Sphinx (named 'sphinx.ext.*') or your custom
   # ones.
   extensions = [
   ]

   # Add any paths that contain templates here, relative to this directory.
   templates_path = ['_templates']

   # List of patterns, relative to source directory, that match files and
   # directories to ignore when looking for source files.
   # This pattern also affects html_static_path and html_extra_path.
   exclude_patterns = []
   master_doc = 'index'


   # -- Options for HTML output -------------------------------------------------

   # The theme to use for HTML and HTML Help pages.  See the documentation for
   # a list of builtin themes.
   #
   html_theme = 'sphinx_rtd_theme'

   # Add any paths that contain custom static files (such as style sheets) here,
   # relative to this directory. They are copied after the builtin static files,
   # so a file named "default.css" will overwrite the builtin "default.css".
   html_static_path = []

   from recommonmark.parser import CommonMarkParser
   source_parsers = {
       '.md': CommonMarkParser,
   }
   source_suffix = ['.rst', '.md']
   html_search_language = 'zh'

**官网给出的一个典型con.py文件：**
https://www.sphinx-doc.org/en/master/usage/configuration.html?highlight=master_doc