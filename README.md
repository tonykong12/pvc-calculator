# PVC 管材价格计算器 (PWA)

基于管壁截面积与原料密度的 PVC 管材每米价格计算工具，支持手机端安装为桌面应用。

## 功能

- 输入内径、外径、密度、原料价等参数
- 自动计算每米重量和每米价格
- 6 步详细计算过程展示
- PWA 支持：离线可用、添加到主屏幕

## 文件结构

```
pvc-calculator/
├── index.html          # 主页面（响应式手机界面）
├── manifest.json       # PWA 配置
├── service-worker.js   # 离线缓存
├── icon-192.png       # 应用图标 192×192
├── icon-512.png       # 应用图标 512×512
└── README.md
```

---

## 部署方案

以下三种方案任选其一，推荐 **GitHub Pages**（免费、零配置、自带 HTTPS）。

### 方案一：GitHub Pages（推荐）

1. 将 `pvc-calculator/` 文件夹推送到 GitHub 仓库：

```bash
cd pvc-calculator
git init
git add .
git commit -m "init: PVC价格计算器 PWA"
git remote add origin https://github.com/你的用户名/仓库名.git
git branch -M main
git push -u origin main
```

2. 在 GitHub 仓库页面进入 **Settings → Pages**
3. **Source** 选择 `Deploy from a branch`
4. **Branch** 选择 `main`，目录选 `/ (root)`
5. 点击 **Save**，等待 30 秒
6. 访问 `https://你的用户名.github.io/仓库名/`

> **提示**：GitHub Pages 自动提供 HTTPS，PWA 的 Service Worker 在 HTTPS 下才能正常工作。

---

### 方案二：Vercel

1. 在 [vercel.com](https://vercel.com) 注册（支持 GitHub 一键登录）
2. 点击 **New Project** → 导入 GitHub 仓库
3. 无需任何配置（Vercel 自动识别静态站点）
4. 点击 **Deploy**
5. 获得 `https://你的项目名.vercel.app` 地址

```bash
# 或通过 CLI 部署
npm i -g vercel
cd pvc-calculator
vercel
```

---

### 方案三：Netlify

1. 在 [netlify.com](https://netlify.com) 注册
2. 点击 **Add new site → Deploy manually**
3. 将 `pvc-calculator/` 文件夹拖入上传区域
4. 等待部署完成，获得 `https://xxx.netlify.app` 地址

```bash
# 或通过 CLI 部署
npm i -g netlify-cli
cd pvc-calculator
netlify deploy --prod
```

---

### 方案四：Cloudflare Pages

1. 在 [pages.cloudflare.com](https://pages.cloudflare.com) 注册
2. 连接 GitHub 仓库
3. 构建设置留空（纯静态站点无需构建命令）
4. 输出目录留空（根目录即为站点根目录）
5. 点击部署，获得 `https://xxx.pages.dev` 地址

---

### 方案五：本地快速预览

```bash
# Python（macOS 自带）
cd pvc-calculator
python3 -m http.server 8080

# 然后用手机浏览器访问 http://你的电脑IP:8080
# 查看本机 IP：ifconfig | grep "inet "
```

---

## 手机使用

### 打开网页
手机浏览器访问部署后的 URL 即可使用。

### 安装到桌面（PWA）
| 平台 | 操作 |
|---|---|
| **iPhone Safari** | 打开页面 → 底部分享按钮 → "添加到主屏幕" |
| **Android Chrome** | 打开页面 → 地址栏右侧"安装"图标，或底部安装提示条 |

安装后以全屏独立窗口运行，**无网络也能使用**。

---

## 二维码生成

部署后将你的 URL 粘贴到以下任一工具生成二维码：

| 工具 | 地址 |
|---|---|
| 草料二维码 | https://cli.im/text |
| QR Code Generator | https://www.qr-code-generator.com |
| 本地命令 | `python3 -c "import qrcode; qrcode.make('你的URL').show()"` |

---

## 计算公式

```
① 外径平方 = 外径²
② 内径平方 = 内径²
③ 每米重量 = (外径² - 内径²) × 密度 × 0.82 / 1000   (kg/m)
④ 公斤价   = 原料价 × 价格系数
⑤ 每米价格 = 每米重量 × 公斤价                       (元/m)
```