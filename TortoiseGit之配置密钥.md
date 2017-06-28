#### TortoiseGit
```
使用扩展名为ppk的密钥，而不是ssh-keygen生成的rsa密钥。
使用命令ssh-keygen -C "邮箱地址" -t rsa产生的密钥在TortoiseGit中不能用。
而基于git的开发必须要用到rsa密钥，因此需要用到TortoiseGit的putty key generator工具来生成既适用于git的rsa密钥也适用于TortoiseGit的ppk密钥，
具体配置步骤如下：
```
#### 1）运行开始菜单中的puttygen程序，如下图示

![](http://img.blog.csdn.net/20140106141805171?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYmVuZGFuYmFpY2hpMTk4OQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
#### 2）点击“Generate”按钮，鼠标在上图的空白地方来回移动直到进度条完毕，就会自动生一个随机的key，如下图示
![](http://img.blog.csdn.net/20140106141830343?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYmVuZGFuYmFpY2hpMTk4OQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
```
如有需要，可以为密钥设置对应的访问密码，就是修改上图中“Key passphrase”和“Confirm passphrase”的值。
```
#### 3）将上图中多行文本框的内容全选、复制，并粘贴到git账户的 SSH public key中，这就是适用于git的公钥。(文本框有滚动条)
```
对于自己搭建的linux服务器,公钥也是放在 /home/git/.ssh/authorized_keys
```
#### 4）点击上图中的“Save private key”按钮,将生成的key保存为适用于TortoiseGit的私钥（扩展名为.ppk）。
#### 5）运行TortoiseGit开始菜单中的Pageant程序，程序启动后将自动停靠在任务栏中，图标显示为，双击该图标，弹出key管理列表，如下图示
![](http://img.blog.csdn.net/20140106141906906?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYmVuZGFuYmFpY2hpMTk4OQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
#### 6）点击上图中的“Add Key”按钮，将第4步保存的ppk私钥添加进来，关闭对话框即可
