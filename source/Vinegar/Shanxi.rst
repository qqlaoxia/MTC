.. MTC documentation master file, created by
   sphinx-quickstart on Tue Aug  4 14:21:29 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

山西老陈醋酿造工艺
===============================

**颜景宗,颜丹.传统山西老陈醋的酿造工艺[J].江苏调味副食品,2003(06):13-16.**


.. image:: imag/7.1/7.1.jpg
   :width: 700 px
   :align: center
   
.. image:: imag/7.1/7.2.jpg
   :width: 700 px
   :align: center

.. image:: imag/7.1/7.3.jpg
   :width: 700 px
   :align: center
   
.. image:: imag/7.1/7.4.jpg
   :width: 700 px
   :align: center

.. image:: imag/7.1/7.5.jpg
   :width: 700 px
   :align: center

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

