利用matlab快速定位文字位置
==================================
本网页介绍了如何利用vba实现字符串的查找，并生成其位置
必须知道的网址： 微软的vba语法手册 -
https://docs.microsoft.com/zh-cn/office/vba/api/word.wdinformation -
https://docs.microsoft.com/en-us/previous-versions/office/developer/office-2003/aa211923(v=office.11)

1. 我们首先从vba开始
^^^^^^^^^^^^^^^^^^^^

版本1： 网址 https://zhidao.baidu.com/question/2011085583766233188.html

::

    Private Sub CommandButton1_Click()
       Dim p, r, s, t
        s= "石膏板造bai型顶"
       With Selection.Find
           .ClearFormatting
           .MatchWholeWord = True
           .MatchCase = False
           t = .Execute(FindText:=s)
       End With
        p= Selection.Information(wdActiveEndPageNumber)
        r= Selection.Information(wdFirstCharacterLineNumber)
       If t Then
           MsgBox "成功，已找到du“" & s & "”" & vbCrLf & _
               "页码："& p & vbCrLf & "行数：zhi" & r, vbOKOnly, _
               "成功"
       Else
           MsgBox "很遗憾dao，没有找到“" & s & "”", vbOKOnly, _
               "遗憾"
       End If
    End Sub

实例2：http://www.exceloffice.net/archives/3094

::

    Sub QQ1722187970()
        Const wdActiveEndPageNumber = 3
        Const wdGoToHeading = 11
        Const wdGoToAbsolute = 1
        Const wdGoToPage = 1
        Dim oDoc As Document
        Dim oWord As Word.Application
        Set oWord = Word.Application
        Set oDoc = oWord.ActiveDocument
        Dim oRng As Range
        With oDoc
            iMin = -1
            I = 1
           Do
                '循环每个标题
                Set oRng = .GoTo(wdGoToHeading, wdGoToAbsolute, I)
                '如果到底或者回到头则退出循环
                If oRng.Start < iMin Or oRng.Start = iMin Then Exit Do
                '输出页码
                 Debug.Print oRng.Information(wdActiveEndPageNumber)
                iMin = oRng.Start
                I = I + 1
          Loop Until 1 <> 1
        End With
    End Sub

这是其他网友给出的vba版本，不在一一列举： -
https://zhuanlan.zhihu.com/p/61358933 -
http://www.360doc.com/content/18/0515/12/9261962\_754100826.shtml -

2. python/matlab版本
^^^^^^^^^^^^^^^^^^^^

我们已经知道，vba语法是微软制定的，它与使用matlab。
如果我们直接将其翻译为python或matlab版本

::

    import win32com

    s="天津"
    w = win32com.client.Dispatch('Word.Application')
    w.Visible = 0;
    w.DisplayAlerts = 0;
    doc = w.Documents.Open(r'F:\天津科技大学\日常工作\2020\1月份\工程认证\最终材料\2020-7-29 版本\报告正文\自评报告正文-20200729--夏梦雷修订.docx');
    w.Selection.Find.ClearFormatting();
    w.Selection.Find.Replacement.ClearFormatting();
    w.Selection.Find.MatchWholeWord = True
    w.Selection.Find.MatchCase = False

    while w.Selection.Find.Execute(s):
        p= w.Selection.Information(wdActiveEndPageNumber)
        print(p)

就会发现程序无法识别wdActiveEndPageNumber这个常量。

有的网友给出了一个解决思路：
https://stackoverflow.com/questions/24005664/finding-the-current-page-in-word-document

该网友认为：\ **wdActiveEndPageNumber是win32com.client**\ 模块中的一个常量，在代码之前导入即可：

::

    from win32com.client.gencache import EnsureDispatch
    from win32com.client import constants
    word = EnsureDispatch("Word.Application")
    mydoc = word.Documents.Open("path:\\to\\file")
    mydoc.ActiveWindow.Selection.Information(constants.wdActiveEndPageNumber)

**这种思路也是错误的，python依旧无法识别该变量**\ ，其实该网页的第二个网友给出的思路是正确的，即：wdActiveEndPageNumber是个枚举值，是一个int值，只需要在vba中找到该值就行。

在这种思路下，我们查找了微软的手册，以及部分网友的总结。
重要的网址如下： -
https://docs.microsoft.com/zh-cn/office/vba/api/word.wdinformation

可以看出，wdActiveEndPageNumber枚举类型对应的是3，因此把对应的符号改为3即可。

值得注意的是，w.Selection.Find.Execute(s)至执行一次，也就是每次只执行以下，只需要做个循环，就可以把整个文档遍历完毕。

3. 完整的python版本和matlab版本
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.1 python版本
''''''''''''''

::

    import win32com


    s="天津"
    w = win32com.client.Dispatch('Word.Application')
    w.Visible = 0
    w.DisplayAlerts = 0
    doc = w.Documents.Open(r'F:\天津科技大学\日常工作\2020\1月份\工程认证\最终材料\2020-7-29 版本\报告正文\自评报告正文-20200729--夏梦雷修订.docx');
    w.Selection.Find.ClearFormatting()
    w.Selection.Find.Replacement.ClearFormatting()
    w.Selection.Find.MatchWholeWord = True
    w.Selection.Find.MatchCase = False

    while w.Selection.Find.Execute(s):
        p= w.Selection.Information(3)
        print(p)

3.2 Matlab版本
''''''''''''''

::

    s='天津科技大学'
    w=actxserver('Word.Application');
    w.Visible = 0;
    w.DisplayAlerts = 0;
    doc = w.Documents.Open('F:\天津科技大学\日常工作\2020\1月份\工程认证\最终材料\2020-7-29 版本\报告正文\自评报告正文-20200729--夏梦雷修订.docx');
    w.Selection.Find.ClearFormatting();
    w.Selection.Find.Replacement.ClearFormatting();
    w.Selection.Find.MatchWholeWord = true
    w.Selection.Find.MatchCase = false


    Num=0
    while(w.Selection.Find.Execute(s))
        Num=Num+1;
        fprintf('运行了%d次',Num)
        disp( w.Selection.Information(3))
    end

总结：
^^^^^^

-  实际上，WdInformation可以给出所有我们想要的信息，只需填入对应的枚举值即可。包括页码、行数、列数、光标等等。
-  https://docs.microsoft.com/zh-cn/office/vba/api/word.wdinformation

4. 本技术讲解视频
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
        <iframe src="https:///player.bilibili.com/player.html?aid=244037321&bvid=BV19v411q7RF&cid=220333810&page=1&high_quality=1&danmaku=0" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>

.. raw:: html

   <script>
	window.onload = function(){	
		var oMessageBox = document.getElementById("messageBox");
		var oInput = document.getElementById("myInput");
		var oPostBtn = document.getElementById("doPost");
		
		oPostBtn.onclick = function(){
			if(oInput.value){
				//写入发表留言的时间
				var oTime = document.createElement("div");
				oTime.className = "time";
				var myDate = new  Date();
				oTime.innerHTML = myDate.toLocaleString();
				oMessageBox.appendChild(oTime);
				
				//写入留言内容
				var oMessageContent = document.createElement("div");
				oMessageContent.className = "message_content";
				oMessageContent.innerHTML = oInput.value;
				oInput.value = "";
				oMessageBox.appendChild(oMessageContent);
			}
			
		}
		
	}

   </script>


   <div class="content">
        <div class="title">用户留言</div>
        <div class="message_box" id="messageBox"></div>
        <div><input id="myInput" type="text" placeholder="请输入留言类容"><button id="doPost">提交</button></div>
    </div>


.. raw:: html

       <script type="text/javascript">
        var caution=false
        function setCookie(name,value,expires,path,domain,secure)
        {
            var curCookie=name+"="+escape(value) +
                ((expires)?";expires="+expires.toGMTString() : "") +
                ((path)?"; path=" + path : "") +
                ((domain)? "; domain=" + domain : "") +
                ((secure)?";secure" : "")
            if(!caution||(name + "=" + escape(value)).length <= 4000)
            {
                document.cookie = curCookie
            }
            else if(confirm("Cookie exceeds 4KB and will be cut!"))
            {
                document.cookie = curCookie
            }
        }
        function getCookie(name)
        {
            var prefix = name + "="
            var cookieStartIndex = document.cookie.indexOf(prefix)
            if (cookieStartIndex == -1)
            {
                return null
            }
            var cookieEndIndex=document.cookie.indexOf(";",cookieStartIndex+prefix.length)
            if(cookieEndIndex == -1)
            {
                cookieEndIndex = document.cookie.length
            }
            return unescape(document.cookie.substring(cookieStartIndex+prefix.length,cookieEndIndex))
        }
        function deleteCookie(name, path, domain)
        {
            if(getCookie(name))
            {
                document.cookie = name + "=" +
                    ((path) ? "; path=" + path : "") +
                    ((domain) ? "; domain=" + domain : "") +
                    "; expires=Thu, 01-Jan-70 00:00:01 GMT"
            }
        }
        function fixDate(date)
        {
            var base=new Date(0)
            var skew=base.getTime()
            if(skew>0)
            {
                date.setTime(date.getTime()-skew)
            }
        }
        var now=new Date()
        fixDate(now)
        now.setTime(now.getTime()+365 * 24 * 60 * 60 * 1000)
        var visits = getCookie("counter")
        if(!visits)
        {
            visits=1000;
        }
        else
        {
            visits=parseInt(visits)+1;
        }
        setCookie("counter", visits, now)

        document.write("<center><b>您是到访的第" + visits + "位用户！</b></center>")
    </script>

