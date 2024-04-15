
## 0.1 日志（模块logging）

- 基本应用：用于统计日志、用来做故障排除debug、用来记录错误，完成代码优化。
- 日志处理本质：Logger/FileHandler/Formatter
- logging.basicconfig和logger对象的区别
  - logging.basicconfig:使用方便，但不能同时向文件和屏幕上输出。（logging.debug,logging.warning）
  - logger对象：复杂
    - 创建一个logger对象
    - 创建一个文件操作符
    - 创建一个屏幕操作符
    - 创建一个格式
    - 给logger对象绑定 文件操作符
    - 给logger对象绑定 屏幕操作符
    - 给文件操作符设定格式
    - 给屏幕操作符设定格式
    - 用logger对象来操作

```python
import logging

logger = logging.getLogger()
fh = logging.FileHandler('log.log')
sh = logging.StreamHandler()
logger.addHandler(fh)
logger.addHandler(sh)
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
fh.setFormatter(formatter)
sh.setFormatter(formatter)
logger.warning('message')
```



- 推荐处理日志方式

```python
import logging

file_handler = logging.FileHandler(filename='x1.log', mode='a', encoding='utf-8',)
logging.basicConfig(
    format='%(asctime)s - %(name)s - %(levelname)s -%(module)s:  %(message)s',
    datefmt='%Y-%m-%d %H:%M:%S %p',
    handlers=[file_handler,],
    level=logging.ERROR
)

logging.error('你好')
```

- 推荐处理日志方式+日志分割

```python
import time
import logging
from logging import handlers
# file_handler = logging.FileHandler(filename='x1.log', mode='a', encoding='utf-8',)
file_handler = handlers.TimedRotatingFileHandler(filename='x3.log', when='s', interval=5, encoding='utf-8')
logging.basicConfig(
    format='%(asctime)s - %(name)s - %(levelname)s -%(module)s:  %(message)s',
    datefmt='%Y-%m-%d %H:%M:%S %p',
    handlers=[file_handler,],
    level=logging.ERROR
)

for i in range(1,100000):
    time.sleep(1)
    logging.error(str(i))
```

注意事项：

```python
# 在应用日志时，如果想要保留异常的堆栈信息。
import logging
import requests

logging.basicConfig(
    filename='wf.log',
    format='%(asctime)s - %(name)s - %(levelname)s -%(module)s:  %(message)s',
    datefmt='%Y-%m-%d %H:%M:%S %p',
    level=logging.ERROR
)

try:
    requests.get('http://www.xxx.com')
except Exception as e:
    msg = str(e) # 调用e.__str__方法
    logging.error(msg,exc_info=True)
```

- 项目结构目录

  - 脚本

  ![1556453767003](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1556453767003.png)

  - 单可执行文件

  ![1556453804687](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1556453804687.png)

  - 多可执行文件

  ![1556453832951](C:\Users\xiaohui\AppData\Roaming\Typora\typora-user-images\1556453832951.png)


