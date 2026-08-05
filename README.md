# 工分 · WorkPoints

一个非常非常简单的**兼职收入可视化系统**，用于记录和可视化我的兼职收入，让牛马当得更有成就感。

## 如何开始

### 在线使用

直接访问：https://w-p.pages.dev/

访问：https://w-p.pages.dev/demo/ 进入演示界面

### 离线本地部署

1. 克隆仓库：`git clone https://github.com/yourusername/workpoints.git`
2. 进入目录：`cd workpoints`
3. 启动本地服务：`npm install && npm run dev`
4. 访问：`http://localhost:4173`

示例：http://localhost:4173/demo

如有需要使用 Google Drive 同步功能请自行部署，并修改为自己的 `index.html`文件第`897`行处的Client ID，才能使用。

Client ID 的申请方式请参考下方：[Google Drive 同步](https://github.com/Tadasuki/Workpoints#google-drive-%E5%90%8C%E6%AD%A5)

## 功能一览

| 功能 | 说明 |
| --- | --- |
| 🕒 时间维度 | 每时段（每次工作）、每日、每月（**工作月**：按设置中的结算日划分，结算日限制为每月 1–28 日）、近 1 / 3 / 7 / 15 / 30 / 60 / 90 日 |
| 📊 图表 | 每日收入曲线、工作月柱状图、近 12 周热力图、时段分布环形图、星期分布条形图、KPI 卡片（含趋势与环比） |
| 📝 记录 | 填写日期、开始或结束时间、任意小数耗时（小时）、单数即可；收入按 `单数 × 单价` 自动计算 |
| 🌐 中英切换 | 顶栏「中 / EN」一键切换 |
| 💱 货币切换 | 顶栏「¥ / $」切换人民币 / 美元显示 |
| 🌙 主题 | 顶栏按钮循环切换 浅色 → 深色 → 跟随系统 |
| 💰 结算 | 设置里可自定义每月结算日（1–28 日），顶部实时显示当前工作月与倒计时 |
| 💾 数据安全 | 数据保存在**你的浏览器本地**；设置里可导出 JSON 备份、导入恢复 |
| ☁️ 云同步 | 设置里连接 Google Drive，可上传备份或从私有应用空间恢复 |

## 使用建议

1. **记录习惯**：每完成一次工作（一个时段），填一笔「单数 + 耗时（小时）」；开始时间和结束时间任选其一即可。
2. **定期备份**：建议每个结算日（20 日）导出一次数据（设置 → 导出数据），以防浏览器缓存被清除。
3. **结算日**：在设置里修改每月结算日，工作月收入图会按数据覆盖范围动态生成，并可在移动端横向滑动查看。
4. **单价调整**：如果单价变化，在设置里修改「每单收入」即可，历史记录会自动按新单价重算。
5. **汇率**：美元显示使用设置中的汇率（默认 1 USD = 6.75 CNY），可根据汇率自行修改。

## Google Drive 同步

我所给网页已内置 Google OAuth Web Client ID，设置中不需要填写 Client ID。

若您自己独立部署，请按下面教程配置 Google Cloud。

### 申请入口

- [创建 Google Cloud 项目](https://console.cloud.google.com/projectcreate)
- [启用 Google Drive API](https://console.cloud.google.com/apis/library/drive.googleapis.com)
- [配置 OAuth consent screen](https://console.cloud.google.com/apis/credentials/consent)
- [创建 OAuth Client ID](https://console.cloud.google.com/apis/credentials)

### 配置步骤

1. 打开「创建 Google Cloud 项目」，新建或选择一个项目。
2. 打开「启用 Google Drive API」，确认当前项目正确后点击启用。
3. 进入 OAuth consent screen：用户类型选择 **External**，填写应用名称、用户支持邮箱和开发者联系邮箱。
4. 在 Scopes 页面继续下一步即可；如果应用处于 **Testing** 状态，在 Test users 中添加自己的 Google 账号。
5. 进入 Credentials → Create credentials → OAuth client ID，Application type 选择 **Web application**。
6. 在 **Authorized JavaScript origins** 添加：`https://你的网站` 或者 `http://localhost:4173`。只填写 Origin，不要添加路径、结尾斜杠等。
7. **Authorized redirect URIs 留空**。本网页使用 Google Identity Services Token 模式，不使用重定向回调。
8. 保存后，网页设置中会直接显示「连接 Google Drive」，点击并完成 Google 授权即可。

如果换了域名，需要把 `https://新的域名` 也加入 Authorized JavaScript origins；

打开网页「设置」后点击「连接 Google Drive」，授权完成后即可使用「同步到 Drive」和「从 Drive 恢复」。数据使用 `drive.appdata` 权限，保存在该应用的私有 Drive 空间，不会出现在普通 Drive 文件列表中。

## 数据说明

- 数据默认通过 `localStorage` 保存在本地，刷新 / 关闭页面不会丢失；连接 Google Drive 后可额外同步到云端。
- `/demo` 使用内置的模拟数据（仅用于体验），不会写入你的真实记录。
- 工作月定义：每月从自定义结算日起算到下一个结算日前一天；结算日限制为每月 1–28 日。
- 页面在线加载 Anthropic Serif 与 Google Fonts 的 Noto Serif SC 600 字重，并提供 Apple touch icon。

## 技术

单文件 HTML（HTML + CSS + JavaScript），无任何外部依赖，纯原生 SVG 图表，可完全离线使用。
