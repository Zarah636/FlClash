# FlClash Android“按需运行”后台定位临时修复

> [!IMPORTANT]
> **这是非官方临时兼容分支。**
>
> 本项目仅为 Android 版 FlClash 补充“始终允许”位置权限声明，用于缓解应用退到后台后无法读取 Wi-Fi SSID、导致“按需运行”失效的问题。
>
> 本项目不提供后续功能更新。待上游正式修复该问题后，本仓库将归档。

## 下载

请仅从本仓库的 [GitHub Releases](https://github.com/Zarah636/FlClash/releases/download/v0.8.94-background-location-temp.1/FlClash-0.8.94-arm64-v8a-background-location-dev.apk) 下载，并自行核对 SHA-256。

SHA-256：

```text
4324AC3947249802C53412A49F4D90D4DE9541D4D4F6E2A40CFE5DE7777BD486
```

## 项目用途

Android 版 FlClash 的“按需运行”需要读取当前 Wi-Fi SSID，以判断是否应当启动或停止代理。

Android 10 及以上系统对后台位置信息访问有额外限制。如果应用没有在 Android Manifest 中声明 `android.permission.ACCESS_BACKGROUND_LOCATION`，系统不会提供“始终允许”位置权限，应用退到后台后可能无法取得 SSID。

本分支只做一项功能改动：

```xml
<uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />
```

对应上游问题：[FlClash #2233](https://github.com/chen08209/FlClash/issues/2233)。

## 安装与使用

1. 下载并安装本仓库发布的 APK。
2. 进入 Android 系统的 FlClash 应用权限页面。
3. 将位置权限设为“始终允许”，并开启精确位置。
4. 建议将电池使用策略设为“不限制”，同时允许后台运行和自启动。
5. 在 FlClash 的“按需运行”设置中添加需要启动或停止代理的 Wi-Fi SSID。

不同 Android 厂商的权限入口名称可能略有差异。部分系统需要先授予“使用应用时允许”，再到应用详情页改为“始终允许”。

## APK 信息

| 项目 | 内容 |
| --- | --- |
| FlClash 版本 | `0.8.94` |
| 包名 | `com.follow.clash.dev` |
| 支持架构 | `arm64-v8a` |
| 最低 Android | Android 7.0（API 24） |
| 目标 SDK | 36 |
| 签名 | Android Debug，APK Signature Scheme v2 |
| 构建标记 | `PRE` |

## 限制与注意事项

- 这是非官方版本，不代表 FlClash 上游项目。
- 当前 APK 仅支持 `arm64-v8a`，不适用于 32 位 ARM 或 x86/x86_64 Android 设备。
- 包名为 `com.follow.clash.dev`，签名与官方版不同，因此会与官方 FlClash 并存，不能覆盖安装官方版本。
- 本临时版与官方版的数据彼此独立，订阅、配置和设置需要自行重新导入或配置。
- 本项目不提供应用内自动更新，也不能接收官方 APK 的覆盖升级。
- 右上角的 `PRE` 只表示预览构建渠道，不影响代理或权限功能。
- 本修改只补充后台位置权限声明，没有改变 FlClash 的后台服务和生命周期逻辑。
- 如果厂商系统冻结或终止 FlClash 进程，应用仍无法接收网络变化，后台切换可能延迟或失效。
- 本构建只验证了 APK Manifest、签名、SHA-256 和 ARM64 原生库，没有覆盖所有 Android 厂商系统及机型。
- 使用非官方 Debug 签名 APK 的风险由使用者自行承担。

## 维护状态

- 本仓库只处理“按需运行缺少始终允许位置权限”这一项问题。
- 不计划跟随上游持续更新，不增加其他功能。
- 不保证提供安全更新、依赖更新、系统兼容性更新或技术支持。
- 上游正式修复 [FlClash #2233](https://github.com/chen08209/FlClash/issues/2233) 后，本仓库将停止发布并归档。
- FlClash 的版权、商标、功能和后续维护归原项目及其贡献者所有。