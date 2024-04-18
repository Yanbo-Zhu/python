
![](images/Pasted%20image%2020240418164129.png)



# 1 DocOpt

![](images/Pasted%20image%2020240418164145.png)

# 2 Click 

Mit decorator 


![](images/Pasted%20image%2020240418164155.png)

# 3 Invoke

```
#!/usr/bin/python
# -*- encoding: utf-8 -*-
from invoke import task
@task
def ship(c, name, speed=12, drifting=False):
    print('ship')
    print('context: {}'.format(c))
    print('name: {}'.format(name))
    print('speed: {}'.format(speed))
    print('drifting: {}'.format(drifting))

@task
def mine(c):
    print('mine')
    print('context: {}'.format(c))


```
