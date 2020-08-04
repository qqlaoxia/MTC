2.1 利用matlab实现word中文字自动替换
================================================================

    本程序记录了2020年学院工程认证中，附件材料替换的小程序。由于比较简单，不做详细解释，仅留作记录，供未来工作中参考。

1. 附录编号自动提取
~~~~~~~~~~~~~~~~~~~

::

    附录编号提取2
    data2={};
    Num=0;
    for i =1:length(data)
        expression ='[0-9]-[0-9]-[0-9]{1,2}'
        matchStr = regexp(data{i,1},expression,'match')
        if length(matchStr) > 0
            Num=Num+1;
            data2{Num,1}=matchStr{1};
            
        end
    end

    data=data2;

2. 含多附录编号的快速提取
~~~~~~~~~~~~~~~~~~~~~~~~~

::

    data2={};
    Num=0;
    for i =1:length(data)
        expression ='[0-9]-[0-9]-[0-9]{1,2}'
        matchStr = regexp(data{i,1},expression,'match')
        if length(matchStr) > 1
            Num=Num+1
           for jj=1:length(matchStr)
               data2{Num,jj}=matchStr{jj};
           end
           end
    end

    data=data2;

3.添加括号
~~~~~~~~~~

::

    加括号
    data=cellfun(@black_add,data)


    function [x] = black_add(x)
    %BLACK_ADD 此处显示有关此函数的摘要
    %   此处显示详细说明
    if x ~=0
        x=[x,'）'];
    else
        x=x;
    end
    end

4.利用冒泡法合并求解元素集合
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    %元素去重--方法3
    %将data转化为字符串数组--非常关键
    data=cellfun(@string,data,'UniformOutput',false);
    data2={};
    for i =1:size(data,1)
        data2{i}=[data{i,1},data{i,2}];
    end


    % for i=length(data2):-1:2
    %     cont1=data2{i};
    %     de=false
    %    for jj=i-1:-1:1
    %        if ~isempty(intersect(cont1,data2{jj}))
    %            data2{jj}=union(cont1,data2{jj})
    %            de=true
    %        end
    %    end  
    %    if de==true
    %    data2(i)=[];
    %    end
    % end

    for i=1:10
        data2 = Union_xia(data2);
    end

    save xia.mat data2

    for i=1:length(data2)
        xlswrite('xia2.xlsx',data2{i},'Sheet1',['A',num2str(i)]);
    end

4.word中内容替换（核心）
~~~~~~~~~~~~~~~~~~~~~~~~

::

    tic
    w=actxserver('Word.Application');
    w.Visible = 0;
    w.DisplayAlerts = 0;
    doc = w.Documents.Open('F:\天津科技大学\日常工作\2020\1月份\工程认证\最终材料\2020-7-29 版本\报告正文\自评报告正文-20200729--夏梦雷修订.docx');
    w.Selection.Find.ClearFormatting();
    w.Selection.Find.Replacement.ClearFormatting();
    for i=1:size(data,1)
        for jj=2:5
            if data{i,jj} ~=0
            w.Selection.Find.Execute(data{i,jj}, false, false, false, false, false, true, 1, true, data{i,1}, 2);
            disp(sprintf('%s→%s：替换完毕',data{i,jj},data{i,1}))
            end
        end
    end
    doc.SaveAs2('F:\天津科技大学\日常工作\2020\1月份\工程认证\最终材料\2020-7-29 版本\报告正文\自评报告正文-20200729--夏梦雷修订.docx');
    doc.Close();
    w.Quit();
    toc

5.编号自动排列
~~~~~~~~~~~~~~

::

    % 确保第一项是从1开始的
    cont1=data{1};
    po1=strfind(cont1,'-');
    if strcmp(cont1(po1(2)+1:end),'1')
        data{1}=[cont1(1:po1(2)),'1'];
    end

    Num=1
    for i =2:length(data)
        cont1=data{i-1};
        cont2=data{i};
        po1=strfind(cont1,'-');
        po2=strfind(cont2,'-');
        
        if strcmp(cont1(1:po1(2)),cont2(1:po2(2)))
            Num=Num+1;
        else
            Num=1;
        end
         data{i}=[cont2(1:po2(2)),num2str(Num)]
    end

