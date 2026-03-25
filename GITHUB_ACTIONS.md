# GitHub Actions 配置指南

本指南将帮助你将掘金签到项目配置为 GitHub Actions 定时任务，实现每天自动签到。

## 步骤 1：Fork 项目

1. 访问 [https://github.com/lucianaib0318/juejin-checkin](https://github.com/lucianaib0318/juejin-checkin)
2. 点击右上角的 "Fork" 按钮，将项目复制到你的 GitHub 账号

## 步骤 2：设置 Secrets

在你的 fork 仓库中，需要设置以下 Secrets：

1. 点击仓库右上角的 "Settings" → "Secrets and variables" → "Actions"
2. 点击 "New repository secret" 按钮，添加以下 secrets：

| Secret 名称 | 描述 | 获取方法 |
|------------|------|----------|
| `JUEJIN_COOKIE` | 掘金 Cookie | 从浏览器开发者工具获取 |
| `JUEJIN_UUID` | 掘金 UUID | 从浏览器请求中获取 |
| `JUEJIN_MS_TOKEN` | 掘金 msToken | 从浏览器请求中获取（需要 URL 解码） |
| `JUEJIN_A_BOGUS` | 掘金 a_bogus | 从浏览器请求中获取 |
| `NOTIFY_METHOD` | 通知方式（可选） | 可选值：feishu, telegram, wechat |
| `WEBHOOK_URL` | 通知 Webhook URL（可选） | 飞书或企业微信的 webhook 地址 |
| `TELEGRAM_BOT_TOKEN` | Telegram Bot Token（可选） | Telegram Bot 的 token |
| `TELEGRAM_CHAT_ID` | Telegram Chat ID（可选） | Telegram 聊天 ID |

## 步骤 3：启用 GitHub Actions

1. 在你的 fork 仓库中，点击 "Actions" 标签
2. 点击 "I understand my workflows, go ahead and run them" 按钮
3. 你应该能看到 "Juejin Checkin" 工作流

## 步骤 4：验证配置

1. 点击 "Juejin Checkin" 工作流
2. 点击 "Run workflow" 按钮，手动触发一次执行
3. 查看执行结果，确保签到成功

## 定时设置

工作流默认配置为每天 **UTC 时间 0:30** 运行，对应 **北京时间 8:30**。

如果你需要调整时间，可以修改 `.github/workflows/checkin.yml` 文件中的 cron 表达式：

```yaml
cron: '30 0 * * *'  # 北京时间 8:30
```

## 查看执行结果

1. 在仓库的 "Actions" 标签页中，你可以查看每次执行的详细日志
2. 如果配置了通知，执行结果会通过你设置的通知方式发送

## 故障排除

### 签到失败
- **原因**：Cookie 过期或无效
- **解决**：重新获取最新的 Cookie 并更新 `JUEJIN_COOKIE` secret

### 通知失败
- **原因**：Webhook URL 或 Telegram 配置错误
- **解决**：检查通知配置并确保正确设置

### 执行超时
- **原因**：网络问题或 API 响应缓慢
- **解决**：GitHub Actions 会自动重试，或手动触发执行

## 注意事项

1. **安全性**：不要在代码中硬编码任何敏感信息，所有配置都通过 Secrets 管理
2. **可靠性**：定期检查 Cookie 是否过期，建议每 1-2 个月更新一次
3. **合规性**：使用本项目时，请遵守掘金平台的相关规定

## 贡献

如果你有任何改进建议或发现问题，欢迎提交 Issue 或 Pull Request！
