title: 利用telnet发邮件
date: 2017-03-28 20:20:58
tags:
categories:
---
玩了下telnet发邮件，仅作记录，如有不妥请见谅。

<!-- more -->

常用的邮件协议有smtp和pop3（IMAP为升级版）。smtp用于不同邮件服务器之间的通讯和用户客户端向服务器投递邮件。pop3仅用于用户客户端从服务器取回邮件。smtp默认端口25，pop3默认端口110。

outlook就是常见的邮件客户端。

服务器与服务器之间投递邮件和用户客户端向服务器投递邮件本来是不需要任何验证的，但由于垃圾邮件的影响，现一般用户使用客户端向服务器投递邮件需要身份验证。注意，服务器之间的投递还是无需验证的，并且这里的投递和接收都是使用smtp协议。那么，服务器是怎么区别对待的呢？我们用outlook之类的邮件客户端时需要设置一个smtp服务器，这个smtp服务器地址一般在邮件服务商那里有直接提供，如qq邮箱的是smtp.qq.com。而邮件服务器之间投递邮件却使用的是另一个smtp服务器，这时使用的smtp服务器由dns解析获得，如查看qq的mx解析记录有mx1.qq.com、mx2.qq.com、mx3.qq.com，向三个其中一个投递即可。

我试了telnet方式模拟使用客户端借助登录163邮箱来向qq邮箱发送邮件，失败了，被当成垃圾邮件，不给发送；想从qq发向163，需要使用ssl的方式，不会搞，放弃了。嗯，试了下服务器投递的方式，直接向qq的mx*.qq.com投递，这个可以。下面过程：

利用nslookup查看qq邮箱的无需验证的smtp服务器（供给其它邮件服务器向其投递邮件的服务器）：
```
>nslookup
默认服务器:  public1.114dns.com
Address:  114.114.114.114

> set type=mx
> qq.com
服务器:  public1.114dns.com
Address:  114.114.114.114

非权威应答:
qq.com  MX preference = 10, mail exchanger = mx3.qq.com
qq.com  MX preference = 20, mail exchanger = mx2.qq.com
qq.com  MX preference = 30, mail exchanger = mx1.qq.com
```

由上可知道qq邮箱的三个smtp服务器，利用telnet连上：
```
> telnet mx1.qq.com 25
Host 'mx1.qq.com' resolved to 183.57.48.35.
Connecting to 183.57.48.35:25...
Connection established.
To escape to local shell, press 'Ctrl+Alt+]'.
220 newmx17.qq.com MX QQ Mail Server
```

打招呼自我介绍~：
```
> ehlo Coande
250-newmx17.qq.com
250-SIZE 73400320
250-STARTTLS
250 OK
```

设置邮件哪里来：
```
> mail from: <coande@e12e.com>
250 Ok
```

设置交给谁：
```
> rcpt to: <e12e@qq.com>
250 Ok
```

开始写邮件：
```
>data
354 End data with <CR><LF>.<CR><LF>
> just test!
> .

```
输入data后显示文字提示，紧跟着就可以填写内容了，要结束，键入`enter`然后输入`.`再`enter`会显示ok字样即为成功，我这次提示：
```
550 Ip frequency limited. http://service.mail.qq.com/cgi-bin/help?subtype=1&&id=20022&&no=1000725
```
ip被限制了。。。

稍等就可以去自己的收件箱查收邮件了，有一定几率会呆在垃圾箱。


伪造发件人原理：在输入data后，这样写：
```
> from: <laowang@e12e.com>
> subject: i just a subject
> 
> just test!
> .
```
收件人收到邮件时，显示的就是data里的邮件地址了，subject是邮件主题。但亲测，不知道为啥发给qq邮箱时，多了一些乱码以致data中的from和subject无效，直接在邮件内容中显示出来了。


另：模拟客户端的方式发送邮件，出现如下字眼时：
```
250-AUTH LOGIN PLAIN
250-AUTH=LOGIN
```
输入：
```
> auth login
```
然后出现`username: `base64后的字符串，这时要输入base64编码后的用户名；再然后是`password: `经过base64编码后的字符串，输入base64编码后的密码即可。

在操作过程中的输入必须要按照顺序一个字符一个字符的输入，不能颠倒顺序输入。输入过程中可能会遇到明明输入的是正确的，但是却报`502 Error: command not implemented`，多试几次就行了。





