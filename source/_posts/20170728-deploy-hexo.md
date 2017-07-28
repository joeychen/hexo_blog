---
title: '使用Hexo搭建Blog'
date: 2017-07-28 19:06:41
tags: [Hexo]
categories: Hexo
---

# 基本安裝
參考[Hexo官方文件](https://hexo.io/zh-tw/docs/index.html)

## 安裝Hexo
``` bash
$ npm install -g hexo-cli
```
<!-- more -->

## 建立檔案
``` bash
$ hexo init blog
$ cd blog
$ npm install
```

## 安裝hexo-deployer-git以支援Git佈署 
``` bash
$ npm install hexo-deployer-git --save
```
## 修改設定
以下[username]必須代換為個人在GitHub的username
```yaml _config.yml
deploy:
  type: git
  repo: https://[username]@github.com/[username]/[username].github.io.git
  branch: master
```

## 安裝主題
這裡使用第三方主題[next](http://theme-next.iissnan.com/)，一般方式是使用git clone到本地修改，但是我們打算使用[Travis CI](https://travis-ci.org/)自動部署，所以必須先fork一份[hexo-theme-next](https://github.com/iissnan/hexo-theme-next)到自己的repository，使用git submodule增加主題，再把要訂製的設定commit到自己的repository中。

```bash
$ git submodule add git@github.com:[username]/hexo-theme-next.git themes/next
```
blog目錄下應該會出現.gitmodules檔案
```
[submodule "themes/next"]
	path = themes/next
	url = git@github.com:[username]/hexo-theme-next.git	
```

如果已經使用過git clone過hexo-theme-next，可能會遇到以下提示：
```
'theme/next' already exists in the index
```
必須使用以下命令：
```bash
$ git rm -r --cached theme/next
```

# 使用Travis CI 部署
參考[使用 Travis CI 自動發布 hexo 到 Github pages](https://levirve.github.io/2016/hexo-deploy-through-travisci/)

如果Travis CI遇到因權限不足，而無法下載submodule問題
```
Permission denied (publickey).
```
可參考以下gist，增加以下內容到.travis.yml中：
{% gist 9830045 gistfile1.txt %}

