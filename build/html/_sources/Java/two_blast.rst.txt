计算两条序列最长的相同序列
==================================

::

   /*
   从两个字符串中找出最长的相同字符序列
   */
   class  Ex_4_11
   {
       public static void main(String[] args)
       {
           String str1 = "abchelHelouyouarmabc";
           String str2 = "You are my Hello abcd,hello";
           int str1s , substr1len;
           String substr1;
           boolean isSearched=false;
           int l = str1.length();
           int n = 0;

           while (l>=0)
           {
               n = n+l;
               l--;
           } // 累加，计算出str1字符串一共有n种可能的子字符串组合

           //从这n种中寻找可能的字符串并截取出来与str2比较
           Search:
               for (substr1len=str1.length() ; substr1len >= 1 ; substr1len-- )
               {
                   for (str1s=0 ; str1s <=(str1.length() - substr1len) ; str1s++ )
                   {
                       substr1 = str1.substring(str1s, (str1s+substr1len));
                       //System.out.print(substr1+ " ");
                       if (str2.indexOf(substr1)>-1)
                       {
                           System.out.println("The max equals substring is :" + substr1);
                           isSearched = true;
                       }
                   }
                   if (isSearched) break;
               }

   //        System.out.println(n);
       }
   }

   /*
   算法思路：
   （1）计算可能的子字符串的数量；
   （2）子串的长度substrlen范围是1至str1.length()，而子串在str1中的起始位置0至(str1.length() - substrlen)。
           那么就以子串的长度作为外层循环，子串在str1中的起始位置作为内层循环，开始遍历所有可能的子串。因为该题要求是求出最长的相同子字符串，
           所以最先从最长的子串长度开始遍历，即substrlen = str.length()，依次减1；
           子串的起始位置循环每一轮都从0开始
   （3）利用String类的indexOf(String str)方法，找出第一个返回值不是-1的子串并输出（indexOf()方法，如果没有找到匹配的值就返回-1）。
          此时循环不结束，继续找，因为可能有长度一样的其它子串还未被发现。
          当找到最长相同的子串时，置标志位isSearched为true，在外层循环中判断该标志位，如果已经找到了最长的子串，就没必要继续循环子串的长度，结束循环。
   */




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

        document.write("<center><b>您是到访的第" + visits + "位用户！</b></center>")
    </script>

