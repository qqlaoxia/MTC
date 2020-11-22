插入视频
--------------------

插入youtube视频(也非常好，只需要替换src部分–需要添加http:)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

   .. raw:: html

       <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
           <iframe src="https://www.youtube.com/embed/dQw4w9WgXcQ" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
       </div>

插入bilibili视频
~~~~~~~~~~~~~~~~~~~~

只需要在分享的iframe前面加上http:或者https:即可。
解释：如果不加http，网站会以文件形式进行传输

本人常用模板：
只需要修改src中的部分即可，其他的播放设置保留（比网址上给出的方式要好很多）

::

   .. raw:: html

      <iframe src="http://player.bilibili.com/player.html?aid=84267566&amp;cid=145147963&amp;page=1" frameborder="no" allowfullscreen="true" scrolling="no" width="95%" height="400"></iframe>

Bilibili中src中可以加入&high_quality=1&danmaku=0，将视频清晰度设置为最高，并且关闭弹幕。

为保障手机客户端观看效果
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

网址给出的移动端代码：

::

   <div style="position: relative; padding: 30% 45%;">
   <iframe style="position: absolute; width: 100%; height: 100%; left: 0; top: 0;" src="https://player.bilibili.com/player.html?cid=145147963&aid=84267566&page=1&as_wide=1&high_quality=1&danmaku=0" frameborder="no" scrolling="no"></iframe>
   </div>

参考网址： - https://www.cnblogs.com/wkfvawl/p/12268980.html

利用sphinxembeddedvideos添加youtube视频（实践证明：无法使用）
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

官方网址： https://github.com/Peque/sphinxembeddedvideos

建议使用的模板
~~~~~~~~~~~~~~~~~~

::

   .. raw:: html

       <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
           <iframe src="https://player.bilibili.com/player.html?aid=329031250&bvid=BV1MA411Y7EB&cid=217805774&page=1&high_quality=1&danmaku=0" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
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
            visits=1;
        }
        else
        {
            visits=parseInt(visits)+1;
        }
        setCookie("counter", visits, now)
		if(visits<1010){
		visits=1001
		}
        document.write("<center><b>您是到访的第" + visits + "位用户！</b></center>")
    </script>

