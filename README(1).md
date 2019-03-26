# 和飞信Mac 端之electron开发环境安装流程

### 1.先装个node环境：

node官方网站下载安装包，安装即可。node安装完成，npm也就一起安装好了。
可在终端中使用命令检查安装的版本
```markdown
node -v 
```
如果安装成功会打印出一个node的版本号,例如: v6.10.0
```markdown
npm -v
```
如果安装成功会打印出一个npm的版本号,例如: v3.10.10
以上输出的版本号是举例，真实版本号会因自己选择安装的node安装包版本不同而不同

### 2.(可选)更改npm镜像源(如果你的网络很好也可以不需要更换,使用npm默认的就好.)：

为了下载速度更快将npm的镜像源改成国内淘宝镜像源地址，在终端中执行下边的命令
```markdown
npm config set registry https://registry.npm.taobao.org
```
如果想查看是否更改地址成功可以在终端执行下边的命令
```markdown
cd ~
cat .npmrc
```
如果终端上打印出下边的内容就成功了
```markdown
registry=https://registry.npm.taobao.org
```

### 3.克隆和飞信Mac代码到本地：

复制项目的git地址，比如：git@git.feinno.com:h5/hfx_mac_new.git     
然后打开 终端 (Windows端推荐gitbash) 使用cd命令切换到你想要放项目代码的目录， 
比如想把代码放到文稿里的workspace这个文件夹里，输入下边的命令 

```markdown
cd ~/Documents
```
回车就进入的文稿文件夹，输入下边的命令创建一个文件夹,例如：workspace
```markdown
mkdir workspace
```
回车文件夹就创建了，使用ls命令可以查看一下，创建成功后进入这个文件夹
```markdown
cd workspace
```
clone代码到本地，输入下边的命令并且回车执行
```markdown
git clone git@git.feinno.com:h5/hfx_mac_new.git

PS: git clone 后边那一串是项目git地址，以上是举例子说明。
```

### 4.安装electron开发环境：
多版本并行时,推荐选择安装到项目目录app/node_modules/下 (也可以将electron安装到全局环境)：

在终端执行下边的命令,执行命令的位置需要进入app目录,在app目录下执行以下命令: 
```markdown
Mac: 
npm install electron@1.6.7 -D

Windows:
npm install electron@2.0.8 -D --arch=ia32

Linux:
待补充...
```

#### 如果安装 electron 失败。

解决办法：
    
①.下载electron对应操作平台的zip包和对应的SHASUMS256文件

访问 https://npm.taobao.org/mirrors/electron 手动下载当前系统对应版本的 electron   

例如：electron-v1.6.7-darwin-x64.zip 。(Mac端)

例如：electron-v2.0.8-win32-ia32.zip 。(Windows端)

例如：electron-v2.0.8-linux-x64.zip 。(Linux端)

然后还要下载SHASUMS256.txt，并在文件名后追加版本号，例如修改如：SHASUMS256.txt-2.0.8（详见electron-download）
    
②.将下载的 压缩包 和 SHASUMS256.txt-2.0.8一起放在.electron目录下，      
它的所在位置:

Mac端: ~/.electron

Windows端: 一般是（系统盘）C:\Users\ {YourUserName} \.electron  

Linux端: 待补充...

注意⚠️这是一个点(.)开头的隐藏文件夹，怎么显示隐藏文件夹?

Mac端: Command+shift+.

Windows端: 自己研究去吧。     
  
③.最后在终端重新执行安装命令
终端命令行:
```markdown
Mac: 
npm install electron@2.0.8 -D

Windows: 
npm install electron@2.0.8 -D --arch=ia32

Linux: 
待补充...
```
④.指定版本号安装是因为和飞信Mac端必须使用这个版本，否则代码run不起来，程序启动报错

### 5.安装node_modules依赖包：
在app下执行`npm install`
需要手动把sqlite3放到node_modules下, 这是个需要重新编译的addon, 与npm上边的包略有不同, 编译略显复杂, 下载地址中已经提供了可以直接下载解压替换OK.

如果你 `npm install` 报错
尝试将package-lock.json文件删除
package.json中依赖包可以把`images`和`imageinfo`这两个依赖删掉, 这俩包已经不用了.
然后保存重新执行 `npm install`
如果你想从终端进入node_modules然后在finder中打开, 可以使用以下操作命令:

进入node_modules
```markdown
cd node_modules
```
在finder中打开
```markdown
open ./
```

以上需要下载的文件可以在这里找到 ( 注意对应操作平台和版本号 ) : 
[下载地址](http://git.feinno.com/h5/new-employee-documentation/tree/master/files): http://git.feinno.com/h5/new-employee-documentation/tree/master/files


然后在app下输入命令:
`npm start`
回车即可在本地启动和飞信了。

### 6.Mac项目从现网环境切换到体验环境的操作：

找到这个配置文件: app/lib/v6sdk/client.config--

将client.config文件后边的两道杠去掉即可切换到体验环境

	