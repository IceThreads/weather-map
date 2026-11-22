# 天气图鉴 · 中国气象地图 — 介绍与下载页

一个纯静态、无构建步骤的展示网站，包含：

- `index.html`：项目介绍、功能、八日时间轴交互演示、搜索、截图画廊、FAQ。
- `download.html`：人机验证 → 选择平台（Windows / Android）→ 选择蓝奏云 / 123 云盘 / GitHub / 本站直链。
- 全站毛玻璃控件、滚动揭示、卡片倾斜、按钮涟漪、悬浮设备、数字增长、时间轴自动播放等动效。
- 默认自动跟随系统主题，也可以点击导航栏主题按钮在“自动 / 明亮 / 黑暗”之间切换，选择会保存在 `localStorage`。

## 本地预览

```powershell
cd weather-atlas-site
python -m http.server 8767
```

然后打开 <http://127.0.0.1:8767/index.html>。直接双击 `index.html` 也能看，但使用本地 HTTP 服务可以保证下载链接与浏览器行为一致。

## 配置云盘下载地址

云盘链接不会是凭空生成的，需要发布者上传文件后填写。打开 `download-config.js`：

```js
links: {
  lanzou: {
    windows: "https://wwi.lanzoup.com/xxxx",
    android: "https://wwi.lanzoup.com/yyyy"
  },
  pan123: {
    windows: "https://www.123pan.com/s/xxxx",
    android: "https://www.123pan.com/s/yyyy"
  },
  github: {
    windows: "https://github.com/you/repo/releases/download/v1.2.0/...",
    android: "https://github.com/you/repo/releases/download/v1.3.0/..."
  }
}
```

- 留空的通道会显示“待配置”，点击后提示如何填写。
- `files` 中的 `direct` 是随站点提供的本地直链，默认已经可用。
- 版本号、文件大小、SHA256 也在 `files` 中，可按新版本替换。

## 目录

```text
weather-atlas-site/
  index.html
  download.html
  styles.css
  core.js              主题、导航、滚动揭示、涟漪、数字动效
  home.js              首页时间轴演示、FAQ、视差
  download.js          人机验证、平台切换、云盘/直链逻辑
  download-config.js   云盘下载地址与文件元数据
  assets/              截图、图标
  downloads/           Windows EXE + Android APK（本站直链）
```

## 说明

- 人机验证是**纯前端交互验证**（拖动滑块），用于阻挡误触和非常简单的自动化，不是服务端防刷系统；正式对外发布如果面对恶意刷量，建议接入服务端验证。
- 下载页的蓝奏云、123 云盘和 GitHub 地址需要发布者自行上传并配置，仓库不包含这些账号或分享链接。
- 数据展示为项目内置的八日天气快照，基准日 2026-11-22；页面本身不请求实时天气接口。
- 截图与安装包：Windows v1.2.0；Android v1.3.0 流畅优化版（APK 约 1.6 MB）。
