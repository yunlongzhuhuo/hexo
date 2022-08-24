最近新入手了M1 MacBook Air，想安装FastGithub来解决GitHub无法访问的问题，于是我下载了arm64版本，发现用不了，用sudo也不行，而且无法生成cacert文件夹，报错信息如下：（其他报错信息也可以通过同样的方法来解决问题）
```
zsh: killed     ./fastgithub

Saving session...
...copying shared history...
...saving history...truncating history files...
...completed.
```

于是我提了issue，开发人员告诉我使用x64版本。
![](./img/2754778-20220719194829807-1885958403.png)
x64确实能用，一点问题也没有。