##将普通爬虫更改为scrapy-redis:
**spider_name.py**

1. from scrapy_redis.spiders import RedisSpider #导入RedisSpider
2. 原本的class NameSpider(scrapy.Spider):继承的类更换为RedisSpider
3. redis_key = 'sinaspider:start_urls' #运行的时候使用redis_key,唯一

**items.py**

加入     `crawled = scrapy.Field()`
    `spider = scrapy.Field()`两个字段

**pipelines.py**

	class ExamplePipeline(object):
	    def process_item(self, item, spider):
	        item["crawled"] = datetime.utcnow()
	        item["spider"] = spider.name+"name" #自定义name
	        return item

**settings.py**

1. 配置redis:
	-  REDIS_HOST="192.168.21.51"
	- REDIS_PORT=6379  #不加引号
	- 如果爬虫端（slave端），刚好是在redis安装的主键上，默认可以不配置redis相关信息
2. SCHEDULER_PERSIST = True #分布式爬虫可以停止/暂停,下次可以继续爬虫
3. DUPEFILTER_CLASS = "scrapy_redis.dupefilter.RFPDupeFilter" #使用scrapy-redis自己的组件去重,不使用scrapy默认的去重
4. SCHEDULER = "scrapy_redis.scheduler.Scheduler" #使用scrapy-redis自己调度器,不使用scrapy默认的调度器
5. SCHEDULER_QUEUE_CLASS = "scrapy_redis.queue.SpiderPriorityQueue"  #按照sorted 排序顺序出队列，建议使用某一个，这样才能在redis数据库中看到,其实可以不写不影响结果
6.  ITEM_PIPELINES 加入pipelines中的ExamplePipeline : ` 'scrapy_redis.pipelines.RedisPipeline': 299,`和`'scrapy_redis.pipelines.RedisPipeline': 400,`#开启redis处理器

**运行**
- 在spiders文件夹下新建启动文件 main.py写入:`from scrapy import cmdline`
`cmdline.execute("scrapy runspider myspider_redis.py".split())`
- 运行: 1. 启动 main.py 2.启动redis:`redis-cli` 3.lpush + redis_key + url