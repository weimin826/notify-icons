# notify-icons

自用 Bark(iOS) 推送通知图标。**公开仓库，仅存放图片，无任何敏感信息。**

供 iOS Bark App 的 `icon` 参数使用（手机端会按 URL 缓存图标，因此改图必须换文件名）。

## jsDelivr 直链

| 文件 | 用途 | 直链 |
|---|---|---|
| `alipay_wm_v1.png` | 支付宝理财 · **伟民** 账户（右上角透光「伟」） | `https://cdn.jsdelivr.net/gh/weimin826/notify-icons@main/alipay_wm_v1.png` |
| `alipay_yz_v1.png` | 支付宝理财 · **宇智** 账户（右上角透光「宇」） | `https://cdn.jsdelivr.net/gh/weimin826/notify-icons@main/alipay_yz_v1.png` |

底图取自 App Store 官方 支付宝 App（`com.alipay.iphoneclient`）artwork，
叠加方式为滤色(screen)混色 —— 只提亮、不遮盖原「支」logo，形成"隐现"效果。

## 换图流程

1. 用新配方的图覆盖（或新增 `*_v2.png`）
2. 推送
3. 把消费方（如 VPS 上的 `BARK_ICON`）指向**新文件名**

> ⚠️ 不要原地覆盖同名文件：Bark 客户端按 URL 缓存，同 URL 只会下载一次，覆盖后手机端看到的仍是旧图。
