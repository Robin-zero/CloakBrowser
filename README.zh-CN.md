<p align="center">
<img src="https://i.imgur.com/cqkp6fG.png" width="500" alt="CloakBrowser">
</p>

<p align="center">
<a href="https://pypi.org/project/cloakbrowser/"><img src="https://img.shields.io/pypi/v/cloakbrowser" alt="PyPI"></a>
<a href="https://www.npmjs.com/package/cloakbrowser"><img src="https://img.shields.io/npm/v/cloakbrowser" alt="npm"></a>
<a href="LICENSE"><img src="https://img.shields.io/github/license/cloakhq/cloakbrowser?v=1" alt="License"></a>
<a href="https://github.com/CloakHQ/CloakBrowser"><img src="https://img.shields.io/github/last-commit/cloakhq/cloakbrowser" alt="Last Commit"></a>
<br>
<a href="https://github.com/CloakHQ/CloakBrowser"><img src="https://img.shields.io/github/stars/cloakhq/cloakbrowser" alt="Stars"></a>
<a href="https://pypi.org/project/cloakbrowser/"><img src="https://img.shields.io/pepy/dt/cloakbrowser?label=pypi&logo=pypi&logoColor=white" alt="PyPI Downloads"></a>
<a href="https://www.npmjs.com/package/cloakbrowser"><img src="https://img.shields.io/npm/dt/cloakbrowser?label=npm&logo=npm&logoColor=white" alt="npm Downloads"></a>
<a href="https://hub.docker.com/r/cloakhq/cloakbrowser"><img src="https://img.shields.io/docker/pulls/cloakhq/cloakbrowser?label=docker&logo=docker&logoColor=white" alt="Docker Pulls"></a>
</p>

<p align="center">
<a href="https://ko-fi.com/cloakhq"><img src="https://ko-fi.com/img/githubbutton_sm.svg" alt="Support on Ko-fi"></a>
</p>

<p align="center">
<a href="./README.md">English</a>
<span>| 简体中文</span>
</p>

<br>

<h3 align="center">可通过所有机器人检测测试的隐身 Chromium。</h3>

<table><tr><td>
不是打补丁的配置。不是 JS 注入。它是真正的 Chromium 二进制，并且在 C++ 源码层修改了浏览器指纹。反机器人系统会把它判定为普通浏览器，因为它<em>本来就是</em>普通浏览器。
</td></tr></table>

<br>

<p align="center">
<img src="https://i.imgur.com/IvB0It7.gif" width="600" alt="Cloudflare Turnstile — 3 项测试通过">
<br><em>Cloudflare Turnstile — 3 项实时测试通过（有头模式，macOS）</em>
</p>

<br>

<p align="center">
适用于 Python 和 JavaScript 的 Playwright/Puppeteer 即插即用替代方案。<br>
API 相同，代码相同，只需要替换 import。<strong>3 行代码，30 秒解除拦截。</strong>
</p>

- **58 个源码级 C++ 补丁** — 覆盖 canvas、WebGL、音频、字体、GPU、屏幕、WebRTC、网络时序、自动化信号、CDP 输入行为
- **`humanize=True`** — 提供类似真人的鼠标轨迹、键盘时序和滚动模式。一个标志位即可通过行为检测
- **0.9 的 reCAPTCHA v3 分数** — 接近真人水平，服务端已验证
- **通过 Cloudflare Turnstile、FingerprintJS、BrowserScan** — 已在 30+ 个检测站点验证
- **自动更新的二进制** — 后台检查更新，始终保持最新隐身构建
- **`pip install cloakbrowser`** 或 **`npm install cloakbrowser`** — 自动下载二进制，零配置
- **免费且开源** — 无订阅，无使用限制

**立即试用** — 无需安装：
```bash
docker run --rm cloakhq/cloakbrowser cloaktest
```

**Python：**
```python
from cloakbrowser import launch

browser = launch()
page = browser.new_page()
page.goto("https://protected-site.com")  # 不再被拦截
browser.close()
```

**JavaScript（Playwright）：**
```javascript
import { launch } from 'cloakbrowser';

const browser = await launch();
const page = await browser.newPage();
await page.goto('https://protected-site.com');
await browser.close();
```

同样支持 Puppeteer：`import { launch } from 'cloakbrowser/puppeteer'`（[详情](#puppeteer)）

## 安装

**Python：**
```bash
pip install cloakbrowser
```

**JavaScript / Node.js：**
```bash
# 配合 Playwright
npm install cloakbrowser playwright-core

# 配合 Puppeteer
npm install cloakbrowser puppeteer-core
```

首次运行时，会自动下载隐身 Chromium 二进制（约 200MB，缓存到本地）。

**可选：** 根据代理 IP 自动检测时区和语言环境：
```bash
pip install cloakbrowser[geoip]
```

**从 Playwright 迁移？** 只需改一行：

```diff
- from playwright.sync_api import sync_playwright
- pw = sync_playwright().start()
- browser = pw.chromium.launch()
+ from cloakbrowser import launch
+ browser = launch()

page = browser.new_page()
page.goto("https://example.com")
# ... 其余代码保持不变
```

> ⭐ **Star** 支持项目 — **[Watch releases](https://github.com/CloakHQ/CloakBrowser/subscription)**，在有新版本发布时收到通知。

## 浏览器配置文件管理器

这是 Multilogin、GoLogin 和 AdsPower 的自托管替代方案。你可以创建带有唯一指纹、代理和持久会话的浏览器配置文件，并通过 noVNC 在浏览器中启动和操作它们。

```bash
docker run -p 8080:8080 -v cloakprofiles:/data cloakhq/cloakbrowser-manager
```

打开 [http://localhost:8080](http://localhost:8080)。创建一个配置文件。点击 **Launch**。完成。

→ **[CloakBrowser Manager](https://github.com/CloakHQ/CloakBrowser-Manager)** — 免费、开源（MIT）

---

## 最新版本：v0.3.30（Chromium 146.0.7680.177.5）

- **58 项指纹补丁** — 提升 Linux 和 Windows 上的渲染一致性，修正 GPU / 显示 / 图形参数，使其与原生 Chrome 146 配置一致
- **Windows 原生 GPU 透传** — 直接透传真实硬件值，而不是伪造，更符合真实浏览器行为
- **HTTP 代理内联凭证** — 新增网络层支持，可直接使用带内联认证信息的代理
- **`extension_paths`** — 所有 launch 函数都可加载 Chrome 扩展
- **Humanize 可操作性** — 在执行人类化操作前，自动等待元素可见、可用且稳定
- **按调用覆盖 `human_config`** — 可在单次方法调用上覆盖 humanize 设置
- **可组合的 JS 辅助函数** — `buildLaunchOptions()` 和 `humanizeBrowser()`，用于自定义 Playwright 集成
- **原生 SOCKS5 代理** — `proxy="socks5://user:pass@host:port"` 可直接用于所有 launch 函数，支持 Python 和 JS。QUIC/HTTP3 可通过 SOCKS5 的 UDP ASSOCIATE 转发
- **移除代理信号** — DNS / connect / SSL 时序清零，去除代理缓存头，移除 `Proxy-Connection` 头泄漏
- **升级到 Chromium 146** — 所有补丁从 145.0.7632.x 重新移植到 146.0.7680.177
- **WebRTC IP 伪装** — `--fingerprint-webrtc-ip=auto` 会解析代理出口 IP，并伪造 WebRTC ICE 候选地址。使用 `geoip=True` 时会自动注入（无需额外网络请求）
- **`humanize=True`** — 一个标志即可让所有鼠标、键盘和滚动交互看起来像真人。包含 Bézier 曲线、逐字符输入、真实滚动模式
- **零标志也可隐身** — 二进制会在启动时自动生成随机指纹种子，无需任何配置
- **根据代理 IP 自动匹配时区和语言环境** — `launch(proxy="...", geoip=True)` 可自动检测时区与语言
- **持久配置文件** — `launch_persistent_context()` 在会话之间保留 cookies 和 localStorage，并绕过无痕模式检测

完整细节见 [CHANGELOG.md](CHANGELOG.md)。

## 为什么选择 CloakBrowser？

- **配置级补丁很脆弱** — `playwright-stealth`、`undetected-chromedriver` 和 `puppeteer-extra` 依赖 JS 注入或标志位调整。每次 Chrome 更新都可能失效，而且反机器人系统能直接检测这些补丁本身。
- **CloakBrowser 修改的是 Chromium 源码** — 指纹在 C++ 层被修改并编译进二进制。检测站点看到的是一个真实浏览器，因为它确实是真实浏览器。
- **源码级隐身** — C++ 补丁在二进制层处理指纹（GPU、屏幕、UA、硬件信息上报）。没有 JavaScript 注入，也没有配置层 hack。多数隐身工具只修补表层。
- **在任何环境下行为一致** — 本地、Docker 和 VPS 上的表现完全一致，不需要环境特定补丁或配置。
- **兼容 AI Agent 和自动化框架** — 可直接作为 browser-use、Crawl4AI、Scrapling、Stagehand、LangChain、Selenium 等框架的隐身浏览器。见 [集成](#framework-integrations)。

CloakBrowser 不负责解 CAPTCHA，而是阻止 CAPTCHA 出现。它不内置打码服务，也不内置代理轮换机制。你只需要使用自己的代理，并继续沿用熟悉的 Playwright API。

## 测试结果

所有测试都基于真实在线检测服务验证。最后测试时间：2026 年 4 月（Chromium 146）。

| 检测服务 | 原生 Playwright | CloakBrowser | 备注 |
|---|---|---|---|
| **reCAPTCHA v3** | 0.1（机器人） | **0.9**（真人） | 服务端已验证 |
| **Cloudflare Turnstile**（非交互） | 失败 | **通过** | 自动通过 |
| **Cloudflare Turnstile**（托管模式） | 失败 | **通过** | 单击即可 |
| **ShieldSquare** | 被拦截 | **通过** | 生产站点 |
| **FingerprintJS** 机器人检测 | 被检测到 | **通过** | demo.fingerprint.com |
| **BrowserScan** 机器人检测 | 被检测到 | **正常**（4/4） | browserscan.net |
| **bot.incolumitas.com** | 13 项失败 | **1 项失败** | 仅剩 WEBDRIVER 规范项 |
| **deviceandbrowserinfo.com** | 6 个 true 标志 | **0 个 true 标志** | `isBot: false` |
| `navigator.webdriver` | `true` | **`false`** | 源码级补丁 |
| `navigator.plugins.length` | 0 | **5** | 真实插件列表 |
| `window.chrome` | `undefined` | **`object`** | 与真实 Chrome 一致 |
| UA 字符串 | `HeadlessChrome` | **`Chrome/146.0.0.0`** | 无 headless 泄漏 |
| CDP 检测 | 被检测到 | **未检测到** | `isAutomatedWithCDP: false` |
| TLS 指纹 | 不匹配 | **与 Chrome 完全一致** | ja3n / ja4 / akamai 匹配 |
| | | **已在 30+ 个检测站点测试** | |

### 证据

<p align="center">
<img src="https://i.imgur.com/hvIQyMv.png" width="600" alt="reCAPTCHA v3 — 0.9 分">
<br><em>reCAPTCHA v3 分数 0.9 — 服务端已验证（真人级）</em>
</p>

<p align="center">
<img src="https://i.imgur.com/qMIRfhq.png" width="600" alt="Cloudflare Turnstile — 成功">
<br><em>Cloudflare Turnstile 非交互挑战 — 自动通过</em>
</p>

<p align="center">
<img src="https://i.imgur.com/PRsw6rT.png" width="600" alt="BrowserScan — 正常">
<br><em>BrowserScan 机器人检测 — 正常（4/4 项通过）</em>
</p>

<p align="center">
<img src="https://i.imgur.com/9n2C7tu.png" width="600" alt="FingerprintJS — 已通过">
<br><em>FingerprintJS 网页抓取演示 — 返回数据，未被拦截</em>
</p>

<p align="center">
<img src="https://i.imgur.com/srCcFtK.png" width="600" alt="deviceandbrowserinfo.com — 你是人类！">
<br><em>deviceandbrowserinfo.com 行为机器人检测 — 使用 humanize=True 时显示 “You are human!”（24/24 信号通过）</em>
</p>

## 对比

| 功能 | Playwright | playwright-stealth | undetected-chromedriver | Camoufox | CloakBrowser |
|---|---|---|---|---|---|
| reCAPTCHA v3 分数 | 0.1 | 0.3-0.5 | 0.3-0.7 | 0.7-0.9 | **0.9** |
| Cloudflare Turnstile | 失败 | 有时可过 | 有时可过 | 可过 | **可过** |
| 补丁层级 | 无 | JS 注入 | 配置级补丁 | C++（Firefox） | **C++（Chromium）** |
| 是否能扛住 Chrome 更新 | N/A | 经常失效 | 经常失效 | 可以 | **可以** |
| 维护状态 | 是 | 停更 | 停更 | 不稳定 | **活跃维护** |
| 浏览器引擎 | Chromium | Chromium | Chrome | Firefox | **Chromium** |
| Playwright API | 原生 | 原生 | 否（Selenium） | 否 | **原生** |

## 工作原理

CloakBrowser 是一个轻量包装层（Python + JavaScript），底层是自定义构建的 Chromium 二进制：

1. **安装** → `pip install cloakbrowser` 或 `npm install cloakbrowser`
2. **首次启动** → 自动下载适配你平台的二进制（Chromium 146）
3. **每次启动** → Playwright 或 Puppeteer 使用我们的二进制和隐身参数启动
4. **继续写代码** → 仍然使用标准 Playwright / Puppeteer API，无需学习新接口

这个二进制包含 58 个源码级补丁，覆盖 canvas、WebGL、音频、字体、GPU、屏幕属性、WebRTC、网络时序、硬件信息上报、自动化信号移除，以及对 CDP 输入行为的模拟。

这些修改是直接编译进 Chromium 二进制中的，不是通过 JavaScript 注入，也不是通过标志位设置。

二进制下载会进行 SHA-256 校验，确保完整性。

## API

### `launch()`

```python
from cloakbrowser import launch

# 基础用法：无头模式，默认隐身配置
browser = launch()

# 有头模式（可看到浏览器窗口）
browser = launch(headless=False)

# 使用代理（HTTP 或 SOCKS5）
browser = launch(proxy="http://user:pass@proxy:8080")
browser = launch(proxy="socks5://user:pass@proxy:1080")

# 使用代理字典（支持 bypass 和分离的认证字段）
browser = launch(proxy={"server": "http://proxy:8080", "bypass": ".google.com", "username": "user", "password": "pass"})

# 追加 Chrome 参数
browser = launch(args=["--disable-gpu"])

# 设置时区和语言环境（通过二进制标志设置，不会触发可检测的 CDP 模拟）
browser = launch(timezone="America/New_York", locale="en-US")

# 根据代理 IP 自动检测时区/语言环境（需要：pip install cloakbrowser[geoip]）
# 同时自动注入 --fingerprint-webrtc-ip 以防止 WebRTC IP 泄漏（无额外成本）
# 注意：会通过你的代理发起 HTTP 请求以解析出口 IP（ipify.org、checkip.amazonaws.com）
browser = launch(proxy="http://proxy:8080", geoip=True)

# 显式设置 timezone/locale 时，总是优先于自动检测
browser = launch(proxy="http://proxy:8080", geoip=True, timezone="Europe/London")

# 仅启用 WebRTC IP 伪装（不需要 geoip 依赖，会通过代理发起 HTTP 请求解析出口 IP）
browser = launch(proxy="http://proxy:8080", args=["--fingerprint-webrtc-ip=auto"])

# 显式指定 WebRTC IP（不发起网络请求）
browser = launch(proxy="http://proxy:8080", args=["--fingerprint-webrtc-ip=1.2.3.4"])

# 启用类人鼠标、键盘和滚动行为
browser = launch(humanize=True)

# 使用更慢、更谨慎的动作模式
browser = launch(humanize=True, human_preset="careful")

# 不使用默认隐身参数（自行提供指纹参数）
browser = launch(stealth_args=False, args=["--fingerprint=12345"])
```

返回标准 Playwright `Browser` 对象。所有 Playwright 方法都可直接使用：`new_page()`、`new_context()`、`close()` 等。

### `launch_async()`

```python
import asyncio
from cloakbrowser import launch_async

async def main():
    browser = await launch_async()
    page = await browser.new_page()
    await page.goto("https://example.com")
    print(await page.title())
    await browser.close()

asyncio.run(main())
```

<a id="launch_context"></a>
### `launch_context()`

便捷函数，一次调用即可同时创建浏览器和上下文，并设置 UA、viewport、locale 和 timezone：

```python
from cloakbrowser import launch_context

context = launch_context(
    user_agent="Custom UA",
    viewport={"width": 1920, "height": 1080},
    locale="en-US",
    timezone="America/New_York",
)
page = context.new_page()
page.goto("https://protected-site.com")
context.close()
```

额外的 kwargs 会透传给 Playwright 的 `browser.new_context()`。可用于 `storage_state`、`permissions`、`extra_http_headers` 等场景，而无需使用持久配置文件目录：

```python
from cloakbrowser import launch_context

# 从 JSON 文件恢复已保存的会话（cookies、localStorage）
context = launch_context(storage_state="state.json")
page = context.new_page()
page.goto("https://example.com")
# 将状态保存回文件，供下次运行继续使用
context.storage_state(path="state.json")
context.close()
```

### `launch_context_async()`

`launch_context()` 的异步版本。签名相同，kwargs 也同样透传：

```python
import asyncio
from cloakbrowser import launch_context_async

async def main():
    ctx = await launch_context_async(storage_state="state.json")
    page = await ctx.new_page()
    await page.goto("https://example.com")
    await ctx.storage_state(path="state.json")
    await ctx.close()

asyncio.run(main())
```

<a id="launch_persistent_context"></a>
### `launch_persistent_context()`

与 `launch_context()` 类似，但使用持久用户配置文件。cookies、localStorage 和缓存都会跨会话保留。

在以下场景中使用它：
- **跨多次运行保持登录状态**（cookies / sessions 可在重启后保留）
- **绕过无痕模式检测**（部分站点会标记空白、短暂的临时配置文件）
- **加载 Chrome 扩展**（扩展只能从真实用户数据目录加载）
- **建立自然的浏览历史**（缓存字体、service worker、IndexedDB 会逐步累积，让配置文件更像真实用户）

```python
from cloakbrowser import launch_persistent_context

# 第一次运行：创建配置文件
ctx = launch_persistent_context("./my-profile", headless=False)
page = ctx.new_page()
page.goto("https://protected-site.com")
ctx.close()  # 保存配置文件

# 下一次运行：自动恢复 cookies 和 localStorage
ctx = launch_persistent_context("./my-profile", headless=False)

# 加载 Chrome 扩展
ctx = launch_persistent_context(
    "./my-profile",
    headless=False,
    extension_paths=["./my-extension"],
)
```

支持 `launch_context()` 的全部选项：`proxy`、`user_agent`、`viewport`、`locale`、`timezone`、`color_scheme`、`geoip`、`extension_paths`。

异步版本为：`launch_persistent_context_async()`。

**存储配额与检测的权衡：** 默认情况下，二进制会标准化存储配额以通过 FingerprintJS，而 FingerprintJS 会拦截报告非无痕存储配额的持久上下文。这意味着惩罚无痕模式的检测服务（例如 BrowserScan 的 `notPrivate` 检查，-10 分）仍然会将其标记出来。如果你的目标站点会惩罚无痕模式、但并不使用 FingerprintJS，可以通过设置更高的配额让它看起来像常规配置文件：

```python
ctx = launch_persistent_context("./my-profile", args=["--fingerprint-storage-quota=5000"])
```

| 配额设置 | FingerprintJS | BrowserScan `notPrivate` |
|---|---|---|
| 默认（自动，约 500MB） | 通过 | -10（被标记为无痕） |
| `--fingerprint-storage-quota=5000` | 可能触发检测 | 通过（看起来像非无痕） |

### CLI

可在命令行中预下载二进制，或检查安装状态：

```bash
python -m cloakbrowser install      # 下载二进制并显示进度
python -m cloakbrowser info         # 显示版本、路径、平台
python -m cloakbrowser update       # 检查并下载更新版本
python -m cloakbrowser clear-cache  # 删除缓存的二进制
```

### 工具函数

```python
from cloakbrowser import binary_info, clear_cache, ensure_binary

# 检查二进制安装状态
print(binary_info())
# {'version': '146.0.7680.177.5', 'platform': 'linux-x64', 'installed': True, ...}

# 强制重新下载
clear_cache()

# 预下载二进制（例如在 Docker 构建期间）
ensure_binary()
```

## JavaScript / Node.js API

CloakBrowser 提供完整 TypeScript 类型定义。你可以选择 Playwright 或 Puppeteer，底层使用的都是同一个隐身二进制。

### Playwright（默认）

```javascript
import { launch, launchContext, launchPersistentContext } from 'cloakbrowser';

// 基础用法
const browser = await launch();

// 带选项启动
const browser = await launch({
  headless: false,
  proxy: 'http://user:pass@proxy:8080',
  args: ['--fingerprint=12345'],
  timezone: 'America/New_York',
  locale: 'en-US',
  humanize: true,
});

// 便捷用法：一次创建浏览器和上下文
const context = await launchContext({
  userAgent: 'Custom UA',
  viewport: { width: 1920, height: 1080 },
  locale: 'en-US',
  timezone: 'America/New_York',
});
const page = await context.newPage();

// 持久配置文件：cookies / localStorage 会跨重启保留，可避免无痕模式检测
const ctx = await launchPersistentContext({
  userDataDir: './chrome-profile',
  headless: false,
  proxy: 'http://user:pass@proxy:8080',
});
```

> **注意：** 上面每个示例都是独立的，不应直接拼接成一个代码块运行。

JS 中同样支持所有 Python 选项：可用 `stealthArgs: false` 关闭默认配置，用 `geoip: true` 根据代理出口 IP 自动检测时区和语言环境。

<a id="puppeteer"></a>
### Puppeteer

> **注意：** 对于使用 reCAPTCHA Enterprise 的站点，推荐使用 Playwright 包装器。Puppeteer 的 CDP 协议会泄漏自动化信号，而 reCAPTCHA Enterprise 可以检测到这些信号，导致间歇性 403 错误。这是 Puppeteer 的已知限制，并非 CloakBrowser 独有。要获得最佳效果，请使用 Playwright。

```javascript
import { launch } from 'cloakbrowser/puppeteer';

const browser = await launch({ headless: true });
const page = await browser.newPage();
await page.goto('https://example.com');
await browser.close();
```

### 工具函数（JS）

```javascript
import { ensureBinary, clearCache, binaryInfo } from 'cloakbrowser';

// 预下载二进制（例如在 Docker 构建期间）
await ensureBinary();

// 检查安装状态
console.log(binaryInfo());

// 强制重新下载
clearCache();
```

## 人类行为模拟

传入 `humanize=True`，即可让所有鼠标、键盘和滚动交互看起来与真人无异。所有 Playwright 调用（`page.click()`、`page.fill()`、`page.type()`、`page.mouse.*`、`page.keyboard.*`、Locator API）以及 Puppeteer 调用（`page.click()`、`page.type()`、`page.mouse.*`、`page.keyboard.*`、ElementHandle API）都会自动替换为类人实现。无需改动业务代码。

```python
browser = launch(humanize=True)
page = browser.new_page()
page.goto("https://example.com")
page.locator("#email").fill("user@example.com")  # 逐字符输入，带思考停顿
page.locator("button[type=submit]").click()       # Bézier 曲线移动，命中点更真实
```

```javascript
// Playwright
import { launch } from 'cloakbrowser';
const browser = await launch({ humanize: true });
```

```javascript
// Puppeteer
import { launch } from 'cloakbrowser/puppeteer';
const browser = await launch({ humanize: true });
```

**变化如下：**

| 交互 | 默认行为 | 启用 `humanize=True` 后 |
|---|---|---|
| 鼠标移动 | 瞬移 | 带缓动和轻微过冲的 Bézier 曲线 |
| 点击 | 瞬时触发 | 真实瞄准点 + 按下停留时长 |
| 键盘 | 立即填充 | 逐字符时序、思考停顿、偶发拼写错误并自动修正 |
| 滚动 | 跳跃式 | 加速 → 匀速 → 减速的微步滚动 |
| `fill()` | 直接设置值 | 先清空已有内容，再逐字符输入 |

**预设** — `default`（正常速度）或 `careful`（更慢、更谨慎，动作之间带空闲微动作）：

```python
browser = launch(humanize=True, human_preset="careful")
```

```javascript
const browser = await launch({ humanize: true, humanPreset: 'careful' });
```

**自定义配置** — 可覆盖任意参数：

```python
browser = launch(humanize=True, human_config={
    "mistype_chance": 0.05,              # 5% 的打字错误率，并会自动修正
    "typing_delay": 100,                 # 更慢的打字速度（每字符毫秒）
    "idle_between_actions": True,        # 点击之间插入微动作
    "idle_between_duration": [0.3, 0.8], # 空闲时长范围（秒）
})
```

```javascript
const browser = await launch({
    humanize: true,
    humanConfig: {
        mistype_chance: 0.05,
        typing_delay: 100,
        idle_between_actions: true,
        idle_between_duration: [0.3, 0.8],
    }
});
```

如果你在某次调用中需要原始、未打补丁的 Playwright 页面，可通过 `page._original` 访问，以获得最大速度。

> **注意（Playwright）：** 请始终使用 `page.click(selector)`、`page.type(selector, text)`、`page.hover(selector)` 或 `page.locator(selector).*`。这些路径会完整进入 humanize 流水线。避免使用 `page.query_selector()`，因为 `ElementHandle` 对象会绕过所有补丁，导致鼠标瞬移、键盘事件没有时序、滚动没有类人曲线。
>
> **注意（Puppeteer）：** 基于 selector 的方法（`page.click()`、`page.type()`）和 ElementHandle 方法（`el.click()`、`el.type()`）都会被完整人类化。`page.$()`、`page.$$()` 和 `page.waitForSelector()` 返回的句柄也会自动打补丁。

> 由 [@evelaa123](https://github.com/evelaa123) 贡献 — 覆盖完整的 Playwright 和 Puppeteer API。

## 配置

| 环境变量 | 默认值 | 说明 |
|---|---|---|
| `CLOAKBROWSER_BINARY_PATH` | — | 跳过下载，改用本地 Chromium 二进制 |
| `CLOAKBROWSER_CACHE_DIR` | `~/.cloakbrowser` | 二进制缓存目录 |
| `CLOAKBROWSER_DOWNLOAD_URL` | `cloakbrowser.dev` | 自定义二进制下载地址 |
| `CLOAKBROWSER_AUTO_UPDATE` | `true` | 设为 `false` 可关闭后台更新检查 |
| `CLOAKBROWSER_SKIP_CHECKSUM` | `false` | 设为 `true` 可跳过下载后的 SHA-256 校验 |
| `CLOAKBROWSER_GEOIP_TIMEOUT_SECONDS` | `5` | GeoIP 解析超时时间（秒），超时后继续运行而不启用它 |

<a id="fingerprint-management"></a>
## 指纹管理

这个二进制**默认就具备隐身能力**，无需任何标志。它会在启动时自动生成随机指纹种子，并伪造所有可检测值（GPU、硬件规格、屏幕尺寸、canvas、WebGL、音频、字体）。每次启动都会得到一个全新且自洽的身份。

**指纹机制如下：**

| 场景 | 发生什么 |
|----------|-------------|
| **不传任何标志** | 启动时自动生成随机种子。GPU、屏幕、硬件规格和所有噪声补丁都会自动伪装。每次启动都是新身份。 |
| **`--fingerprint=seed`** | 由该种子生成确定性身份。同一个种子 = 每次启动得到相同指纹。适合会话持久化（回访用户）。 |
| **`--fingerprint=seed` + 显式标志** | 显式标志会覆盖自动生成的单项值，种子负责补齐其余字段。 |

二进制会在编译时检测自身平台：macOS 二进制会报告为 macOS + Apple GPU，Linux 二进制会报告为 Linux + NVIDIA GPU。**包装器**在 Linux 上会通过 `--fingerprint-platform=windows` 覆盖这一点，使会话看起来像 Windows 桌面浏览器（更常见，也更难聚类）。如果直接运行二进制，可使用 `--fingerprint-platform` 进行跨平台伪装。

> **建议：重复访问同一站点时使用固定种子。** 随机种子会让每次会话都像不同设备，如果你从同一个 IP 反复访问同一站点，这反而可能显得可疑。对于 reCAPTCHA v3 Enterprise 之类的评分系统，固定种子会在多次会话中保持一致指纹，让你看起来像回访用户：
> ```python
> browser = launch(args=["--fingerprint=12345"])
> ```
> ```javascript
> const browser = await launch({ args: ['--fingerprint=12345'] });
> ```

### 默认指纹

每次 `launch()` 都会自动设置这些值。**包装器**会根据平台应用默认值：Linux 上默认伪装成 Windows，以获得更常见的指纹；macOS 上则保持原生 Mac 浏览器身份：

| 标志 | Linux / Windows 默认值 | macOS 默认值 | 控制项 |
|------|--------------|---------------|----------|
| `--fingerprint` | 随机（10000–99999） | 随机（10000–99999） | canvas、WebGL、音频、字体、client rects 的主种子 |
| `--fingerprint-platform` | `windows` | `macos` | `navigator.platform`、User-Agent OS、GPU 池选择 |

其余所有值都由二进制基于种子自动生成：GPU、hardware concurrency、device memory、屏幕尺寸。每个种子都会生成唯一且一致的指纹。如有需要，可通过显式标志覆盖。

> **直接运行二进制？** 零标志即可工作，二进制会自动完成所有伪装。传入 `--fingerprint=seed` 可获得持久身份，也可以用 `--fingerprint-gpu-renderer` 这类显式标志覆盖任意自动生成的值。

### 其他标志

由二进制支持，但**默认不会设置**。如需自定义，可通过 `args` 传入：

| 标志 | 控制项 |
|------|----------|
| `--fingerprint-gpu-vendor` | WebGL `UNMASKED_VENDOR_WEBGL`（根据种子 + 平台自动生成） |
| `--fingerprint-gpu-renderer` | WebGL `UNMASKED_RENDERER_WEBGL`（根据种子 + 平台自动生成） |
| `--fingerprint-hardware-concurrency` | `navigator.hardwareConcurrency`（自动值：`8`） |
| `--fingerprint-device-memory` | `navigator.deviceMemory`（GB，自动值：`8`） |
| `--fingerprint-screen-width` | 屏幕宽度（自动值：Win/Linux 为 `1920`，macOS 为 `1440`） |
| `--fingerprint-screen-height` | 屏幕高度（自动值：Win/Linux 为 `1080`，macOS 为 `900`） |
| `--fingerprint-brand` | 浏览器品牌：`Chrome`、`Edge`、`Opera`、`Vivaldi` |
| `--fingerprint-brand-version` | 品牌版本（UA + Client Hints） |
| `--fingerprint-platform-version` | Client Hints 平台版本 |
| `--fingerprint-location` | 地理位置坐标 |
| `--fingerprint-timezone` | 时区（例如 `America/New_York`） |
| `--fingerprint-locale` | 语言环境（例如 `en-US`） |
| `--fingerprint-storage-quota` | 覆盖存储配额（MB）— 会影响 `storage.estimate()`、`storageBuckets` 和旧版 webkit API。设置 `--fingerprint` 时会自动标准化 |
| `--fingerprint-taskbar-height` | 覆盖任务栏高度（二进制默认：Win=48，Mac=95，Linux=0） |
| `--fingerprint-fonts-dir` | 指向目标平台字体目录的路径（见 [Linux 上的字体配置](#font-setup-on-linux)） |
| `--fingerprint-webrtc-ip` | WebRTC ICE candidate IP 替换。传 `auto` 时会通过代理解析出口 IP（会发起一次 HTTP 请求），也可直接传显式 IP。使用 `geoip=True` 时会自动注入 |
| `--fingerprint-noise=false` | 关闭噪声注入（canvas、WebGL、音频、client rects），但保留确定性指纹种子 |
| `--enable-blink-features=FakeShadowRoot` | 访问 closed shadow DOM 元素 |

> **注意：** 所有隐身测试都基于上面的默认指纹配置验证。修改这些标志可能影响检测结果，上生产前请务必自行测试。

<a id="font-setup-on-linux"></a>
### Linux 上的字体配置

**对 Kasada、Akamai 这类高强度反机器人站点是必需项。** 这类系统会在隐藏 canvas 上渲染 emoji，并对像素输出做哈希。精简 Linux 环境（Docker、云主机）通常缺少 emoji 和扩展字体，得到的哈希与真实浏览器不匹配。安装标准字体包即可修复：

```bash
sudo apt install -y fonts-noto-color-emoji fonts-freefont-ttf fonts-unifont \
    fonts-ipafont-gothic fonts-wqy-zenhei fonts-tlwg-loma-otf
```

Docker 镜像（`cloakhq/cloakbrowser`）已预装这些字体。如果你是在 Linux 服务器或自定义 Docker 镜像中直接运行二进制，请手动安装。

**可选：用于提升 CreepJS 字体枚举分数的 Windows 字体。** 上述字体包能修复反机器人 canvas 检查，但不会改善 CreepJS 的字体得分。为此你需要真实的 Windows 字体（Segoe UI、Calibri、Bahnschrift 等），可从 Windows 机器的 `C:\Windows\Fonts\` 目录获取；`ttf-mscorefonts-installer` 仅包含 XP 时代的旧字体，不够用。

```bash
mkdir -p ~/.local/share/fonts/windows
cp /path/to/windows/fonts/*.ttf ~/.local/share/fonts/windows/
cp /path/to/windows/fonts/*.TTF ~/.local/share/fonts/windows/
fc-cache -f  # 手动复制字体后必须刷新缓存
```

```python
browser = launch(
    args=["--fingerprint-fonts-dir=/home/user/.local/share/fonts/windows"],
)
```

### 示例

```python
# 固定一个种子，获得持久身份
browser = launch(args=["--fingerprint=42069"])

# 完全手动控制：关闭默认值，自行指定所有内容
browser = launch(stealth_args=False, args=[
    "--fingerprint=42069",
    "--fingerprint-platform=windows",
])

# 覆盖 GPU，伪装成某一台特定机器
browser = launch(args=[
    "--fingerprint-gpu-vendor=Intel Inc.",
    "--fingerprint-gpu-renderer=Intel Iris OpenGL Engine",
])
```

## 示例

**Python** — 见 [`examples/`](examples/)：
- [`basic.py`](examples/basic.py) — 启动并加载一个页面
- [`persistent_context.py`](examples/persistent_context.py) — 持久配置文件，保存 cookies / localStorage
- [`recaptcha_score.py`](examples/recaptcha_score.py) — 检查你的 reCAPTCHA v3 分数
- [`stealth_test.py`](examples/stealth_test.py) — 在 6 个检测站点上运行测试
- [`fingerprint_scan_test.py`](examples/fingerprint_scan_test.py) — 对 fingerprint-scan.com 和 CreepJS 进行测试

**JavaScript** — 见 [`js/examples/`](js/examples/)：
- [`basic-playwright.ts`](js/examples/basic-playwright.ts) — 使用 Playwright 启动并加载页面
- [`basic-puppeteer.ts`](js/examples/basic-puppeteer.ts) — 使用 Puppeteer 启动并加载页面
- [`stealth-test.ts`](js/examples/stealth-test.ts) — 在 6 个检测站点上运行测试

<a id="framework-integrations"></a>
### 框架集成

CloakBrowser 可与任何基于 Playwright 或 Chromium 的框架一起使用：

```python
# 方式 1：由框架直接启动我们的二进制（Selenium、Stagehand、UC）
from cloakbrowser.download import ensure_binary
from cloakbrowser.config import get_default_stealth_args
binary_path = ensure_binary()              # 如有需要会自动下载
stealth_args = get_default_stealth_args()  # 所有指纹参数

# 方式 2：先启动 CloakBrowser，再让框架通过 CDP 连接（browser-use、Crawl4AI、Scrapling）
from cloakbrowser import launch_async
browser = await launch_async(args=["--remote-debugging-port=9242"])
# 将你的框架连接到 http://127.0.0.1:9242 —— 所有隐身参数都已设置好
# 注意：humanize 仍然需要包装器层支持（见下文）
```

> **通过 CDP 使用 humanize：** 指纹隐身补丁在通过 CDP 连接时会自动生效，但 `humanize=True` 是包装器层功能。如果你从独立脚本通过 CDP 连接 CloakBrowser，需要显式导入补丁函数来启用人类行为模拟：
>
> ```js
> import { patchBrowser, resolveConfig } from 'cloakbrowser/human';
> patchBrowser(browser, resolveConfig('default'));
> ```

| 框架 | Stars | 语言 | 示例 |
|-----------|-------|----------|---------|
| [browser-use](https://github.com/browser-use/browser-use) | 70K | Python | [`browser_use_example.py`](examples/integrations/browser_use_example.py) |
| [Crawl4AI](https://github.com/unclecode/crawl4ai) | 58K | Python | [`crawl4ai_example.py`](examples/integrations/crawl4ai_example.py) |
| [Crawlee](https://github.com/apify/crawlee-python) | 8.6K | Python | [`crawlee_example.py`](examples/integrations/crawlee_example.py) |
| [Scrapling](https://github.com/D4Vinci/Scrapling) | 21K | Python | [`scrapling_example.py`](examples/integrations/scrapling_example.py) |
| [Stagehand](https://github.com/browserbase/stagehand) | 21K | TypeScript | [`stagehand.ts`](js/examples/stagehand.ts) |
| [LangChain](https://github.com/langchain-ai/langchain) | 100K+ | Python | [`langchain_loader.py`](examples/integrations/langchain_loader.py) |
| [Selenium](https://github.com/SeleniumHQ/selenium) | — | Python | [`selenium_example.py`](examples/integrations/selenium_example.py) |
| [undetected-chromedriver](https://github.com/ultrafunkamsterdam/undetected-chromedriver) | 12K | Python | [`undetected_chromedriver.py`](examples/integrations/undetected_chromedriver.py) |
| [agent-browser](https://github.com/nichochar/agent-browser) | — | Shell | [`agent_browser.sh`](examples/integrations/agent_browser.sh) |

### 部署集成

| 平台 | 示例 |
|----------|---------|
| [AWS Lambda](https://aws.amazon.com/lambda/) | [`aws_lambda/`](examples/integrations/aws_lambda/) — 在 Lambda 中进行一次性抓取（容器镜像） |

## 平台

| 平台 | Chromium | 补丁数 | 状态 |
|---|---|---|---|
| Linux x86_64 | 146 | 58 | ✅ 最新 |
| Linux arm64（RPi、Graviton） | 146 | 58 | ✅ |
| macOS arm64（Apple Silicon） | 145 | 26 | ✅ |
| macOS x86_64（Intel） | 145 | 26 | ✅ |
| Windows x86_64 | 146 | 58 | ✅ 最新 |

包装器会自动下载适用于你平台的正确二进制。

**macOS 首次启动：** 该二进制使用 ad-hoc 签名。首次运行时，macOS Gatekeeper 会阻止它。右键应用 → **Open** → 在弹窗中点击 **Open**。这只需要做一次。

## Docker

Docker Hub 提供了预构建镜像，无需安装，无需配置。

### 快速测试

```bash
docker run --rm cloakhq/cloakbrowser cloaktest
```

### 运行脚本

```bash
# 内联脚本
docker run --rm cloakhq/cloakbrowser python -c "
from cloakbrowser import launch
browser = launch()
page = browser.new_page()
page.goto('https://example.com')
print(page.title())
browser.close()
"

# 挂载你自己的脚本
docker run --rm -v ./my_script.py:/app/my_script.py cloakhq/cloakbrowser python my_script.py

# 使用代理
docker run --rm cloakhq/cloakbrowser python -c "
from cloakbrowser import launch
browser = launch(proxy='http://user:pass@proxy:8080')
page = browser.new_page()
page.goto('https://example.com')
print(page.title())
browser.close()
"
```

### CDP 服务器模式

启动一个持久的隐身浏览器，并通过 Chrome DevTools Protocol 远程连接：

```bash
docker run -d --name cloak -p 127.0.0.1:9222:9222 cloakhq/cloakbrowser cloakserve
```

然后从宿主机连接：

```python
from playwright.sync_api import sync_playwright

pw = sync_playwright().start()
browser = pw.chromium.connect_over_cdp("http://localhost:9222")
page = browser.new_page()
page.goto("https://example.com")
print(page.title())
browser.close()
```

向浏览器传递额外标志：

```bash
# 使用代理
docker run -d --name cloak -p 127.0.0.1:9222:9222 cloakhq/cloakbrowser \
  cloakserve --proxy-server=http://proxy:8080

# 有头模式（在容器内通过 Xvfb 渲染）
docker run -d --name cloak -p 127.0.0.1:9222:9222 cloakhq/cloakbrowser \
  cloakserve --headless=false
```

停止服务：

```bash
docker stop cloak && docker rm cloak
```

> **安全性：** CDP 拥有对浏览器的完全控制权（执行 JS、读取页面、访问文件）。
> 示例将端口绑定到 `127.0.0.1`，因此只有本机可以连接。切勿在没有额外认证措施的情况下
> 将 9222 端口暴露到公网。

### Docker Compose

```yaml
services:
  cloakbrowser:
    image: cloakhq/cloakbrowser
    command: cloakserve
    restart: unless-stopped
    ports:
      - "127.0.0.1:9222:9222"
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:9222/json/version"]
      interval: 30s
      timeout: 5s
      retries: 3
      start_period: 10s
```

**按连接分配指纹种子** — 你可以在单个容器中运行多个浏览器身份。每个不同的种子都会启动一个独立的 Chrome 进程，并拥有自己的指纹：

```python
# 每个种子都会得到不同的 canvas 噪声、client rects 和其他浏览器信号
b1 = pw.chromium.connect_over_cdp("http://localhost:9222?fingerprint=11111")
b2 = pw.chromium.connect_over_cdp("http://localhost:9222?fingerprint=22222")

# 通过查询参数完整控制身份
b3 = pw.chromium.connect_over_cdp(
    "http://localhost:9222?fingerprint=33333"
    "&timezone=Asia/Tokyo&locale=ja-JP&platform=macos"
    "&hardware-concurrency=4&device-memory=8"
)

# 根据代理出口 IP 自动检测时区/语言环境
b4 = pw.chromium.connect_over_cdp(
    "http://localhost:9222?fingerprint=44444"
    "&proxy=http://proxy:8080&geoip=true"
)
```

支持的查询参数有：`fingerprint`、`timezone`、`locale`、`platform`、`platform-version`、`brand`、`brand-version`、`gpu-vendor`、`gpu-renderer`、`hardware-concurrency`、`device-memory`、`screen-width`、`screen-height`、`proxy`、`geoip`。相同种子会复用同一进程（以第一次连接的参数为准）。不传种子时使用共享的默认进程（向后兼容）。可通过 `GET /` 查看活动进程（返回包含 PID、端口和连接数的 JSON）。

**持久配置文件** — 可挂载 volume，在容器重启后保留 cookies 和会话：

```bash
docker run --rm -v ./my-profile:/profile cloakhq/cloakbrowser python -c "
from cloakbrowser import launch_persistent_context
ctx = launch_persistent_context('/profile')
page = ctx.new_page()
page.goto('https://example.com')
ctx.close()
"
```

再次使用同一个 volume 运行时，会自动恢复 cookies、localStorage 和缓存。

**资源占用：** 空闲约 190MB RAM，打开 3 个标签页约 280MB。每增加一个标签页约多 30MB。

### 使用你自己的镜像扩展

```dockerfile
FROM cloakhq/cloakbrowser
COPY your_script.py /app/
CMD ["python", "your_script.py"]
```

**从 pip 构建你自己的镜像** — 在构建期间使用 `python -m cloakbrowser install` 下载二进制，并显示可见进度：

```dockerfile
FROM python:3.12-slim
RUN pip install cloakbrowser && python -m cloakbrowser install
COPY your_script.py /app/
CMD ["python", "/app/your_script.py"]
```

**从源码构建** — 仓库也自带了一个 [`Dockerfile`](Dockerfile)，如果你想构建自己的镜像，可直接使用：

```bash
docker build -t cloakbrowser .
```

CloakBrowser 在本地、Docker 和 VPS 中的行为完全一致，不需要环境特定配置。

**注意：** 如果你在启用了 uvloop 的 Web 服务器中运行 CloakBrowser（例如 `uvicorn[standard]`），请使用 `--loop asyncio`，以避免子进程管道卡住。

## 故障排查

---

### 在高强度站点（DataDome、Turnstile）上仍然被拦截？

有些站点即使面对我们的 C++ 补丁，仍然会检测 headless 模式。请改用**有头模式**并配合虚拟显示：

```bash
# 安装 Xvfb（虚拟帧缓冲）
sudo apt install xvfb

# 启动虚拟显示
Xvfb :99 -screen 0 1920x1080x24 &
export DISPLAY=:99
```

```python
from cloakbrowser import launch

# 有头模式 + 住宅代理，获得最高隐身效果
browser = launch(headless=False, proxy="http://your-residential-proxy:port")
page = browser.new_page()
page.goto("https://heavily-protected-site.com")  # 可通过 DataDome 等站点
browser.close()
```

这会在虚拟显示上运行一个真实的有头浏览器，不需要实体显示器。结合下方推荐配置，可获得最佳隐身效果。

---

### 面向反机器人站点的推荐配置

大多数拦截都不是因为浏览器指纹本身，而是因为少了以下三项中的一项：

```python
browser = launch(
    proxy="http://your-residential-proxy:port",  # 住宅 IP；机房 IP 往往会因信誉问题直接被拦截
    geoip=True,      # 让时区和语言环境与代理出口 IP 匹配（否则 UTC + en-US 很像机器人）
    headless=False,  # 有头模式；有些站点即使面对 C++ 补丁也会检测 headless
    humanize=True,   # 类人鼠标、键盘和滚动行为
)
```

```javascript
const browser = await launch({
    proxy: 'http://your-residential-proxy:port',
    geoip: true,
    headless: false,
    humanize: true,
});
```

如果你的代理支持 SOCKS5，建议优先使用。它兼容性更好，因为 SOCKS5 传输的是原始 TCP，可以绕开某些代理在 HTTP/2 场景下的 HTTP CONNECT 问题：

```python
browser = launch(proxy="socks5://user:pass@proxy:1080", geoip=True, headless=False, humanize=True)
```

如果这样仍然被拦截，请检查下面的字体配置部分。

---

### 在配置正确的情况下，仍然被 Kasada / Akamai 拦截？

在精简 Linux 环境中，缺失字体包会导致 canvas 上的 emoji 渲染结果生成反机器人系统无法识别的哈希。在代理、geoip 和有头模式都已正确设置的前提下，这是最常见的拦截原因。

请安装上文 [Linux 上的字体配置](#font-setup-on-linux) 一节中列出的字体包。

---

### 站点在新会话时挑战你，但访问一次后就恢复正常

有些站点会通过 HTTP/2 对没有 cookies 的首次访问者发起挑战。这不是 CloakBrowser 独有问题，而是所有 Chromium 浏览器都可能遇到。可通过持久配置文件先“预热”一次 cookies，然后在后续会话中复用：

```python
from cloakbrowser import launch_persistent_context

# 第一次运行：配合 --disable-http2 预热
ctx = launch_persistent_context("./profile", args=["--disable-http2"])
page = ctx.new_page()
page.goto("https://example.com")  # 预热 cookies
ctx.close()

# 后续运行：不再需要 --disable-http2
ctx = launch_persistent_context("./profile")
page = ctx.new_page()
page.goto("https://example.com")  # 使用已保存 cookies，可直接通过
```

```javascript
import { launchPersistentContext } from 'cloakbrowser';

// 第一次运行：配合 --disable-http2 预热
let ctx = await launchPersistentContext({ userDataDir: './profile', args: ['--disable-http2'] });
let page = await ctx.newPage();
await page.goto('https://example.com');
await ctx.close();

// 后续运行：不再需要 --disable-http2
ctx = await launchPersistentContext({ userDataDir: './profile' });
```

如果你的场景是无状态 / 临时会话，也可以直接使用 `launch(args=["--disable-http2"])` 强制降级为 HTTP/1.1，从而绕过检查。只在确实需要的站点上使用此标志，因为大多数站点在 HTTP/2 下本来就能正常工作。如果你的代理支持 SOCKS5，也可以改用 `proxy="socks5://user:pass@host:port"`，因为 SOCKS5 能完全绕开 HTTP CONNECT。

---

### 有东西不工作？先确认你使用的是最新版本

旧版本可能仍在使用过时的隐身参数，或者下载了旧版二进制：
```bash
pip install -U cloakbrowser     # Python
npm install cloakbrowser@latest # JavaScript
docker pull cloakhq/cloakbrowser:latest  # Docker
```

---

### 二进制下载失败 / 超时

可设置自定义下载 URL，或直接使用本地二进制：
```bash
export CLOAKBROWSER_BINARY_PATH=/path/to/your/chrome
```

---

### 新更新导致问题？回滚到上一版本

安装指定版本的包装器，即可同时回退包装器本身及其下载的二进制版本：
```bash
pip install cloakbrowser==0.3.21               # Python
npm install cloakbrowser@0.3.21                # JavaScript
docker pull cloakhq/cloakbrowser:0.3.21        # Docker
```
每个包装器版本都固定对应自己的二进制版本，因此回退包装器后，下一次启动就会自动得到匹配的旧版二进制。

---

### macOS："App is damaged" 或被 Gatekeeper 阻止启动

该二进制使用 ad-hoc 签名。macOS 会对下载的文件添加隔离属性。运行一次下面的命令即可清除：
```bash
xattr -cr ~/.cloakbrowser/chromium-*/Chromium.app
```

---

### `playwright install` 与 CloakBrowser 二进制的关系

你**不需要**执行 `playwright install chromium`。CloakBrowser 会下载它自己的二进制。你只需要安装 Playwright 的系统依赖：
```bash
playwright install-deps chromium
```

---

### macOS 上被拦截，但同一站点在 Linux 上可通过

macOS 指纹配置目前存在一些已知不一致性，激进的机器人检测系统能够利用这些差异。如果某个站点在 macOS 上拦截你、但在 Linux 上可以通过，请传入 `stealth_args=False`，并手动设置 `--fingerprint-platform=windows` 及匹配的 GPU 标志（完整标志列表见 [指纹管理](#fingerprint-management)）。

---

### 站点检测到无痕 / 私密浏览模式

默认情况下，`launch()` 打开的是无痕上下文。一些站点会因此扣分。请改用 `launch_persistent_context()`，以获得带 cookie 持久化的真实配置文件：

```python
from cloakbrowser import launch_persistent_context

ctx = launch_persistent_context("./my-profile", headless=False)
```

如果站点仍然将其标记为无痕，可提高存储配额，让它看起来更像普通浏览会话。详见 [存储配额权衡](#launch_persistent_context)。

---

### reCAPTCHA v3 分数过低（0.1–0.3）

避免使用 `page.wait_for_timeout()`，因为它会发送 CDP 协议命令，而 reCAPTCHA 能检测到这些命令。请改用原生 sleep：

```python
# 错误示例：会发送 CDP 命令，reCAPTCHA 可检测到
page.wait_for_timeout(3000)

# 正确示例：对浏览器不可见
import time
time.sleep(3)
```

```javascript
// 错误示例：会发送 CDP 命令
await page.waitForTimeout(3000);

// 正确示例：对浏览器不可见
await new Promise(r => setTimeout(r, 3000));
```

其他提升 reCAPTCHA 分数的建议：
- **尝试 Patchright 后端** — 它会在 Playwright 协议层抑制更多 CDP 自动化信号。安装方式：`pip install cloakbrowser[patchright]`，然后使用 `launch(backend="patchright")`，或全局设置 `CLOAKBROWSER_BACKEND=patchright`。注意：Patchright 会破坏代理认证和 `add_init_script`，只有在尝试过上面的步骤后分数仍低时才建议使用
- **使用 Playwright，而不是 Puppeteer** — Puppeteer 会发送更多 CDP 协议流量，reCAPTCHA 能检测到这些流量（[详情](#puppeteer)）
- **使用住宅代理** — 机房 IP 被拦截通常是 IP 信誉问题，而不是浏览器指纹
- **在触发 reCAPTCHA 之前在页面停留 15 秒以上** — 停留时间太短通常分数更低
- **拉开请求间隔** — 同一会话中连续调用 `grecaptcha.execute()` 会被扣分。处理带 reCAPTCHA 的页面时，最好间隔 30 秒以上
- **使用固定指纹种子**，让设备身份在多次会话之间保持一致（见 [指纹管理](#fingerprint-management)）
- **表单填写优先使用 `page.type()`，不要用 `page.fill()`** — `fill()` 会直接设置值，不产生键盘事件，容易被 reCAPTCHA 的行为分析识别。`type()` 配合 delay 可模拟真实按键：
  ```python
  page.type("#email", "user@example.com", delay=50)
  ```
- **尽量减少 `page.evaluate()` 调用** — 在 reCAPTCHA 检查触发前，每次 `evaluate()` 都会发送一次 CDP 流量

## 常见问题

**Q：这合法吗？**
A：CloakBrowser 是基于开源 Chromium 构建的浏览器。我们不鼓励任何非法用途。未经授权的自动化操作、撞库以及滥用账号注册都被明确禁止。完整条款见 [BINARY-LICENSE.md](https://github.com/CloakHQ/CloakBrowser/blob/main/BINARY-LICENSE.md)。

**Q：它和 Camoufox 有什么不同？**
A：Camoufox 修改的是 Firefox，我们修改的是 Chromium。Chromium 意味着原生 Playwright 支持、更大的生态，以及与真实 Chrome 匹配的 TLS 指纹。Camoufox 在 2026 年初回归，但仍处于不稳定测试阶段；CloakBrowser 已可用于生产环境。

**Q：检测站点最终会不会识别出它？**
A：有可能。机器人检测本质上是一场军备竞赛。源码级补丁比配置级补丁更难检测，但并非绝对不可能。我们会持续监控并在检测方式演化时及时更新。

**Q：我可以使用自己的代理吗？**
A：可以。将 `proxy="http://user:pass@host:port"` 或 `proxy="socks5://user:pass@host:port"` 传给 `launch()` 即可。原生支持 HTTP 和 SOCKS5 代理。

## 路线图

| 功能 | 状态 |
|---------|--------|
| Linux x64 — Chromium 146（58 个补丁） | ✅ 已发布 |
| macOS arm64/x64 — Chromium 145（26 个补丁） | ✅ 已发布 |
| Windows x64 — Chromium 146（58 个补丁） | ✅ 已发布 |
| JavaScript / Puppeteer + Playwright 支持 | ✅ 已发布 |
| 按会话轮换指纹 | ✅ 已发布 |
| 内置代理轮换 | 📋 规划中 |

## 链接

- 📋 **更新日志** — [CHANGELOG.md](CHANGELOG.md)
- 🌐 **官网** — [cloakbrowser.dev](https://cloakbrowser.dev)
- 🐛 **Bug 报告与功能请求** — [GitHub Issues](https://github.com/CloakHQ/CloakBrowser/issues)
- 📦 **PyPI** — [pypi.org/project/cloakbrowser](https://pypi.org/project/cloakbrowser/)
- 📦 **npm** — [npmjs.com/package/cloakbrowser](https://www.npmjs.com/package/cloakbrowser)
- ☕ **支持项目** — [ko-fi.com/cloakhq](https://ko-fi.com/cloakhq)
- 📧 **联系邮箱** — cloakhq@pm.me

## 安全

所有发布版本都经过签名，用于供应链校验。

```bash
# 验证 GPG 签名（二进制发布 tag）
gpg --keyserver keyserver.ubuntu.com --recv-keys C60C0DDC9D0DE2DD
git verify-tag chromium-v146.0.7680.177.5

# 验证 GitHub 二进制证明（Sigstore）
gh attestation verify cloakbrowser-linux-x64.tar.gz --repo CloakHQ/cloakbrowser

# 验证 Docker 镜像签名（Cosign / Sigstore）
cosign verify \
  --certificate-identity-regexp "https://github.com/CloakHQ/CloakBrowser/" \
  --certificate-oidc-issuer "https://token.actions.githubusercontent.com" \
  cloakhq/cloakbrowser:latest
```

## 许可证

- **包装器代码**（本仓库）— MIT。见 [LICENSE](https://github.com/CloakHQ/CloakBrowser/blob/main/LICENSE)。
- **CloakBrowser 二进制**（编译后的 Chromium）— 可免费使用，但不可再分发。见 [BINARY-LICENSE.md](https://github.com/CloakHQ/CloakBrowser/blob/main/BINARY-LICENSE.md)。

## 贡献

欢迎提交 Issue 和 PR。如果有任何功能异常，请[提一个 issue](https://github.com/CloakHQ/CloakBrowser/issues)；我们响应很快。

## 贡献者

- [@evelaa123](https://github.com/evelaa123) — humanize 行为、持久上下文、Windows 修复
- [@yahooguntu](https://github.com/yahooguntu) — 持久上下文
- [@kitiho](https://github.com/kitiho) — 空 viewport 修复
- [@eofreternal](https://github.com/eofreternal) — humanConfig 类型修复、人类化方法选项类型修复
- [@manaskarra](https://github.com/manaskarra) — humanized frame actions 的 iframe 作用域修复、GeoIP 超时保护
- [@Youhai020616](https://github.com/Youhai020616) — SOCKS5 凭证编码日志
- [@AlexTech314](https://github.com/AlexTech314) — AWS Lambda 集成、冷启动加固
- [@dgtlmoon](https://github.com/dgtlmoon) — 优雅处理 `pw.stop()` 清理
- [@zackycodes](https://github.com/zackycodes) — Chrome 扩展加载
- [@aaronjmars](https://github.com/aaronjmars) — 安全修复（shell 注入、依赖升级）
- [@Seryiza](https://github.com/Seryiza) — Nix / NixOS flake
- [@245678000000](https://github.com/245678000000) — package-lock 同步
- [@honor2030](https://github.com/honor2030) — cloakserve WebSocket origin 防护、可组合 JS 启动辅助函数
- [@0xlally](https://github.com/0xlally) — 安全报告（cloakserve 路径遍历、WebSocket origin 绕过）
