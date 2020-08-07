Matlab调用Origin作图
=====================================

1.前期准备
~~~~~~~~~~

1.1 学生版申请
^^^^^^^^^^^^^^

目前Originlab对于盗版打击力度很大，会根据已经发表但没有正版许可的论文进行维权。因此特别建议在校学生注册学生版本。与专业版相比，在校注册版已经完全满足日常科研需求。
申请方法：https://my.originlab.com/forum/topic.asp?TOPIC_ID=22328 

1.2 环境搭建
^^^^^^^^^^^^^^
matlab是通过origin的com接口实现的。（同样道理，其他语言利用接口也可以实现各种功能）。origin的com接口介绍见：https://www.originlab.com/doc/COM

Matlab调用Origin的示例程序位于:..\Samples`:raw-latex:\COM `Server
and Client:raw-latex:`\MATLAB路径下`（以Origin
2015为例，其他版本的位置可能有所不同）。一共有两个m文件，CreatePlotInOrigin.m及MATLABCallOrigin.m，前者用于实现调用Origin绘图，并将结果保存到剪贴板中，后者演示了如何创建工作表(Worksheet)，如何插入新列等操作。另外一个CreatePlotInOrigin.opj文件是供CreatePlotInOrigin.m调用的一个Origin模板文件
。根据这两个案例，加上origin官方api，就可以开发出各式各样的脚本了。

**参考网址:**
   
- https://gaomf.cn/2016/01/28/Matlab%E8%B0%83%E7%94%A8Origin%E4%BD%9C%E5%9B%BE/
- Origin语法官网： https://www.originlab.com/doc/X-Function/ref/

2：导出图片案例
~~~~~~~~~~~~~~~~~~~~~

无法导出图片可能的原因： 

- 1.保存路径文件夹不存在（该程序不会在没有文件夹的情况下构建文件夹） 
- 2.origin中图片一定要是激活状态（即打开origin的时候，图片页面必须前置，否则无法输出）

::


   % mdata : 需要填充到Origin Worksheet中的数据
   % template : Origin模板函数名，不含后缀，需要保存在当前工作目录下，如'CreatePlotInOrigin'
   % fdir : 输出图片目标文件夹，如'D:\image'
   % fname : 输出图片文件名，不含后缀，如'abc'


   function OriginPlot_xia(mdata, template, fdir, fname)
   % Obtain Origin COM Server object
   % This will connect to an existing instance of Origin, or create a new one if none exist
   originObj=actxserver('Origin.ApplicationSI');
   % invoke(originObj, 'Execute', 'doc -mc 1;') %设置为可见！

   % Clear "dirty" flag in Origin to suppress prompt for saving current project
   invoke(originObj, 'IsModified', 'false');

   % Load the custom template project
   dir = pwd;
   dir = strcat(dir, '\', template, '.opj');
   invoke(originObj, 'Load', dir);

   % Send this data over to the Data1 worksheet
   invoke(originObj, 'PutWorksheet', 'Data1', mdata);

   % Save graph
   cmd = 'expGraph type:=jpg overwrite := rename tr1.unit := 2 tr1.width := 10000 path:= "';
   cmd = strcat(cmd, fdir, '" filename:= "', fname, '.emf";');
   invoke(originObj, 'Execute', cmd);
   % Release
   release(originObj);
   end

3.保存为工程文件opju案例
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

   invoke(originObj, 'Execute', 'pe_save fname:="F:\天津科技大学\论文发表\六月份主打论文\B4B投稿\历次返修\版本4\版本4.1\数据分析\版本2\mywork.opj "; ')