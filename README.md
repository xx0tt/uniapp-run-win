# Uniapp Run Win 安装说明

## 安装

1. 禁用或卸载原扩展 `hb0730.uniapp-run`。
2. 首选在 VS Code 的扩展视图中点击 `...`，选择“从 VSIX 安装...”，再选择团队交付的 VSIX 文件。
3. 也可以在包含所交付 VSIX 的目录中运行以下命令；如果在其他目录运行，请改用 VSIX 的绝对路径：

   ```powershell
   code --install-extension .\uniapp-run-win-0.1.0.vsix --force
   ```

4. 重新加载 VS Code。
5. 保留现有设置 `uniapp-run.HBuilderX` 和 `uniapp-run.wxDevtool`，无需迁移或改名。

## 项目配置

团队共享的 `.vscode/launch.json` 不需要写入绝对 `src` 路径。可使用以下配置：

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "uniapp-run",
      "request": "launch",
      "name": "运行到微信小程序",
      "platform": "mp-weixin",
      "vueVersion": "v2",
      "openDevTool": true,
      "compress": true
    }
  ]
}
```

## 验证

打开命令面板并运行“发布uniapp”（命令 ID：`uniapp-run.publish`）以执行生产构建；若出现选择提示，请选择 `mp-weixin` 的共享配置。此流程不同于按 F5 启动的开发调试。

生产打包日志中的 `WorkPath` 应使用大写驱动器盘符，例如：

```text
WorkPath: D:\work\miniapp\eBikeLicenseSeller
```

构建日志应显示 `Build complete`，且不应出现 `No module factory available for dependency type: CssDependency`。

## 升级

在 VS Code 的扩展视图中点击 `...`，选择“从 VSIX 安装...”，并选择新交付的 VSIX。也可以用命令行安装，将 `VERSION` 替换为实际交付的版本号：

```powershell
code --install-extension .\uniapp-run-win-VERSION.vsix --force
```

不要同时启用上游扩展和本 fork：两者注册相同的命令和调试器 ID。
