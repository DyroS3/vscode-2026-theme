# 2026 Theme (Dark & Light)

将 VS Code 2026 版内置的 **默认深色 / 默认浅色** 主题提取为一个独立、可维护的扩展。安装后会在主题选择器中新增 **2026 深色**（`2026 Dark`）与 **2026 浅色**（`2026 Light`）两个配色。

适用于 **Cursor** 或尚未内置这两个主题的旧版 VS Code。

---

## 主题来源与还原方式

这两个主题在官方实现里并非独立文件，而是基于 `include` 链层层覆盖。本扩展**原样保留了整条链**，因此渲染效果与官方 1:1 一致：

| 主题 | include 链 |
|------|-----------|
| `2026 Dark` | `2026-dark.json` → `dark_modern.json` → `dark_plus.json` → `dark_vs.json` |
| `2026 Light` | `2026-light.json` → `light_modern.json` → `light_plus.json` → `light_vs.json` |

`themes/` 目录中的 8 个 JSON 均为官方原始文件，未做任何改动。`2026-*.json` 只包含在 Modern 主题之上的颜色覆盖与一套 GitHub 风格的 `tokenColors`。

---

## 安装

### 方式一：开发版直装（最快，适合自用 / 调试）

把整个 `vscode-2026-theme` 文件夹复制到编辑器的扩展目录，然后重启编辑器：

- Cursor：`%USERPROFILE%\.cursor\extensions\`
- VS Code：`%USERPROFILE%\.vscode\extensions\`

建议复制后将文件夹命名为 `local-themes.vscode-2026-theme-1.0.0`，以符合扩展目录的命名习惯。

### 方式二：打包成 VSIX 再安装（适合分发 / 长期维护）

```bash
npm install -g @vscode/vsce
cd vscode-2026-theme
vsce package
```

生成 `vscode-2026-theme-1.0.0.vsix` 后，在命令面板执行 **Extensions: Install from VSIX...** 选择该文件即可。

> 发布到市场前，请先在 `package.json` 中把 `publisher` 改成你自己的发布者 ID，并补充 `repository` 字段。

---

## 使用

命令面板（`Ctrl+K Ctrl+T`）→ **Color Theme** → 选择 **2026 深色** 或 **2026 浅色**。

也可直接写入设置：

```json
{
  "workbench.colorTheme": "2026 Dark"
}
```

---

## 维护：如何从上游同步更新

当 VS Code 更新了这两个主题时，只需用最新的官方文件覆盖 `themes/` 下对应文件即可。官方文件位于安装目录：

```
<VS Code 安装目录>\resources\app\extensions\theme-defaults\themes\
```

需要同步的文件：`2026-dark.json`、`2026-light.json`、`dark_modern.json`、`light_modern.json`、`dark_plus.json`、`light_plus.json`、`dark_vs.json`、`light_vs.json`。

随后按需在 `CHANGELOG.md` 记录版本变化、提升 `package.json` 的 `version`。

---

## 本地化标签

主题在选择器中的显示名通过 `package.nls.json`（英文）与 `package.nls.zh-cn.json`（简体中文）提供：中文环境显示「2026 深色 / 2026 浅色」，其余环境显示「2026 Dark / 2026 Light」。

---

## 发布到市场前的清单（已做好准备，但有意未发布）

> 本扩展已具备发布条件，但**当前不发布到市场**。将来若要发布，请按以下步骤：

1. 把 `package.json` 的 `publisher` 改为你在市场注册的发布者 ID（当前为占位值 `local-themes`）。
2. 仓库地址已指向 `https://github.com/DyroS3/vscode-2026-theme`，如需更换可自行修改 `repository` / `bugs` / `homepage`。
3. 在 Azure DevOps 创建发布者的 Personal Access Token。
4. 执行 `vsce login <publisher>`，随后 `vsce publish`（或 `vsce publish minor` 自动升版本号）。

## 许可与署名

本扩展中的主题文件版权归 Microsoft Corporation 所有，遵循 MIT 许可（源自 VS Code 的 `theme-defaults` 扩展）。本扩展同样以 MIT 许可分发，详见 `LICENSE`。
