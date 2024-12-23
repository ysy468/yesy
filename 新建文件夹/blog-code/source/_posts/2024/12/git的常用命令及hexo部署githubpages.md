---
title: git的常用命令及hexo部署githubpages
tags: [blog, git, github, hexo]
date: 2024-12-13 23:01:00
updated: 2024-12-13 23:01:00
author: xulong
---
# Git 操作示例  
以 `https://github.com/xulong0826/blog-code` 为例  

## 克隆远程仓库  
```bash
git clone https://github.com/xulong0826/blog-code
```

## 拉取更新  
```bash
git pull
```

## 查看远程仓库地址  
```bash
git remote -v
```

## 修改远程仓库地址  
### 删除指定的远程仓库地址：  
```bash
git remote set-url --delete (--push) origin https://github.com/xulong0826/blog-code.git
```

### 添加新的远程仓库地址：  
```bash
git remote set-url --add origin https://github.com/xulong0826/blog-code.git
```

## 添加文件到暂存区  
### 添加所有更改：  
```bash
git add .
```

### 单独添加指定文件：  
```bash
git add <文件名/文件夹>  # 如 xx.md 或 xx.jpg
```

## 提交更改  
```bash
git commit -m "update the project"
```

## 推送更改到远程分支  
```bash
git push origin main
```

### 注意：
- 本地分支：`origin`  
- 远程分支：`main`

---

# Hexo 配置  

## 安装 Hexo Git 部署插件  
```bash
npm install hexo-deployer-git --save
```

## 配置 `_config.yml` 文件  
在 `_config.yml` 文件中添加以下内容：  
```yaml
deploy:
  type: git
  repo: https://github.com/xulong0826/blog
  branch: main
```
## 部署 
```bash
# 安装项目依赖文件
npm install 
# 清理生成的缓存和旧文件
npm run clean
# 构建并发布静态博客
npm run deploy
(hexo deploy)
```

通过以上操作，你可以顺利完成 Git 和 Hexo 的配置与更新部署。如果还有其他问题，可以随时补充说明！
