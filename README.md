# notify-icons

Bark 通知图标（自托管，走 jsDelivr CDN）。

线上各服务的 Bark 通知通过 `icon` 参数引用本仓库的图片：

    https://cdn.jsdelivr.net/gh/weimin826/notify-icons@main/<file>.png

## 图标清单

| 文件 | 用途 | 说明 |
|---|---|---|
| `alipay_wm_v3.png` | 伟民 · 基金买卖提示 | 支付宝官方底图，「支」缩 38%，左上角透光「伟」 |
| `alipay_yz_v3.png` | 宇智 · 基金买卖提示 | 同上，左下角透光「宇」 |
| `ths.png` | 东吴持仓（holdings-rescue） | 东吴证券 App 官方图标 |
| `em.png` | 东方持仓（holdings-rescue-em） | 东方财富 App 官方图标 |
| `okx.png` | OKX 机器人 | OKX App 官方图标 |
| `paper.png` | A股量化模拟盘 | 自绘：深蓝底 + 白色柱状 + 绿色涨势线 |

另有 `_v1` / `_v2` 历史版本，仅作留存，线上已不用。

## ⚠️ 换图必须换文件名

**手机端按 URL 缓存图标** —— 同名文件换内容**不会**生效。改版一律升版本号
（`_v2` → `_v3`），再更新各服务 `.env` 里的 `BARK_ICON`。

## 图标设计要点

- 合成用 **滤色（`ImageChops.screen`）**，不是半透明覆盖 —— 只提亮、不遮盖底图笔画。
- 底图是压平的 JPEG，要挪/缩其中的字必须先**重建背景**（6 阶二维多项式最小二乘，残差 RMS ≈1.3/255）。
- **iOS 会对通知图标做圆角/圆形遮罩**：边距 m（512 基准）需 ≥ 33px(6.5%) 才不被圆角裁、
  ≥ 75px(14.6%) 才不被圆形裁。当前 v3 用 69px。
- 验收必须**套遮罩在真实 60px 下看** —— 512px 预览会骗人。

## 换图流程

```bash
# 1) 生成（本地，需 Pillow + numpy）
python gen_final_icons_v4.py          # 支付宝账号图标
python build_icon_set.py              # 汇总整套
# 2) 上传（gh api，绕开 git 代理）
bash upload_icons_v3.sh
# 3) 校验 CDN（在 VPS 上做，本地会被沙箱代理的 MITM 证书挡住）
curl -s -o /tmp/a.png -w '%{http_code} %{size_download}' \
  https://cdn.jsdelivr.net/gh/weimin826/notify-icons@main/alipay_wm_v3.png
md5sum /tmp/a.png
# 4) 改各服务 .env 的 BARK_ICON，重启需要重读 env 的常驻服务
```
