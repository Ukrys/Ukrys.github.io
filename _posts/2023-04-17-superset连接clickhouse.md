---
layout:     post
title:      superset连接clickhouse
subtitle:   superset连接clickhouse
date:       2023-04-17
author:     ukrys
header-img: img/post-bg-art.jpg
catalog: 	 true
tags:
    - superset
    - clickhouse
    - data-integration

---

# superset 安装及使用

[toc]

## 1. 安装 miniconda

### 1.1 下载Miniconda

下载地址：`https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh`

### 1.2 安装Miniconda

```bash
bash Miniconda3-latest-Linux-x86_64.sh
```

在安装过程中，出现以下提示时，可以指定安装路径（也可直接Enter默认地址）：

```bash
[/home/ukrys/miniconda3] >>> /opt/module/miniconda3
```

出现`Thank you for installing Miniconda3!` 则安装成功！[![pp4Ohes.png](https://s1.ax1x.com/2023/04/04/pp4Ohes.png)](https://imgse.com/i/pp4Ohes)

加载环境变量配置文件：

```bash
source ~/.bashrc
```

取消激活base环境

```bash
conda config --set auto_activate_base false
```



## 2. 创建环境

### 2.1 配置国内镜像

```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
conda config --set show_channel_urls yes
```

### 2.2 创建superset环境并指定Python3.9

```
 conda create --name superset python=3.9
```

### 2.3 激活superset环境

```
conda activate superset
```



## 3. superset部署

部署前先进入superset环境

```
conda activate superset
```

### 3.1 安装依赖

```
sudo apt-get install -y gcc
sudo apt-get install g++
```

[![pp4X8mj.png](https://s1.ax1x.com/2023/04/04/pp4X8mj.png)](https://imgse.com/i/pp4X8mj)

### 3.2 更新setuptools和pip

```
pip install --upgrade setuptools pip -i https://pypi.douban.com/simple/
```

[![pp4Xtkq.png](https://s1.ax1x.com/2023/04/04/pp4Xtkq.png)](https://imgse.com/i/pp4Xtkq)

### 3.3 安装superset

```
 pip install apache-superset==2.0.0 -i https://pypi.douban.com/simple/
```

[![pp4jVvF.png](https://s1.ax1x.com/2023/04/04/pp4jVvF.png)](https://imgse.com/i/pp4jVvF)

如上图所示即安装成功。

#### 3.3.1 网络问题

[![pp5DNaq.png](https://s1.ax1x.com/2023/04/05/pp5DNaq.png)](https://imgse.com/i/pp5DNaq)

可能会遇到HTTP报错，可以重新尝试下载直至成功。

### 3.4 初始化superset数据库

```
superset db upgrade
```

[![pp4jLZ9.png](https://s1.ax1x.com/2023/04/04/pp4jLZ9.png)](https://imgse.com/i/pp4jLZ9)

如图 成功

#### 3.4.1 踩到的坑

**1：**ModuleNotFoundError: No module named 'cryptography.hazmat.backends.openssl.x509'

[![pp4j6Kg.png](https://s1.ax1x.com/2023/04/04/pp4j6Kg.png)](https://imgse.com/i/pp4j6Kg)

- 原因是 `cryptography`库的等级太高了

  ```
  pip uninstall cryptography
  pip install cryptography==3.3.2 -i https://pypi.douban.com/simple/
  ```

**2：**“Could not locate a Flask application. Use the 'flask --app' option, 'FLASK_APP' environment variable, or a 'wsgi.py' or 'app.py' file in the current directory.”
[![pp4jgbj.png](https://s1.ax1x.com/2023/04/04/pp4jgbj.png)](https://imgse.com/i/pp4jgbj)

- 执行以下命令即可

  ```
  export FLASK_APP=superset
  ```

**3：**ModuleNotFoundError: No module named 'werkzeug.wrappers.etag'

- 这个是在 superset 2.0 版本出现的bug，通过降低Werkzeug的版本解决

  ```
  python -m pip uninstall -y Werkzeug
  python -m pip install Werkzeug==2.0.3
  ```

**4：**ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
flask 2.2.3 requires Werkzeug>=2.2.2, but you have werkzeug 2.0.3 which is incompatible.

[![pp4j5GV.png](https://s1.ax1x.com/2023/04/04/pp4j5GV.png)](https://imgse.com/i/pp4j5GV)

- Flask版本过高 降低版本

  ```
  python -m pip uninstall -y Flask
  python -m pip install Flask==2.0.3
  ```

**5：**“ModuleNotFoundError: No module named 'wtforms.ext'”

- 这个是因为WTForms 3.0的版本去掉了ext，需要降低WTForms的版本到2.3.3

  ```
  python -m pip uninstall -y WTForms
  python -m pip install WTForms==2.3.3
  ```

### 3.5 创建管理员用户

```
export FLASK_APP=superset
superset fab create-admin
```

[![pp4jvPx.png](https://s1.ax1x.com/2023/04/04/pp4jvPx.png)](https://imgse.com/i/pp4jvPx)

注意： username默认为admin，请记住Password！！！后续有用

### 3.6 superset初始化

```
superset init
```

[![pp4vCse.png](https://s1.ax1x.com/2023/04/04/pp4vCse.png)](https://imgse.com/i/pp4vCse)



## 4. superset启动

### 4.1 安装gunicorn

```
pip install gunicorn -i https://pypi.douban.com/simple/
```

[![pp4vPqH.png](https://s1.ax1x.com/2023/04/04/pp4vPqH.png)](https://imgse.com/i/pp4vPqH)

### 4.2 启动Superset

确保当前conda环境为superset

``` 
gunicorn --workers 5 --timeout 120 --bind 127.0.0.1:8080  "superset.app:create_app()" --daemon 

--workers：指定进程个数
--timeout：worker进程超时时间，超时会自动重启
--bind：绑定本机地址，即为Superset访问地址
--daemon：后台运行
```

### 4.3 登录superset

浏览器打开输入网址 `localhost:8080` 。输入**步骤3.5**创建的账号密码进行登录 

[![pp4vKsg.png](https://s1.ax1x.com/2023/04/04/pp4vKsg.png)](https://imgse.com/i/pp4vKsg)

[![pp4vGiq.png](https://s1.ax1x.com/2023/04/04/pp4vGiq.png)](https://imgse.com/i/pp4vGiq)

登陆成功！

### 4.4 关闭superset

```
ps -ef | awk '/superset/ && !/awk/{print $2}' | xargs kill -9
```

## 5. 连接clickhouse

### 5.1 安装驱动

```
pip install clickhouse-connect
```

[![pp5MHyD.png](https://s1.ax1x.com/2023/04/04/pp5MHyD.png)](https://imgse.com/i/pp5MHyD)

### 5.2 页面操作

依次点击右上角 **＋** → **Data** → **Connect database**  

[![pp5Mdds.png](https://s1.ax1x.com/2023/04/04/pp5Mdds.png)](https://imgse.com/i/pp5Mdds)

依次填入clickhouse信息，点击 CONNECT 进行连接。

[![pp5M4F1.png](https://s1.ax1x.com/2023/04/04/pp5M4F1.png)](https://imgse.com/i/pp5M4F1)

添加成功后，点击上方导航栏 **SQL Lab** → **SQL Editor**

选择要操作的表，并填入SQL语句

[![pp5QMXF.png](https://s1.ax1x.com/2023/04/05/pp5QMXF.png)](https://imgse.com/i/pp5QMXF)

生成结果选择想要呈现的图表形式。

## 6. 可视化展示

可视化展示部分我们在在线数据和离线表数据中各选择了一组表，展示**相应维度随时间变动的特征**，并作出简要分析。

### 6.1 在线数据



[![pp5QPOg.png](https://s1.ax1x.com/2023/04/05/pp5QPOg.png)](https://imgse.com/i/pp5QPOg)

上图描述了2021年01月银行账目每日的流水额。可以发现 每日流水总额是呈周期性波动的。查询日历可以发现 1月16-17日、1月23-24日为周末。可以推断大概是由于周末部分企业财务人员休息，每一个周一工作日，流水额都会激增。

### 6.2 离线表数据

| [![pp5NZtg.png](https://s1.ax1x.com/2023/04/05/pp5NZtg.png)](https://imgse.com/i/pp5NZtg) | [![pp5N1BV.png](https://s1.ax1x.com/2023/04/05/pp5N1BV.png)](https://imgse.com/i/pp5N1BV) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

以上是分期付款金额随不同时间粒度变化的曲线。可以发现每年的年底和年初，金额都会激增；而年中始终处在低水平波动。银行应在每年年末做好相应资金流的准备，以防出现资金短缺的情况。