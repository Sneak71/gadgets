BaicNewsRecipe����ı�дrecipe��API

class calibre.web.feeds.news.**BasicNewsRecipe**(options, log, progress_reporter)
	���ࡣ��������recipe������߼���ͨ���𲽸���������еĴ󲿷ֹ��ܣ����Ա�д�����Զ���/ǿ������recipe������recipe�����Ž̳̣��鿴[������ϲ����������վ](http://manual.calibre-ebook.com/news.html)
	
	abort_article(msg=None)
		������Ԥ�������е��ô˷�������ֹ��ǰ���µ����ء�����������Щ�������紿��Ƶ���µȵĲ��ʵ������������õġ�

	abort_recipe_processing(msg)
		����recipe����ϵͳֹͣ���recipe�����ء����û�չʾһ���򵥵Ļ�����Ϣ��

	add_toc_thumbnail(article, src)
		Call this from populate_article_metadata with the src attribute of an <img> tag from the article that is appropriate for use as the thumbnail representing the article in the Table of Contents. Whether the thumbnail is actually used is device dependent (currently only used by the Kindles). Note that the referenced image must be one that was successfully downloaded, otherwise it will be ignored.

	classmethod adeify_images(soup)
		If your recipe when converted to EPUB has problems with images when viewed in Adobe Digital Editions, call this method from within postprocess_html().

	canonicalize_internal_url(url, is_link=True)
		Return a set of canonical representations of url. The default implementation uses just the server hostname and path of the URL, ignoring any query parameters, fragments, etc. The canonical representations must be unique across all URLs for this news source. If they are not, then internal links may be resolved incorrectly.

		Parameters:	is_link �C Is True if the URL is coming from an internal link in an HTML file. False if the URL is the URL used to download an article.
	
	cleanup()
		�����е��������ؽ�������á���������һЩ����ǳ�������վ�ȵ���������

	clone_browser(br)
		Clone the browser br. Cloned browsers are used for multi-threaded downloads, since mechanize is not thread safe. The default cloning routines should capture most browser customization, but if you do something exotic in your recipe, you should override this method in your recipe and clone manually.

		Cloned browser instances use the same, thread-safe CookieJar by default, unless you have customized cookie handling.

	default_cover(cover_file)
		Ϊһ��û�з����recipe����һ��ͨ�÷��档

	download()
		Download and pre-process all articles from the feeds in this recipe. This method should be called only once on a particular Recipe instance. Calling it more than once will lead to undefined behavior. :return: Path to index.html

	extract_readable_article(html, url)
		��html����ȡ��Ҫ���������ݣ���������һ��Ԫ��(article_html, extracted_title)������Arc90��ԭʼ�ɶ��㷨��

	get_article_url(article)[source]
		Override in a subclass to customize extraction of the URL that points to the content for each article. Return the article URL. It is called with article, an object representing a parsed article from a feed. See feedparser. By default it looks for the original link (for feeds syndicated via a service like feedburner or pheedo) and if found, returns that or else returns article.link.

	get_browser(*args, **kwargs)
		����һ��������web��ȡ�ĵ��������ʵ����Ĭ������£�������һ��[mechanize](http://wwwsearch.sourceforge.net/mechanize/)�����ʵ�������ʵ��֧��cookies, ����robots.txt������ˢ�¼�ӵ��һ��mozilla firefox�û�����
		
		������recipeҪ�����ȵ�¼����ô�������������д������������磬����New York Times recipe�еĴ���������¼�Ի�ȡȫ����룺
		
		```python
		def get_browser(self):
			br = BasicNewsRecipe.get_browser(self)
			if self.username is not None and self.password is not None:
				br.open('http://www.nytimes.com/auth/login')
				br.select_form(name='login')
				br['USERID']   = self.username
				br['PASSWORD'] = self.password
				br.submit()
			return br
		```
	get_cover_url()[source]
		Return a URL to the cover image for this issue or None. By default it returns the value of the member self.cover_url which is normally None. If you want your recipe to download a cover for the e-book override this method in your subclass, or set the member variable self.cover_url before this method is called.

	get_feeds()[source]
		Return a list of RSS feeds to fetch for this profile. Each element of the list must be a 2-element tuple of the form (title, url). If title is None or an empty string, the title from the feed is used. This method is useful if your recipe needs to do some processing to figure out the list of feeds to download. If so, override in your subclass.

	get_masthead_title()[source]
		Override in subclass to use something other than the recipe title

	get_masthead_url()[source]
		Return a URL to the masthead image for this issue or None. By default it returns the value of the member self.masthead_url which is normally None. If you want your recipe to download a masthead for the e-book override this method in your subclass, or set the member variable self.masthead_url before this method is called. Masthead images are used in Kindle MOBI files.

	get_obfuscated_article(url)[source]
		If you set articles_are_obfuscated this method is called with every article URL. It should return the path to a file on the filesystem that contains the article HTML. That file is processed by the recursive HTML fetching engine, so it can contain links to pages/images on the web.

		This method is typically useful for sites that try to make it difficult to access article content automatically.

	classmethod image_url_processor(baseurl, url)[source]
		Perform some processing on image urls (perhaps removing size restrictions for dynamically generated images, etc.) and return the precessed URL.

	index_to_soup(url_or_raw, raw=False, as_tree=False)[source]
		Convenience method that takes an URL to the index page and returns a BeautifulSoup of it.

		url_or_raw: Either a URL or the downloaded index page as a string

	is_link_wanted(url, tag)[source]
		Return True if the link should be followed or False otherwise. By default, raises NotImplementedError which causes the downloader to ignore it.

		Parameters:	
		url �C The URL to be followed
		tag �C The Tag from which the URL was derived
	
	javascript_login(browser, username, password)[source]
		This method is used to login to a website that uses javascript for its login form. After the login is complete, the cookies returned from the website are copied to a normal (non-javascript) browser and the download proceeds using those cookies.

		An example implementation:

		def javascript_login(self, browser, username, password):
			browser.visit('http://some-page-that-has-a-login')
			form = browser.select_form(nr=0) # Select the first form on the page
			form['username'] = username
			form['password'] = password
			browser.submit(timeout=120) # Submit the form and wait at most two minutes for loading to complete
		Note that you can also select forms with CSS2 selectors, like this:

		browser.select_form('form#login_form')
		browser.select_from('form[name="someform"]')
	
	parse_feeds()
		����BasicNewsRecipe.get_feeds()���ص�feed�б��������б�����һ��Feed�����б�

	parse_index()
		recipeӦ��ʵ���������������һ����վ��������ʹ��feed�����������б����͵�Ӧ���Ƕ���Щӵ��һ��"��ӡ�汾"����ҳ��չʾ�������µĴ�ӡ�汾������Դ����ʵ�ִ˷�������������BasicNewsRecipe.parse_feeds()ʹ�ô˷�����

		�����뷵��һ���б��б��е�ÿ��Ԫ�ر������һ����ʽΪ('feed����'�� �����б�)�Ķ�ԪԪ�顣

		ÿ�������б�������������ʽ���ֵ䡣
		
		```python
		{
		'title'       : article title,
		'url'         : URL of print version,
		'date'        : The publication date of the article as a string,
		'description' : A summary of the article
		'content'     : The full article (can be an empty string). Obsolete
						do not use, instead save the content to a temporary
						file and pass a file:///path/to/temp/file.html as
						the URL.
		}
		```
		�ٸ����ӣ�������������The Atlantic��recipe�����⣬�����Ϊ��������"����"��һ�����õ������ǣ�

		�������ĳЩԭ������Ҫ��ֹ����������calibre���û�չʾһ���򵥵���Ϣ��������һ�����󣬵���abort_recipe_processing()��

	populate_article_metadata(article, soup, first)
		������ÿһ���������µ�HTMLҳ��ʱ���á��������Դӽ�����HTML (soup)�л�ȡ���µ�Ԫ���ݣ���������/�ܽ�ȡ�
		
		:param article: calibre.web.feeds.Article���һ������������޸���summary���ǵ�ҲҪ�޸�text_summary��
		param soup: ������µĽ������HTML
		:param first: ��������HTML�����µĵ�һ��ҳ�棬��ΪTrue.

	postprocess_book(oeb, opts, log)[source]
		Run any needed post processing on the parsed downloaded e-book.

		Parameters:	
		oeb �C An OEBBook object
		opts �C Conversion options
	
	postprocess_html(soup, first_fetch)[source]
		This method is called with the source of each downloaded HTML file, after it is parsed for links and images. It can be used to do arbitrarily powerful post-processing on the HTML. It should return soup after processing it.

		Parameters:	
		soup �C
		A BeautifulSoup instance containing the downloaded HTML.
		first_fetch �C True if this is the first page of an article.
	
	preprocess_html(soup)
		���������ÿһ�����ص�HTML�ļ�Դ�����ڽ������Ӻ�ͼƬǰ�����á�����������remove_tags��ָ�����������á�������������HTML��������ǿ���Ԥ�����ڴ�����֮��Ӧ�÷���һ��soup����

		soup: һ��BeautifulSoupʵ�������������ص�HTML��

	preprocess_raw_html(raw_html, url)
		This method is called with the source of each downloaded HTML file, before it is parsed into an object tree. raw_html is a unicode string representing the raw HTML downloaded from the web. url is the URL from which the HTML was downloaded.

		Note that this method acts before preprocess_regexps.

		This method must return the processed raw_html as a unicode object.

	classmethod print_version(url)
		����һ��ָ���������ݵ���ҳ��url������һ��ָ�����´�ӡ�汾��url��Ĭ�ϲ����κβ��������磺
		```python
		def print_version(self, url):
			return url + '?&pagewanted=print'
		```
	skip_ad_pages(soup)[source]
	This method is called with the source of each downloaded HTML file, before any of the cleanup attributes like remove_tags, keep_only_tags are applied. Note that preprocess_regexps will have already been applied. It is meant to allow the recipe to skip ad pages. If the soup represents an ad page, return the HTML of the real page. Otherwise return None.

	soup: A BeautifulSoup instance containing the downloaded HTML.

	sort_index_by(index, weights)[source]
	Convenience method to sort the titles in index according to weights. index is sorted in place. Returns index.

	index: A list of titles.

	weights: A dictionary that maps weights to titles. If any titles in index are not in weights, they are assumed to have a weight of 0.

	classmethod tag_to_string(tag, use_alt=True, normalize_whitespace=True)[source]
	Convenience method to take a BeautifulSoup Tag and extract the text from it recursively, including any CDATA sections and alt tag attributes. Return a possibly empty unicode string.

	use_alt: If True try to use the alt attribute for tags that don��t have any textual content

	tag: BeautifulSoup Tag

	articles_are_obfuscated = False
		��ΪTrue��Ȼ��ʵ��get_obfuscated_article()��������Щ����ץȡ���ݵ���վ��

	auto_cleanup = False
		Automatically extract all the text from downloaded article pages. Uses the algorithms from the readability project. Setting this to True, means that you do not have to worry about cleaning up the downloaded HTML manually (though manual cleanup will always be superior).

	auto_cleanup_keep = None
		ָ���Զ������㷨��Ӧ���Ƴ���Ԫ�ء��﷨Ϊһ��XPath���ʽ�����磺

		`auto_cleanup_keep = '//div[@id="article-image"]'` ����������ӵ�� id="article-image"��div��ǩ
		`auto_cleanup_keep = '//*[@class="important"]'` ����������ӵ������class="important"��Ԫ��
		`auto_cleanup_keep = '//div[@id="article-image"]|//span[@class="important"]'`����������ӵ������id="article-image"��divԪ�ؼ�ӵ������class="important"��spanԪ�ء�
						  
	center_navbar = True
		If True the navigation bar is center aligned, otherwise it is left aligned

	compress_news_images = False
		Set this to False to ignore all scaling and compression parameters and pass images through unmodified. If True and the other compression parameters are left at their default values, jpeg images will be scaled to fit in the screen dimensions set by the output profile and compressed to size at most (w * h)/16 where w x h are the scaled image dimensions.

	compress_news_images_auto_size = 16
		The factor used when auto compressing jpeg images. If set to None, auto compression is disabled. Otherwise, the images will be reduced in size to (w * h)/compress_news_images_auto_size bytes if possible by reducing the quality level, where w x h are the image dimensions in pixels. The minimum jpeg quality will be 5/100 so it is possible this constraint will not be met. This parameter can be overridden by the parameter compress_news_images_max_size which provides a fixed maximum size for images. Note that if you enable scale_news_images_to_device then the image will first be scaled and then its quality lowered until its size is less than (w * h)/factor where w and h are now the scaled image dimensions. In other words, this compression happens after scaling.

	compress_news_images_max_size = None
	Set jpeg quality so images do not exceed the size given (in KBytes). If set, this parameter overrides auto compression via compress_news_images_auto_size. The minimum jpeg quality will be 5/100 so it is possible this constraint will not be met.

	conversion_options = {}
	Recipe specific options to control the conversion of the downloaded content into an e-book. These will override any user or plugin specified values, so only use if absolutely necessary. For example:

	conversion_options = {
	  'base_font_size'   : 16,
	  'tags'             : 'mytag1,mytag2',
	  'title'            : 'My Title',
	  'linearize_tables' : True,
	}
	cover_margins = (0, 0, '#ffffff')
	By default, the cover image returned by get_cover_url() will be used as the cover for the periodical. Overriding this in your recipe instructs calibre to render the downloaded cover into a frame whose width and height are expressed as a percentage of the downloaded cover. cover_margins = (10, 15, ��#ffffff��) pads the cover with a white margin 10px on the left and right, 15px on the top and bottom. Color names defined at http://www.imagemagick.org/script/color.php Note that for some reason, white does not always work on windows. Use #ffffff instead

	delay = 0
		��������֮����ӳ٣�����Ϊ��λ���ò���������һ������������ʾһ������ȷ��ʱ�䡣

	description = u''
		A couple of lines that describe the content this recipe downloads. This will be used primarily in a GUI that presents a list of recipes.

	encoding = None
		Specify an override encoding for sites that have an incorrect charset specification. The most common being specifying latin1 and using cp1252. If None, try to detect the encoding. If it is a callable, the callable is called with two arguments: The recipe object and the source to be decoded. It must return the decoded source.

	extra_css = None
		Ϊ���ص�HTML�ļ�����ָ������������CSS�����������뵽������</head>��ǩǰ��<style>��ǩ�У���ˣ��Ḳ�ǳ�����Щ��HTML��ǩ��ʹ��style�������������е�CSS��ʽ�����磺

		`extra_css = '.heading { font: serif x-large }'`
	
	feeds = None
		�����ص�feed�б���ʽ������ [url1, url2, ...] ���� [('title1', url1), ('title2', url2),...]

	filter_regexps = []
		List of regular expressions that determines which links to ignore. If empty it is ignored. Used only if is_link_wanted is not implemented. For example:

		filter_regexps = [r'ads\.doubleclick\.net']
		will remove all URLs that have ads.doubleclick.net in them.

		Only one of BasicNewsRecipe.match_regexps or BasicNewsRecipe.filter_regexps should be defined.

	ignore_duplicate_articles = None
		������Щ����һ������Ԫ���ظ������¡�һ���ظ�������ָ������Щӵ����ͬ��title����/��url�����¡�Ҫ���Ծ�����ͬ��������£���������Ϊ��

		`ignore_duplicate_articles = {'title'}`
		
		��URL���棬��������Ϊ��
		`ignore_duplicate_articles = {'url'}`
		
		Ҫƥ��������URL����������Ϊ��
		``ignore_duplicate_articles = {'title', 'url'}``
	
	keep_only_tags = []
		ֻ����ָ���ı�ǩ�����ǵ��ӱ�ǩ��ָ��һ����ǩ�ĸ�ʽ����ο�BasicNewsRecipe.remove_tags. �����б�ǿգ���ô<body>��ǩ���ᱻ��գ�Ȼ����������ƥ����б�����ı�ǩ�����磺

		`keep_only_tags = [dict(id=['content', 'heading'])]`
		��ֻ��������idΪ��content�� �� ��heading���ı�ǩ��

	language = 'und'
		The language that the news is in. Must be an ISO-639 code either two or three characters long

	masthead_url = None
		By default, calibre will use a default image for the masthead (Kindle only). Override this in your recipe to provide a url to use as a masthead.

	match_regexps = []
		������ʽ�б�����ָ��follow�����ӡ���Ϊ�գ����������ֻ�е�is_link_wantedδʵ��ʱ��ʹ���������磺

		`match_regexps = [r'page=[0-9]+']`
		��ƥ������ӵ��page=���ֵ�URL

		ֻ�ܶ���BasicNewsRecipe.match_regexps �� BasicNewsRecipe.filter_regexps��

	max_articles_per_feed = 100
		ÿһ��feed���ص���������������������Щû���������ڵ�feed��˵�Ǻ����á����ڴ������feed����Ӧ��ʹ��BasicNewsRecipe.oldest_article��

	needs_subscription = False
		������ΪTrue�������ص�ʱ�򣬽��潫��ѯ���û����û��������롣������Ϊ��optional�����û����������ѡ��

	no_stylesheets = False
		��ݱ�ǣ��������ü�����Щ���й��ڸ��Ӷ����ʺ�ת��Ϊ�������ʽ����ʽ����վ����ʽ�����ȡֵΪTrue������ʽ���ᱻ���ش���

	oldest_article = 7.0
		������Դ���ص����ϵ����¡�����Ϊ��λ��

	preprocess_regexps = []
		List of regexp substitution rules to run on the downloaded HTML. Each element of the list should be a two element tuple. The first element of the tuple should be a compiled regular expression and the second a callable that takes a single match object and returns a string to replace the match. For example:

	preprocess_regexps = [
	   (re.compile(r'<!--Article ends here-->.*</body>', re.DOTALL|re.IGNORECASE),
		lambda match: '</body>'),
	]
		���Ƴ�<!�CArticle ends here�C> �� </body>֮����κζ�����

	publication_type = 'unknown'
		Publication type Set to newspaper, magazine or blog. If set to None, no publication type metadata will be written to the opf file.

	recipe_disabled = None
		Set to a non empty string to disable this recipe. The string will be used as the disabled message

	recursions = 0
		Number of levels of links to follow on article webpages

	remove_attributes = []
		�����б�ǩ���Ƴ��������б����磺

		`remove_attributes = ['style', 'font']`
		
	remove_empty_feeds = False
		If True empty feeds are removed from the output. This option has no effect if parse_index is overridden in the sub class. It is meant only for recipes that return a list of feeds using feeds or get_feeds(). It is also used if you use the ignore_duplicate_articles option.

	remove_javascript = True
		Convenient flag to strip all javascript tags from the downloaded HTML

	remove_tags = []
		����Ҫ�Ƴ��ı�ǩ��ָ�������ص�HTML��Ҫ�Ƴ��ı�ǩ��һ����ǩ��һ���ֵ����ʽ������
		```python
		{
		 name      : 'tag name',   #e.g. 'div'
		 attrs     : a dictionary, #e.g. {class: 'advertisment'}
		}
		```
		���еļ����ǿ�ѡ�ġ��鿴[Beautiful Soup](http://www.crummy.com/software/BeautifulSoup/bs3/documentation.html#Searching%20the%20Parse%20Tree),���������׼������˵����һ�����õ������ǣ�

		`remove_tags = [dict(name='div', attrs={'class':'advert'})]`
		
		�⽫�����ص�HTML���Ƴ����е�<div class="advert">��ǩ�����ӱ�ǩ��

	remove_tags_after = None
		�Ƴ�������ָ����ǩ����ֵı�ǩ���鿴[BasicNewsRecipe.remove_tags](http://manual.calibre-ebook.com/news_recipe.html#calibre.web.feeds.news.BasicNewsRecipe.remove_tags)�Ի�ȡָ��һ����ǩ�ĸ�ʽ�����磺

		`remove_tags_after = [dict(id='content')]`
		�����Ƴ���һ�����־���id="content"���Եı�ǩ������б�ǩ��

	remove_tags_before = None
		�Ƴ�������ָ����ǩǰ���ֵı�ǩ���鿴[BasicNewsRecipe.remove_tags](http://manual.calibre-ebook.com/news_recipe.html#calibre.web.feeds.news.BasicNewsRecipe.remove_tags)�Ի�ȡָ��һ����ǩ�ĸ�ʽ�����磺

		remove_tags_before = dict(id='content')
		�����Ƴ���һ�����־���id="content"���Եı�ǩǰ�����б�ǩ��

	requires_version = (0, 6, 0)
		ʹ�����recipe��Ҫ����Сcalibre�汾��

	resolve_internal_links = False
		If set to True then links in downloaded articles that point to other downloaded articles are changed to point to the downloaded copy of the article rather than its original web URL. If you set this to True, you might also need to implement canonicalize_internal_url() to work with the URL scheme of your particular website.

	reverse_article_order = False
		��ÿ��feed����������

	scale_news_images = None
		Maximum dimensions (w,h) to scale images to. If scale_news_images_to_device is True this is set to the device screen dimensions set by the output profile unless there is no profile set, in which case it is left at whatever value it has been assigned (default None).

	scale_news_images_to_device = True
		Rescale images to fit in the device screen dimensions set by the output profile. Ignored if no output profile is set.

	simultaneous_downloads = 5
		Number of simultaneous downloads. Set to 1 if the server is picky. Automatically reduced to 1 if BasicNewsRecipe.delay > 0

	summary_length = 500
		�����е����������

	template_css = u'\n .article_date {\n color: gray; font-family: monospace;\n }\n\n .article_description {\n text-indent: 0pt;\n }\n\n a.article {\n font-weight: bold; text-align:left;\n }\n\n a.feed {\n font-weight: bold;\n }\n\n .calibre_navbar {\n font-family:monospace;\n }\n '
		����Ϊtemplate�ṩ��ʽ��CSS�����磬�����������ݱ�����ڸ��������������Ӧ�������recipe��ʹ��extra_css��������ʽ��

	timefmt = ' [%a, %d %b %Y]'
		��ҳ��ʾ�����ڸ�ʽ��Ĭ����: Day_Name, Day_Number Month_Name Year

	timeout = 120.0
		�ӷ�������ȡ�ļ��ĳ�ʱʱ�䣬����Ϊ��λ��

	title = u'Unknown News Source'
		������ʹ�õı���

	use_embedded_content = None
		Normally we try to guess if a feed has full articles embedded in it based on the length of the embedded content. If None, then the default guessing is used. If True then the we always assume the feeds has embedded content and if False we always assume the feed does not have embedded content.

	use_javascript_to_login = False
		If you set this True, then calibre will use javascript to login to the website. This is needed for some websites that require the use of javascript to login. If you set this to True you must implement the javascript_login() method, to do the actual logging in.