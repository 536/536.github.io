---
title: nodejs-cheat-sheet
date: 2024-03-09 23:59:46
tags:
    - nodejs
    - npm
    - n
    - pnpm
---

## npm

```bash
# 查看npm当前版本
npm -v
# 升级到最新版本
sudo npm install -g npm
# 升级到指定版本
sudo npm install -g npm@8.3.0
```

## n

```bash
# 安装n模块，使用n命令升级node
sudo npm install -g n
# 升级到稳定版
sudo n stable
# 升级到指定版本
sudo n v16.13.1
# 或者
sudo n 16.13.1
```

## pnpm

```bash
sudo npm install -g pnpm
```

## 替换国内源

```bash
npm config set registry https://registry.npmmirror.com
npm config set registry http://registry.npmjs.org
```

## 设置代理

```bash
npm config set proxy=http://127.0.0.1:8087
npm config delete proxy

npm config delete https-proxy
```
