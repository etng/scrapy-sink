# 发送爬取道的内容到制定的网址

## 一、安装

使用`PIP`或其他工具安装包 `scrapy-sink`:
```shell
pip install scrapy-sink
```
## 二、配置

### 1. `scrapy`项目
* 添加如下配置到`scrapy`项目的``settings.py``文件中:

```python
SINK_ADDR = 'http://api.mysite.com/v1/scraped-results'
```
也可以直接设置到环境变量中,这样就不用修改代码了

```shell
export SINK_ADDR=http://api.mysite.com/v1/scraped-results
```

>>> 对于 `SPIDERHUB` 托管的由 `SPIDERMAN` 运行的项目，默认会直接设置此地址，可以直接跳过此步骤

* 向配置文件 ``settings.py`` 中的 ``ITEM_PIPELINES``配置项中添加如下内容:
   
```python
ITEM_PIPELINES = {
    'scrapy_sink.pipelines.SinkPipeline': 9999,
}
```
优先级应该是设置成数据预处理完成待写入数据库的管道之间的样子.

### 2. 非`scrapy`项目

* 设置环境变量`SINK_ADDR`为待接收爬取内容的网址

```shell
export SINK_ADDR=http://api.mysite.com/v1/scraped-results
```

* 引入 `Sink`类到你的脚本中

```python
from scrapy_sink.simple import Sink
```

* 初始化 `Sink` 实例

```python
sink = Sink('your_site_name')
```
如果没有设置环境变量的话，也可以直接将`SINK_ADDR`作为参数传入
```python
sink = Sink('your_site_name', sink_addr='http://api.mysite.com/v1/scraped-results')
```
>>> 对于 `SPIDERHUB` 托管的由 `SPIDERMAN` 运行的项目，由于地址会自动生成和调整，不需要设置环境变量或用可选参数传入，如果传入了有可能得不到正确的结果

* 通过 `Sink` 发送爬取结果

```python
## todo: 实现提取数据的相关操作
payload = parse_scraped_page_as_dict(response.text)
sink.feed(payload)
```
## 三、使用方式

如上所述几乎不用修改代码

## 四、获得帮助

请使用 `github` 项目提供的工单系统提交工单

## 五、贡献代码

欢迎提交 `PR` , 我们会尽快讨论合并.