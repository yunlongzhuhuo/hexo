最近发Markdown帖的时候想插入多个图片，一个一个弄实在太费劲了，所以自己就写了一个4行的python小脚本来批量插入，在这里分享给大家。

```
urls = str(input("请输入图片链接（以空格来分割）："))
pictures = urls.split(' ')
for markdown in pictures:
    print("![](%s)" % markdown)
```


效果如下：
```
请输入图片链接（以空格来分割）：链接0 链接1
![](链接0)
![](链接1)
```
