# 需求

从两个主线理解 StackHub 的需求：

- 应用生命周期管理：寻找、安装、发布、停止、卸载、升级等软件全生命周期。
- 基础设施运维管理：安全、存储、文件、容器、监控等系统管理

## 应用生命周期

### 业务需求

#### 寻找

用户可以通过两个入口寻找应用：

- 应用商店：采用一级分类的方式展现应用，并支持**筛选+搜索**的方式以便于用户检索
- Docker 镜像仓库：检索 Docker 镜像仓库，找到对应的应用

#### 安装

- 用户自主安装应用，后端按顺序依次启动目标应用
- 启动应用之前先进行资源约束判断，不符合条件的目标应用不予安装
- 与安装有关的状态：安装中、运行中、安装失败、反复重启、已停止

#### 发布

- 以域名或端口的方式，将运行中的应用发布出去，供外部用户访问。
- 自助设置 HTTPS，上传或更新证书

#### 停止

将应用服务停止

#### 卸载

卸载应用并删除数据

#### 升级

升级应用，如果升级失败会自动回滚到升级之前的状态

#### 恢复

在已有的完整备份的基础，恢复应用。

可能存在两种情况：

- 覆盖现有应用
- 恢复成一个新的应用

#### 克隆

克隆一个已经存在的应用，命名为新应用

### 技术需求

#### 模板编排

应用的底层编排 100% 以 Docker Compose 语法作为编排语言

#### 多语言

- 前端支持 i18n
- 后端接口支持英文

#### 用户管理

- 支持多个用户，用户角色分为普通用户和管理员用户
- 普通用户可以创建和管理自己的应用，不可以删除他人的应用

#### UI 自适应

UI 自适应各种屏幕尺寸

#### 2FA

引入一种双重登录策略

#### 商店基础设置

- 商店 Logo 可自定义
- 语言、时区可选
- 绑定域名
- SMTP 信息填写

#### 通知

- SMTP 邮件通知

#### 商店更新

商店支持在线更新提示和在线更新

#### API

支持生成 API Tokens

#### CLI

基于 API 的 CLI

#### 仓库管理

默认以 DockerHub 作为镜像仓库，支持自建仓库并同步 DockerHub 镜像

#### 安装程序

一键自动化安装程序，类似：

```
curl https://websoft9.github.io/StackHub/install/install.sh | bash
```

主要步骤包括：

1. Check 硬件、操作系统、cpu 架构
2. 安装依赖包
3. 安装 docker
4. 下载各源码包
5. 启动个源码对应服务

## 基础设施运维

### SSH 终端

Web-Based SSH 终端

### 文件管理器

Web-Based 文件管理器

### 存储管理

- 支持接入第三方对象存储

### 备份

备份完整的应用数据：

- 自定义备份时间区间
- 自动备份可取消
- 备份可以管理：删除、下载等

### 容器管理

可视化的容器管理，包括：拉镜像、创建/删除/停止容器、SSH 进入容器、向容器上传文件等

### 系统监控

- 监控容器的 CPU，内存和存储消耗情况
- 监控系统的 CPU，内存和存储消耗情况