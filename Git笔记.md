# Git笔记

***

## 身份信息配置

### 配置用户名

`git config --global user.name "xxx"`

### 配置邮箱

`git config --global user.email "xxxx@xx.com"`

### 检查身份

`git config user.name`

`git config user.email`

`git config -l`

### 修改身份

重复配置用户名和配置邮箱

***

## 常用命令

### 初始化仓库

`git init`

### 添加文件到缓冲区/追踪

`git add .`

### 提交到仓库/创建快照

`git commit -m "注释"`

### 提交到 Github

```bash
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:r1cardohj/someNote.git
git push -u origin main
```



