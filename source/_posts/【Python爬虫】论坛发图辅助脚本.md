因为论坛发帖手动插入链接太费时间，所以我自己用Python爬虫写了一个小脚本，用来自动上传图片到图床，然后返回链接，我们只需直接复制链接就可以啦

因为不同图床需要提交的POST表单不一致，所以在这里我用ImgURL图床做示范，如果大家有需求，可自行修改代码。

使用脚本的时候，我们只需把需要上传的图片和这个脚本放在同一个文件夹中，然后运行脚本，稍作等待，看到提示时就可以在脚本运行文件夹中发现一个名为“图片链接.txt”的文件，里面就是图片链接啦！
代码如下：
```python
# -- coding:UTF-8 --
import requests
import os
import glob


def get(filename):
    url = "https://www.imgurl.org/upload/aws_s3"
    files = {'file': open(filename, 'rb')}
    data = {'file': files}
    headers = {
        'User-Agent':
        'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36'
    }
    response = requests.post(url, files=files, data=data, headers=headers)
    json = response.json()
    return "%s" % (json['url'])


filelist = []
filelist.extend(glob.glob(os.path.join("./", "*.jpg")))
filelist.extend(glob.glob(os.path.join("./", "*.png")))
filelist.extend(glob.glob(os.path.join("./", "*.webp")))
filelist.extend(glob.glob(os.path.join("./", "*.jpeg")))
# 以上内容可自行修改，将代码中的后缀名修改一下就可以匹配更多你想要的文件名啦！
f = open('图片链接.txt', 'a')
f.write("Markdown:\n")
for pictures in filelist:
    f.write("![](%s)\n" % get(pictures))
f.write("\n\n\nBBcode:\n")
for pictures in filelist:
    f.write("[img]%s[/img]\n" % get(pictures))
f.close()
print("链接已生成，请在脚本所在文件夹中找到名为“图片链接.txt”的文件，里面就是图片链接啦！")
```
开源地址：https://github.com/yunlongzhuhuo/pictures-uploader

效果如下：
![](./img/2754778-20220722180507851-1120206417.png)