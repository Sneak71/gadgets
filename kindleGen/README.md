��ָ����վ/������ǰһ����������±��һ����Ŀ¼����(.mobi)��Ȼ�����͵�kindle

# ˼·
1. ץȡָ����վ/������ǰһ����������£�ʹ��Calibre
2. ����YYYYMMDD_blogs.mobi�ļ���ʹ��Calibre
3. ʹ���������͵�kindle��ʹ��Calibre
4. ���ö�ʱ����ÿ���賿xx��ʱ��ִ�У�ʹ��cronb

# �ο�
1. [��calibreץȡRSS�������������鼰���͵�kindle](http://pangyi.github.io/blog/20141208/yong-calibrezhua-qu-rssxin-wen-zhi-zuo-dian-zi-shu-ji-tui-song-dao-kindle/)
2. [ץȡ��ҳ��������Kindle������](http://blog.codinglabs.org/articles/convert-html-to-kindle-book.html)

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
1. ����԰���ţ� http://feed.cnblogs.com/news/rss(��ǰ�޷�ʹ��)
2. FreeBuf��http://www.freebuf.com/feed
3. Woo Yun֪ʶ�⣺http://drops.wooyun.org/feed
4. HACKDAY ��https://hackaday.com/blog/feed/
5. InfoQ ��http://www.infoq.com/cn/feed
6. ���͹�԰��http://www.geekpark.net/rss
7. ��������http://feed.yeeyan.org/latest