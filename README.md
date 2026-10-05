<!-- managed test distribution: Farm Tracker / Local DRF Core -->
# Local DRF Core — 本地桥接

当前版本：**0.2.2 预发布测试版（prototype）**。作者：Assumine。

[下载 Local_DRF_Core.dll](https://github.com/Assumine/GW2-LocalDRFCore/releases/download/v0.2.2/Local_DRF_Core.dll) · [版本页面](https://github.com/Assumine/GW2-LocalDRFCore/releases/tag/v0.2.2)

每个发布仓库只有一个顶层 DLL，Nexus GitHub 更新器可正确识别。需要允许预发布版本；旧手动版首次须手动升级。

# Farm Tracker 打金追踪 — 测试版安装说明

本包提供 Farm Tracker 0.11.9 与 Local DRF Core 0.2.2，均为 prototype 测试版。
包含两个自制插件；Nexus、原版 DRF 和个人数据不包含在本包中。

## 功能

实时记录本次游玩的物品和钱包货币增减，显示净收益、每小时估值和会话时间。
支持主窗口／悬浮窗、物品平铺／列表、收藏、中文悬停介绍、会话历史和收益曲线／柱状图。
名称、说明、图标和报价可以本地缓存，重启时优先读取；无需 API Key。

## 安装步骤

1. 退出 Guild Wars 2。
2. 先安装 [Nexus](https://raidcore.gg/gw2/nexus)。本包使用 Nexus API 6。
3. 将包内 `addons/Farm_Tracker.dll` 和 `addons/Local_DRF_Core.dll` 复制到游戏安装目录的 `addons` 文件夹。
   游戏安装目录是包含 `Gw2-64.exe` 的目录，不是「文档」中的 Guild Wars 2 目录。
4. 另行安装受支持的原版 DRF，将其 `drf.dll` 放入同一个 `addons` 文件夹。
5. 启动游戏，在 Nexus「已安装」中检查 Farm Tracker 与 Local DRF Core 的加载状态。
   涉及桥接的更新或切换状态，请退出游戏后操作，再重新启动。

安装完成后的结构应为：

```text
Guild Wars 2/
├─ Gw2-64.exe
├─ d3d11.dll                  ← Nexus，由玩家另行安装
└─ addons/
   ├─ Farm_Tracker.dll         ← 本包
   ├─ Local_DRF_Core.dll       ← 本包
   └─ drf.dll                 ← 原版 DRF，由玩家另行安装
```

`Farm_Tracker.dll` 与第三方 `_FarmingTracker.dll` 是不同插件。本包不需要第三方 FarmingTracker。
缺少兼容的数据源时，本插件仍能打开界面，但会等待数据，无法记录新的实时增量。

## DRF 兼容范围

当前桥接只接受经过校验的确切 DRF 文件：

| 版本 | SHA-256 | 已有验证情况 |
| --- | --- | --- |
| 1.9.12 | `49c5bda80bbf21ec161c5ca7655f47669f0d97682053b1b32692fe3f8faf54d3` | 已有真实增量验证记录 |
| 1.9.13 | `27416ed368414c0fcf67295a31165f5206394497b5cf804975060acc81cc4e00` | 静态校验通过；完整真实增量、卸载与恢复认证仍待补齐 |

请从 DRF 作者或 Nexus 对应渠道安装原版 DRF。最新下载可能变成其他版本，
不能仅凭文件名或版本号认定兼容。不支持的文件或函数签名不匹配时，桥接会停用并等待兼容更新。
原版 DRF 的分发授权由其作者决定，本包不附带原版或修改版 DRF。

## 使用

- `Ctrl+Shift+F`：打开主窗口。
- `Ctrl+Shift+M`：切换悬浮窗；也可恢复点击穿透后的交互。
- 三点菜单：暂停／继续、估值方式、会话历史、保存并重置等操作。
- 活动结束后选「保存并重置」，再打开「会话历史」并点击记录查看详情。
- Nexus 的插件配置中可设置背景透明度、悬浮窗、锁定和点击穿透。
- 主窗口和悬浮窗不会被 ESC 关闭；历史窗口和临时菜单仍可用 ESC 关闭。

## 收益与缓存

净收益是「金币变化＋物品变现估值变化」，不是账号金币余额。
卖给 NPC 的已有物品会抵扣其价值；交易所估值按约 15% 手续费扣除，实际成交价格和手续费舍入可能不同。
无法变现或缺资料的物品不会被假定成已经确认的收益。

缓存保存在 `addons/FarmTracker/cache/`，会话历史与配置也保存在 `addons/FarmTracker/`。
插件只查询公共物品／货币资料和交易所报价，不需要 API Key。
缓存中已有资料可在 API 暂时不可用时继续使用；未缓存的新物品仍需联网查询。
缓存报价会显示更新时间；历史图表使用保存时的估值依据，不代表每一秒当时的真实交易所成交价。

资料与图片查询使用 `api.guildwars2.com`、`render.guildwars2.com`。
Local DRF Core 阻断已知 DRF 上传端口 41206，DRF 的更新检查仍可联网。
该桥接仍依赖原版 DRF，不是完整独立替代品。

## 更新、卸载与反馈

两个插件分别使用独立公开仓库，由 Nexus 检查 GitHub Release 更新：
[打金追踪](https://github.com/Assumine/GW2-FarmTracker)／
[本地桥接](https://github.com/Assumine/GW2-LocalDRFCore)。
目前只发布预发布测试版，需要在 Nexus 对应插件的选项中打开「允许预发布版本／Allow prereleases」。
如看不到该选项，确认已使用本包新 DLL；旧手动版没有更新地址，首次必须退出游戏后手动替换。
之后可由 Nexus 检查更新；Local DRF Core 禁止热卸载，更新后需要重启游戏生效。
未允许预发布时，不会自动获取这些测试版。也可退出游戏后手动下载替换，并保留旧 DLL。
卸载前退出游戏，删除本包的两个 DLL 即可；如要保留历史，不要删除 `addons/FarmTracker/`。

出现问题时请提供本包版本、GW2／Nexus／DRF 版本、操作步骤、发生时间和 Windows 故障模块。
Nexus 日志位于 `addons/Nexus/Nexus.log`。分享日志或历史前请检查并遮挡个人信息。
报告问题请联系给你安装包的发布者。本包仍需第二台干净环境机器及完整真实游戏认证，
遇到异常可退出游戏后移除本包 DLL，并恢复此前备份。


本仓库仅用于二进制与使用文档分发，不包含开发仓库、原版 DRF、账号资料或日志。
