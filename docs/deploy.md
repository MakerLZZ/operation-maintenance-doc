# Deploy
``` bash
# 部署项目相关知识
```

## 安装node
### nvm
``` bash
# 通过使用```nvm```来安装和管理```node```版本，[官网地址](https://github.com/nvm-sh/nvm)
```

#### 安装nvm
1.进入官网查看```README.md```文件如下模块
```
Installation and Update
```
2.输入如下命令：
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
```
或者如下命令：
```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
```
即可安装```nvm```，如果不是```ubuntu```不能识别```curl```和```wget```命令，先安装```yum```然后输入如下命令：
```
yum install curl wget
```
然后再安装```nvm```即可
***

#### 配置nvm环境变量
1.进入```nvm```安装目录
```
cd ~/.nvm
```
2.编辑```.bash_profile```文件，没有则为新建
```
vim .bash_profile
```
3.编写如下代码，按照安装时所给提示编写（```$HOME```即是会变化的）
```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
```
4.保存并退出以后```nvm```命令即可使用了
***

### 使用nvm安装node
```nvm install stable``` 安装```node```最新稳定版

其他```nvm```相关常用命令
```bash
nvm install ## 安装指定版本，可模糊安装，如：安装v4.4.0，既可nvm install v4.4.0，又可nvm install 4.4
nvm uninstall ## 删除已安装的指定版本，语法与install类似
nvm use ## 切换使用指定的版本node
nvm ls ## 列出所有安装的版本
nvm ls-remote ## 列出所以远程服务器的版本（官方node version list）
nvm current ## 显示当前的版本
nvm alias ## 给不同的版本号添加别名
nvm unalias ## 删除已定义的别名
nvm reinstall-packages ## 在当前版本node环境下，重新全局安装指定版本号的npm包
```

## 安装git
1.```ubuntu```使用如下命令即可安装
```
apt-get install git
```
2.```centOS```使用如下命令
```
yum install git
```
3.克隆远程仓储代码到服务器
```bash
git clone xxx # xxx为代码地址
```

## 搭建node静态站点部署前端项目（待完善）
