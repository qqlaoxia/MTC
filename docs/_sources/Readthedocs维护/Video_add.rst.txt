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