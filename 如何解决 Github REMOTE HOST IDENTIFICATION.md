# 如何解决 Github REMOTE HOST IDENTIFICATION HAS CHANGED

## 问题

通过 `SSH` 克隆 Github 项目时 会报以下错误 `WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!`

```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the RSA key sent by the remote host is
SHA256:uNiVztksCsDhcc0u9e8BujQXVUpKZIDTMczCvj3.
Please contact your system administrator.
Add correct host key in /Users/xxx/.ssh/known_hosts to get rid of this message.
Offending RSA key in /Users/xxx/.ssh/known_hosts:12
Host key for github.com has changed and you have requested strict checking.
Host key verification failed.
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

## 原因

2023年3月23日，github博客发布的文章中提到， `GitHub.com` 的 `RSA SSH private key` 被提交到了一个公开的仓库，为了保证用户数据安全，替换了新的密钥。

> 
> 
> 
> **What happened and what actions have we taken?**
> 
> This week, we discovered that GitHub.com’s RSA SSH private key was briefly exposed in a public GitHub repository. We immediately acted to contain the exposure and began investigating to understand the root cause and impact. We have now completed the key replacement, and users will see the change propagate over the next thirty minutes. Some users may have noticed that the new key was briefly present beginning around 02:30 UTC during preparations for this change.
> 
> Please note that this issue was not the result of a compromise of any GitHub systems or customer information. Instead, the exposure was the result of what we believe to be an inadvertent publishing of private information. We have no reason to believe that the exposed key was abused and took this action out of an abundance of caution.
> 

## 解决方法

1. 编辑 `~/.ssh/known_hosts` ，搜索``github`` 关键字，删除对应的一行。
2. 重新`clone` ，弹出询问后输入`yes` 即可

```bash
Cloning into 'code.github.io'...
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```

## 参考链接

- [Github Blog - We updated our RSA SSH host key](https://github.blog/2023-03-23-we-updated-our-rsa-ssh-host-key/)