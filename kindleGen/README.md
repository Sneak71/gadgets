��ָ����վ/������ǰһ����������±��һ����Ŀ¼����(.mobi)��Ȼ�����͵�kindle

# ˼·
1. ץȡָ����վ/������ǰһ����������£�ʹ��Calibre
2. ����{name}_{timestamp}.mobi�ļ���ʹ��Calibre
3. ʹ���������͵�kindle��ʹ��Calibre
4. ���ö�ʱ����ÿ���賿xx��ʱ��ִ�У�ʹ��cronb

# �ο�
1. [��calibreץȡRSS�������������鼰���͵�kindle](http://pangyi.github.io/blog/20141208/yong-calibrezhua-qu-rssxin-wen-zhi-zuo-dian-zi-shu-ji-tui-song-dao-kindle/)
2. [ץȡ��ҳ��������Kindle������](http://blog.codinglabs.org/articles/convert-html-to-kindle-book.html)
3. [Customizing the fetch process using Calibre](http://manual.calibre-ebook.com/news.html#customizing-the-fetch-process)
4. [API Documentation for recipes](http://manual.calibre-ebook.com/news_recipe.html)

# ʹ�õĵ���������
1. Calibre: `apt-get install calibre`

# ʹ�÷���
1. �޸�settings.py�ļ�
2. ���ö�ʱ����
```
#!/bin/sh
#file: blogPush.sh
cd /home/ele/git/Gadgets/kindleGen
python kindleBlogUpdate.py
```
Ȼ��
`30 0 * * * /root/timeSchedule/blogPush.sh`

����
**ItComm.recipe**
1. ����԰���ţ� http://feed.cnblogs.com/news/rss(��ǰ�޷�ʹ��)
2. HACKDAY ��https://hackaday.com/blog/feed/
3. InfoQ ��http://www.infoq.com/cn/feed
4. ���͹�԰��http://www.geekpark.net/rss

**ItSecurity.recipe**
1. FreeBuf��http://www.freebuf.com/feed
2. Woo Yun֪ʶ�⣺http://drops.wooyun.org/feed

**Others.recipe**
1. ��������http://feed.yeeyan.org/latest