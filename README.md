# Pipeline to post `scrapy` item to your url


## Installation

Install `scrapy-sink` using `pip`:
```shell
pip install scrapy-sink
```
## Configuration

### for `scrapy` projects
1. Add the  ``settings.py`` of your Scrapy project like this:

```python
SINK_ADDR = 'http://api.mysite.com/v1/scraped-results'
```

You can also only set it in your environment variable

2. Enable the pipeline by adding it to ``ITEM_PIPELINES`` in your ``settings.py`` file:
   
```python
ITEM_PIPELINES = {
    'scrapy_sink.pipelines.SinkPipeline': 9999,
}
```
The order should after your persist pipeline such as save to database and after your preprocess pipeline.

### for none-`scrapy` projects

1. set enviroment variable `SINK_ADDR` to your target url that receving scraped result

```shell
export SINK_ADDR=http://api.mysite.com/v1/scraped-results
```

1. import `Sink` class to your script

```python
from scrapy_sink.simple import Sink
```

1. initialize `Sink` instance

```python
sink = Sink('your_site_name')
```

1. post result throgh `Sink` instance

```python
## todo: implement the payload extract action
payload = parse_scraped_page_as_dict(response.text)
sink.feed(payload)
```
## Usage

no need to change your code

## Getting help

Please use github issue

## Contributing

PRs are always welcomed.