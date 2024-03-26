
https://www.cnblogs.com/ghylpb/p/12513908.html
https://cloud.tencent.com/developer/article/1520592


安装	pip install GitPython
来自 <https://cloud.tencent.com/developer/article/1520592> 

# 1 Git add 

```
1
repo.index.add('**')

To answer your question, repo.index.add(...) is low-level enough to unconditionally add all paths given in the items iterable, and therefore it is not suited to emulate something like git add -u.

When I perform repo.index.add('.') gitpython adds .git directory...

1.2  add 某个 file 
index.add([new_file_path])   

2 
repo.git.add(all=True)
repo.git.add('--all')

It's one-to-one correspondence for git add --all
```

