# App Downloads

开发者本人的应用安装包分发站，通过 GitHub Pages 提供**长期固定**的直链下载。

## 目录约定

```
/
├─ index.html                      # 站点首页：列出所有项目
└─ <项目名>/
   ├─ index.html                   # 该项目的下载落地页
   ├─ <产品名>.apk                 # 固定文件名：始终指向最新版本
   └─ icon.png                     # 该项目的图标
```

**每个项目的落地页放在自己的目录里**，站点根目录只做项目导航。

| 项目 | 下载页 | 安装包直链 |
| --- | --- | --- |
| 鱼缸管家 AquaKeeper | `https://cq-tyl.github.io/app-downloads/aquakeeper/` | `https://cq-tyl.github.io/app-downloads/aquakeeper/AquaKeeper.apk` |

新增项目：新建以项目名命名的目录，放入 `index.html`、`<产品名>.apk`、`icon.png` 三件套，再到根目录 `index.html` 复制一张项目卡片即可。

## 命名原则

安装包一律**不含版本号**（如 `AquaKeeper.apk`）。每次发版只需用新包覆盖同名文件，这样 App 内分享文案、文档、外链都不需要跟着改；版本信息写在落地页的版本标签里。

## 发版流程

```bash
git clone https://github.com/cq-tyl/app-downloads.git
cp 新包.apk aquakeeper/AquaKeeper.apk        # 覆盖同名文件
# 同步更新 aquakeeper/index.html 里的版本 / 大小 / 日期
git add -A && git commit -m "更新 AquaKeeper 到 x.y.z"
git checkout --orphan fresh && git add -A && git commit -m "发布分组梳理"
git branch -M fresh main && git push -f origin main
```

> 每次覆盖同名 APK 会在 git 历史里多存一份对象，因此统一采用 **orphan 分支 + 强推**，让 main 始终只有一个最新提交，仓库体积维持在单个安装包的量级。

## 限制

- 单个文件不超过 100 MB（GitHub 限制）
- Pages 站点建议总容量控制在 1 GB 以内
- Android 安装需允许「未知来源」；App 内置浏览器请改用系统浏览器下载