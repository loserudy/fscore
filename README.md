# F-SCORE PWA 部署包

把 F-SCORE 做成手机可离线刷题的网页应用（安卓 + iOS），部署到 GitHub Pages。

## 这个目录里有什么

| 文件 | 作用 |
|------|------|
| `index.html` | 你要放进来的主文件（导出的题库 HTML，重命名为 index.html） |
| `sw.js` | Service Worker，负责离线缓存 |
| `manifest.json` | PWA 配置（应用名/图标/全屏） |
| `icon-192.png` / `icon-512.png` | 应用图标 |
| `README.md` | 本说明 |

## 第一步：导出题库 HTML

1. 双击打开 `F-SCORE.min.html`（管理版）。
2. 点「导入 / 替换题库」，选你的题库 Excel（如 `result.xlsx` 或 `sw.xlsx`）。
3. 导入成功后，点「**导出查询版**」（含查询/练习/抽题/考试四个功能）或「**导出考试版**」（仅考试）。
4. 浏览器会下载一个 `F-SCORE_查询版_xxxx.html` 文件。

## 第二步：放入部署包

1. 把下载的 HTML 文件**重命名为 `index.html`**。
2. 放进这个 `pwa-deploy` 文件夹（替换原来的占位文件）。

## 第三步：部署到 GitHub Pages

**方式 A：网页端上传（推荐，无需命令行）**

1. 登录 github.com → 右上角 `+` → `New repository`。
2. 仓库名随便填（如 `fscore`），选 **Public**，点 `Create repository`。
3. 进入仓库，点 `uploading an existing file` 链接。
4. 把 `pwa-deploy` 里的 5 个文件全部拖进去，点 `Commit changes`。
5. 仓库页点 `Settings` → 左侧 `Pages` → `Branch` 选 `main` / 根目录 → `Save`。
6. 等 1~2 分钟，页面顶部会显示地址：`https://你的用户名.github.io/fscore/`。

**方式 B：git 命令**

```bash
git init && git add . && git commit -m "fscore pwa"
git remote add origin https://github.com/你的用户名/fscore.git
git push -u origin main
# 然后同样去 Settings → Pages 开启
```

## 第四步：手机添加到主屏幕（离线刷题）

1. 手机打开 `https://你的用户名.github.io/fscore/`（第一次需要联网）。
2. **安卓**：Chrome 菜单 → 「添加到主屏幕」。
3. **iOS**：Safari 分享按钮 → 「添加到主屏幕」。
4. 之后从主屏幕图标进入，**断网也能刷题**（首次联网缓存后）。

## 更新题库时

1. 重新导出 `index.html`（同上步骤一）。
2. 把 `sw.js` 里的 `const CACHE = 'fscore-v1'` 改成 `'fscore-v2'`（版本号 +1，否则浏览器用旧缓存）。
3. 重新上传这两个文件，刷新手机页面即可。

## 注意

- 部署后链接是**公开的**，知道链接的人都能访问。
- 题库是加密内置的，但密钥在客户端，懂技术的人仍可能破解（和单文件版一样，防普通用户不防高手）。
