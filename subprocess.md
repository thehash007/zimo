https://zhuanlan.zhihu.com/p/348311219  
https://www.bilibili.com/video/BV1jL4y1w7jS/?spm_id_from=333.337.search-card.all.click&vd_source=4f6603e7b64f10214d0c5526224f2679
# subprocess 模块
## subprocess.Popen 学习
``` bash
# subprocess 使用方法

>>> import subprocess
>>> obj = subprocess.Popen('ping -c 4 google.com', shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
>>> res = obj.stdout.read()
>>> print(res.decode('utf-8'))
>>>
>>> res = obj.stderr.read()
>>> print(res.decode('utf-8'))
```
`注：参数 shell 相当于添加 /bin/sh 做解析，以下两局代码等价，都是通过 shell 模式执行 'ls -l'`  
`>>> subprocess.Popen('ls -l', shell=True)`  
`>>> subprocess.Popen(['/bin/sh', '-c', 'ls -l'], shell=False)`  
`使用 res.poll()  方法可以监控子进程运行状态，如果子进程正在运行则该方法返回 None ，如果子进程运行结束则该方法返回0。使用res.stdout.readline()读取正在运行的子进程的输出。`
### 使用 shlex 分割命令字符串：
``` bash
# shlex 使用方法

>>> import shlex
>>> command_line = "ping -c 4 google.com"
>>> args = shlex.split(command_line)
>>> args
['ping', '-c', '4', 'google.com]
```
### shlex 安全的方式传入参数
```bash
# 将命令的一部分作为参数传入

>>> from shlex import quote
>>> filename = 'somefile; rm -rf ~'
>>> command = 'ls -l {}'. format(quote(filename))
>>> print(command)
ls -l 'somfile; rm -rf ~'
```

    