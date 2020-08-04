Primer_blast算法实现
--------------------

1. 16s核糖体序列检测
~~~~~~~~~~~~~~~~~~~~

具体的信息为:27f 1492r

======== ========================
序列名称 序列内容
======== ========================
前引物链 ‘AGAGTTTGATCCTGGCTCAG’
后引物链 ‘TACGGCTACCTTGTTACGACTT’
======== ========================

..

   本程序实现了ncbi中primer_blast的核心功能

::

   function [Right_result,Wrong_result]=primer_blast_xia(seq,a,b)
   % 本函数实现了NCBI中primer_blast的功能
   %
   % seq为序列，a为前引物，b为后引物
   %
   % Right_result为正确的序列，Wrong_result为包含所有的可能组合（假想的，错误的序列几乎不太会在真实试验中出现）
   %
   % Copywrite: MTC, 2020.7,Version 1.0, Written by Ray
   %
   % see also: seqrcomplement, strfind, seqcomplement

   b1=seqrcomplement(b);
   po1=strfind(seq,a);
   po2=strfind(seq,b1);
   % 一般情况下，两者是一一对应的，为了考虑极端情况，我们做个循环处理
   Right_result=[];
   Wrong_result=[];

   for i=1:length(po1)
     po_temp=min(po2(po2>po1(i)));
     Right_result=[Right_result;po1(i), po_temp+length(b1)-1];
   end

   for i=1:length(po1)
     po_temp=po2(po2>po1(i));
     for jj=1:length(po_temp)
         Wrong_result=[Wrong_result;po1(1),po_temp(jj)+length(b1)-1];
     end
   end
   end

2.利用efetch自动下载ncbi上的核酸序列
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

   利用efetch函数，实现了ncbi上基因数据的自动下载
   https://www.ncbi.nlm.nih.gov/books/NBK25501/ NCBI上关于API的介绍

::

   function fasta_download(ID)
   url_base='https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nucleotide&id=%s&rettype=fasta&retmode=text';
   url=sprintf(url_base,ID);
   websave([ID,'.fasta'],url);
   end

3. 自动下载序列并检测结果
~~~~~~~~~~~~~~~~~~~~~~~~~

==== ===========
序列 基因号
==== ===========
1    NR_074511.2
2    KC166235.1
3    AB675522.1
4    AB675515.1
5    CP002660.1
6    CP002118.1
7    NR_113246.1
8    AE001437.1
9    AM231184.1
10   NR_118784.1
11   X78071.1
12   AM231182.1
13   AM231183.1
14   AB678231.1
15   KU891982.1
16   MH538942.1
17   KT897715.1
18   NR_119091.1
19   X78072.1
20   MT357013.1
21   MT357001.1
22   FM994940.1
23   KJ951058.1
24   KR080514.1
25   KR056086.1
26   KC969670.1
27   KF158795.1
28   KJ951059.1
29   KM975638.1
30   X78073.1
31   S46735.1
32   FJ610237.1
33   KP999982.1
34   KT920407.1
35   KP410579.1
36   KR067608.1
37   KR067610.1
38   KP410577.1
39   KP410575.1
40   KT920409.1
41   KT920408.1
42   KR185842.1
43   KP872298.1
44   KR185879.1
45   KP410578.1
46   MK463634.1
47   KR011769.1
48   JQ086380.1
49   KR185871.1
50   MK463632.1
51   KP410576.1
52   KT321978.1
53   KT321976.1
54   U17030.1
55   KP872300.1
56   U16164.1
57   KF176994.1
58   MH109372.1
59   KF176995.1
60   KT321977.1
==== ===========

以下为分析代码 这些基因保存为data

::

   for i=1:length(data)
       fasta_download(data{i});
       fprintf('第%d个下载完毕\n',i)
       pause(0.5);
   end

   a='AGAGTTTGATCCTGGCTCAG'; %正义链
   b='TACGGCTACCTTGTTACGACTT'; %反义链

   Res=[];
   Res1=[];
   for i =1:length(data)
       try
           seq=fastaread([data{i},'.fasta']).Sequence;
           [Right_result,Wrong_result]=primer_blast_xia(seq,a,b);
           Res=[Res;Right_result];
           Res1=[Res1;Wrong_result];
           [Right_result,~]=primer_blast_xia(seqrcomplement(seq),b,a);
           Res=[Res;Right_result];
           Res1=[Res1;Wrong_result];
       catch ME
           fprintf('该序列有错:%d\n',i)
       end
   end
   data2=Res(:,2)-Res(:,1)+1;
   unique(data2)

   data3=Res1(:,2)-Res1(:,1)+1;
   unique(data3)