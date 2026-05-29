# 角色管理插件 TODO

## 变更记录

### 6.69
- **版本号**：6.69（内部 version: 61）
- **改动点**：
  1. 修复 `refreshCharacterData`：不再始终读取全局 `characterRecords.json`，改为根据 `cunfang.txt` 获取当前书籍名，从对应的 `shuming.当前书籍.json` 加载角色数据。
  2. 修复后同步调用 `initBookSpinner()`，确保书籍下拉框与当前书籍保持一致。
- **新增/修复**：解决书籍切换后角色列表仍显示旧数据的问题；解决角色列表不显示已分配角色（发音人）的问题。

### 6.68
- **版本号**：6.68（内部 version: 61）
- **改动点**：
  1. 重构 `showReleaseSingleDialog`：释放单个时列出所有可释放的**具体别名**（带所属角色提示），支持**多选**。
  2. 新增 `doReleaseSelectedAliases`：按角色分组处理被选中的别名，仅释放用户勾选的别名，其余别名保留在原角色中。
  3. 按角色索引降序处理，避免插入新角色导致后续索引错位。
- **新增/修复**：避免一次性释放角色全部别名，支持精细化选择要拆分的别名。

### 6.67
- **版本号**：6.67（内部 version: 60）
- **改动点**：
  1. 重构 `doReleaseOperation`：释放角色时新增选择对话框，提供 **"释放全部"** 与 **"释放单个"** 两个选项。
  2. 新增 `showReleaseSingleDialog`：选择"释放单个"时弹出角色列表，仅从当前已选中的、且带有别名的角色中选择目标。
  3. 新增 `doReleaseAllOperation` 与 `doReleaseSingleOperation`，分别处理批量释放与单角色释放逻辑。
- **新增/修复**：避免误操作释放全部角色，支持精确释放单个角色的别名。

### 6.66
- **版本号**：6.66（内部 version: 59）
- **改动点**：
  1. 删除"更换发音人"搜索对话框快捷关键词中的"核心女"、"核心男"按钮（从 `PRESET_KEYWORDS_ROW3` 移除）。
  2. 删除3处"选择操作"长按菜单中的"设为核心女"、"设为核心男"选项，并重新编号后续 `switch/case`。
- **新增/修复**：功能精简，移除不再使用的核心角色快捷操作入口。

### 6.65
- **版本号**：6.65（内部 version: 58）
- **改动点**：基线版本，包含完整的角色管理功能。

## 会话摘要

### 2026-05-30
- **当前版本**：6.69
- **主目录结构**：
  ```
  ttsrv-plugin/
  ├── AGENTS.md
  ├── .gitignore
  ├── TODO.md
  ├── ttsrv-plugin-角色管理6.69.json
  └── 历史版本/
      ├── ttsrv-plugin-角色管理6.65.json
      ├── ttsrv-plugin-角色管理6.66.json
      ├── ttsrv-plugin-角色管理6.67.json
      └── ttsrv-plugin-角色管理6.68.json
  ```
- **已完成事项**：
  - 备份并创建 6.66 版本文件。
  - 从 `PRESET_KEYWORDS_ROW3` 移除"核心女"、"核心男"。
  - 从3个 `showFirstDialog` 的 options 数组中移除"设为核心女"、"设为核心男"。
  - 同步调整3处 `switch/case` 编号。
  - 更新顶层及 code 内部的 `name` 和 `version` 字段。
  - 备份并创建 6.67 版本文件。
  - 重构 `doReleaseOperation`，新增释放全部/释放单个选择对话框。
  - 新增 `showReleaseSingleDialog`、`doReleaseAllOperation`、`doReleaseSingleOperation`。
  - 备份并创建 6.68 版本文件。
  - 重构 `showReleaseSingleDialog`：列出所有具体别名，支持多选释放。
  - 新增 `doReleaseSelectedAliases`，仅释放被选中的别名。
  - 备份并创建 6.69 版本文件。
  - 修复 `refreshCharacterData`：按当前书籍加载 `shuming.XXX.json`，同步刷新 `initBookSpinner`。
- **仓库与推送**：
  - GitHub 新仓库 `misscafes/ttsrv-plugin` 已创建并推送成功：`https://github.com/misscafes/ttsrv-plugin`
  - cnb.cool 远程 `misscafe.eec/ttsrv-plugin` 已强制推送同步，旧历史已备份到 `backup` 分支。origin 已配置双推（GitHub + cnb.cool）。
- **注意事项**：
  - `setAsCoreFemaleCharacter()` 和 `setAsCoreMaleCharacter()` 函数定义仍保留在代码中（仅移除了菜单入口）。
  - `js/` 目录和 `extract-js.js` 尚未初始化，如需提取 JS 请先生成脚本。
