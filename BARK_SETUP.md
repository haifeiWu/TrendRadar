# Bark 通知配置指南

Bark 是一款 iOS 推送通知应用,支持自托管服务器。TrendRadar 已集成 Bark 通知功能。

## 前置条件

1. iOS 设备上安装 Bark APP ([App Store 下载](https://apps.apple.com/cn/app/bark-customed-notifications/id1403753865))
2. 打开 APP 获取您的设备密钥 (Device Key)

## 配置步骤

### 方法一: 使用配置文件 (推荐)

编辑 `config/config.yaml` 文件:

```yaml
notification:
  webhooks:
    bark_server_url: "https://api.day.app"  # 官方服务器,也可以使用自托管服务器
    bark_device_key: "your_device_key_here"  # 从 Bark APP 中获取
```

### 方法二: 使用环境变量

在 Docker 环境中,编辑 `docker/.env` 文件:

```bash
BARK_SERVER_URL=https://api.day.app
BARK_DEVICE_KEY=your_device_key_here
```

或在 GitHub Actions 中设置 Secrets:
- `BARK_SERVER_URL`: Bark 服务器地址 (可选,默认为 https://api.day.app)
- `BARK_DEVICE_KEY`: 您的 Bark 设备密钥

## 获取 Device Key

1. 打开 Bark APP
2. 首页会显示您的推送 URL,格式类似: `https://api.day.app/your_device_key/测试内容`
3. 其中 `your_device_key` 就是您需要配置的设备密钥

## 使用自托管服务器

如果您部署了自己的 Bark 服务器:

```yaml
notification:
  webhooks:
    bark_server_url: "https://your-bark-server.com"
    bark_device_key: "your_device_key"
```

## 功能特性

- ✅ 支持消息分批发送 (单条消息不超过 4KB)
- ✅ 自动按反向顺序推送,确保手机上显示顺序正确
- ✅ 支持 Markdown 格式
- ✅ 消息自动归档到 "TrendRadar" 分组
- ✅ 支持点击跳转到新闻链接

## 推送示例

配置完成后,TrendRadar 会定时向您的 Bark 推送热点新闻汇总,包括:
- 📊 热点词汇统计
- 🔥 高频词汇新闻列表
- 🆕 新增热点新闻
- 📈 排名和时间信息

## 常见问题

**Q: 没有收到推送通知?**
- 检查 Device Key 是否正确
- 确保 iOS 设备已允许 Bark 通知权限
- 检查网络连接

**Q: 推送消息顺序混乱?**
- TrendRadar 已自动处理消息顺序,最新的批次会先推送,在 Bark 中显示时顺序是正确的

**Q: 可以同时使用多个通知渠道吗?**
- 可以!您可以同时配置 Bark、飞书、钉钉、Telegram 等多个通知渠道

## 参考文档

- [Bark 官方文档](https://bark.day.app/)
- [Bark GitHub](https://github.com/Finb/Bark)
