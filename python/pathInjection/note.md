# Python路径注入


sinks


文件读取
```python
flask.send_file;Argument[0] # 读取文件
fastapi.responses.FileResponse;Argument[0]  # 读取文件
```

文件删除
```python
os.remove;Argument[0]   # 删除文件
os.unlink;Argument[0]   # 删除文件
os.removedirs;Argument[0]   # 删除多级目录
os.rmdir;Argument[0]    # 删除目录
shutil.rmtree;Argument[0]   # 删除目录
```

其他
```python
os.open;Argument[0] # 该方法返回文件对象,可进行文件读取、写入、获取文件信息等操作
os.chdir;Argument[0]    # 将当前工作目录更改为指定路径
os.renames;Argument[0, 1]   # 将old文件夹或文件移动到new文件夹或文件
os.rename;Argument[0, 1]    # 将src文件夹或文件移动到dst文件夹或文件
os.replace;Argument[0, 1]   # 将文件或目录src重命名为dst
os.scandir;Argument[0]  # 返回目录
os.listdir;Argument[0]  # 返回目录
os.stat;Argument[0] # 获取文件或文件描述符的状态
os.lstat;Argument[0] # 获取文件或文件描述符的状态
os.truncate;Argument[0] # 截断文件为指定长度
os.makedirs;Argument[0] # 递归创建文件夹
os.mkdir;Argument[0] # 创建文件夹
os.access;Argument[0] # 判断当前用户是否对指定文件有指定的访问权限,多用于判断文件访问权限后读取或写入文件
os.chflags;Argument[0] # 将路径flags设置为目标flags, 例如:只读. 只支持在 Unix 下使用
os.lchflags;Argument[0] # 将路径flags设置为目标flags. 只支持在 Unix
os.chmod;Argument[0]    # 将路径flags设置为目标flags, 例如:只读.
os.lchmod;Argument[0]   # 将路径mode设置为目标mode. 只支持在 Unix
os.chown;Argument[0]    # 将路径的所有者和组 ID 更改为数字uid和gid. 只支持在 Unix
os.chroot;Argument[0]   # 将当前进程的根目录更改为path. 只支持在 Unix
os.lchown;Argument[0]   # 将路径的所有者和组ID更改为数字uid和gid. 只支持在 Unix
os.link;Argument[0, 1]  # 创建一个指向名为dst的src的硬链接. 支持Unix、Windows
os.mkfifo;Argument[0]   # 创建文件
os.pathconf;Argument[0] # 返回文件指定配置信息
```


示例

```python
from flask import Flask, send_file

app = Flask(__name__)

@app.route('/<path:path>')
def hello_world(path):
    return send_file(path)


if __name__ == '__main__':
    app.run()
```

修复

```python
from werkzeug.utils import secure_filename
from flask import Flask, send_file

app = Flask(__name__)

@app.route('/<path:path>')
def hello_world(path):
    path = secure_filename(path)
    return send_file(path)


if __name__ == '__main__':
    app.run()
```
