## Python 文章摘要提取的库


>  示例文本来自 http://news.steelcn.cn/a/105/20100123/103370A9F83806.html, 保存正文至 content.txt

### 1. Textrank4zh

https://github.com/letiantian/TextRank4ZH

#### 安装

```bash
$ pip install textrank4zh
```

#### 示例

```python
import codecs
from textrank4zh import TextRank4Keyword, TextRank4Sentence


content = codecs.open('content.txt', 'r', 'utf-8').read()
tr4s = TextRank4Sentence()
tr4s.analyze(text=content, lower=True, source='all_filters')

for item in tr4s.get_key_sentences(num=3):
    print(item.index, item.weight, item.sentence)
    

    
# Result:
# 0 0.11783211562891267 日前获悉，世界首家运用日本神户制钢公司第三代炼铁法(ITmk3)的商业铁厂，钢动态公司(Steel Dynamics)位于明尼苏达州的Hoyt Lakes厂
# 6 0.09533764028919228 铁厂产量将随着生产情况而逐步提升，预计至2010年中期可达到50万吨粒铁的设计年产能
# 1 0.08828227247879757 已正式投入粒铁的生产
```



### 2. FastTextRank

https://github.com/ArtistScript/FastTextRank

#### 安装

```
$ pip install 
```

#### 示例

```python
import codecs
from FastTextRank.FastTextRank4Sentence import FastTextRank4Sentence


mod = FastTextRank4Sentence(use_w2v=False, tol=0.0001)

sentence_number = 1
content = codecs.open('content.txt', 'r', 'utf-8').read()
print(mod.summarize(content, sentence_number))


# Result:
# ['日前获悉，世界首家运用日本神户制钢公司第三代炼铁法(ITmk3)的商业铁厂，钢动态公司(Steel Dynamics)位于明尼苏达州的Hoyt Lakes厂已正式投入粒铁的生产。']
```


### 3. Sumy

https://github.com/miso-belica/sumy

#### 安装

```bash
$ pip install sumy
```

#### 示例

```python
from __future__ import absolute_import
from __future__ import division, print_function, unicode_literals

from sumy.parsers.html import HtmlParser
from sumy.nlp.tokenizers import Tokenizer
from sumy.parsers.plaintext import PlaintextParser
from sumy.summarizers.lsa import LsaSummarizer as Summarizer
from sumy.nlp.stemmers import Stemmer
from sumy.utils import get_stop_words


LANGUAGE = "chinese"
SENTENCES_COUNT = 1


if __name__ == "__main__":
    url = "http://news.steelcn.cn/a/105/20100123/103370A9F83806.html"
    parser = HtmlParser.from_url(url, Tokenizer(LANGUAGE))
    # or for plain text files
    # parser = PlaintextParser.from_file("content.txt", Tokenizer(LANGUAGE))
    # parser = PlaintextParser.from_string("Check this out.", Tokenizer(LANGUAGE))
    stemmer = Stemmer(LANGUAGE)

    summarizer = Summarizer(stemmer)
    summarizer.stop_words = get_stop_words(LANGUAGE)

    for sentence in summarizer(parser.document, SENTENCES_COUNT):
        print(sentence)


# Result:
# 除北美地区以外，神户制钢还在越南、印度、俄罗斯、澳大利亚等国建有粒铁项目，其总年产能将达数百万吨。
```

### 4. Gensim

https://github.com/RaRe-Technologies/gensim

#### 安装

```
$ pip install gensim
```

#### 示例

```
import codecs
from gensim.summarization.summarizer import summarize



content = codecs.open('content.txt', 'r', 'utf-8').read()

summary = summarize(content, ratio=0.2)
print(summary)


# Result:
# 结果为空, 可能 gensim 不适合做短文本的摘要提取吧
```




### 5. SnowNLP

https://github.com/isnowfy/snownlp

#### 安装

```bash
$ pip install snownlp				
```

#### 示例

```python
from snownlp import SnowNLP
import codecs

content = codecs.open('content.txt', 'r', 'utf-8').read()
s = SnowNLP(content)
print(s.keywords(3))
print(s.summary(3))

# Result:
# ['公司', '铁', '生产']
# ['已正式投入粒铁的生产', '该厂于去年第四季度投入生产', '钢动态公司(Steel Dynamics)位于明尼苏达州的Hoyt Lakes厂']
```

### 6. Textteaser

https://github.com/IndigoResearch/textteaser

好像目前只支持英文

```python
import codecs


content = codecs.open('content.txt', 'r', 'utf-8').read()
title = ""

tt = TextTeaser(content)
summary = tt.summarize(title, text)
print(summary)
```



### 总结
以上为抽取型摘要, 都试过一遍, 感觉  Textrank4zh 和 FastTextRank 效果还可以, 其次是 Sumy。后续还会补充一些关于抽象型摘要的库。


