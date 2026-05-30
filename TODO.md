# 角色管理插件 TODO

## 变更记录

### 6.71
- **版本号**：6.71（内部 version: 20260531）
- **改动点**：
  1. 删除 `onLoadUI` 内部覆盖 `EditorJS` 的残代码（约第 3233 行），避免下次打开设置页面时执行残缺的 `onLoadUI`。
  2. 删除重复的 `refreshCharacterData`（保留从 `shuming.当前书籍.json` 读取的版本，与 6.69 设计保持一致）。
  3. 修复 `restoreBackup`：恢复备份后补上 `replaceFayinrenName` 正向映射，避免恢复后发音人显示为存储值。
  4. 修复释放别名创建新角色时 `voice` 硬编码为空字符串的问题，改为继承原角色发音人（`character.voice || "默认发音人"`）。
  5. 删除 `onLoadUI` 内部后面重复定义的 `getCurrentBookName`、`getBookList`、`saveCurrentBookBeforeSwitch`、`useBook` 函数组。
  6. 删除全局作用域中多余的 `saveCurrentBookBeforeSwitch`、`useBook` 函数定义（约第 5410 行），避免操作全局未初始化的 `characterRecords`。
- **新增/修复**：解决角色列表不显示/丢失发音人的问题；清理代码中大量重复/冗余函数定义。

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
- **当前版本**：6.71
- **主目录结构**：
  ```
  ttsrv-plugin/
  ├── AGENTS.md
  ├── .gitignore
  ├── TODO.md
  ├── ttsrv-plugin-角色管理6.71.json
  └── 历史版本/
      ├── ttsrv-plugin-角色管理6.65.json
      ├── ttsrv-plugin-角色管理6.66.json
      ├── ttsrv-plugin-角色管理6.67.json
      ├── ttsrv-plugin-角色管理6.68.json
      └── ttsrv-plugin-角色管理6.69.json
  ```
- **已完成事项**：
  - 备份并创建 6.71 版本文件（基于 6.70 修复）。
  - 删除 `onLoadUI` 内部覆盖 `EditorJS` 的残代码，避免下次打开设置页面执行残缺 `onLoadUI`。
  - 删除重复的 `refreshCharacterData`，保留从 `shuming` 读取的版本。
  - 修复 `restoreBackup`：恢复备份后补上 `replaceFayinrenName` 正向映射。
  - 修复释放别名：新角色继承原角色发音人（不再硬编码为空字符串）。
  - 删除 `onLoadUI` 内部后面重复的书籍切换函数组。
  - 删除全局作用域中多余的 `saveCurrentBookBeforeSwitch`、`useBook` 函数定义。
  - 更新 TODO.md 变更记录。
  - Git 提交并推送到远程仓库。
- **仓库与推送**：
  - GitHub 新仓库 `misscafes/ttsrv-plugin` 已创建并推送成功：`https://github.com/misscafes/ttsrv-plugin`
  - cnb.cool 远程 `misscafe.eec/ttsrv-plugin` 已强制推送同步，旧历史已备份到 `backup` 分支。origin 已配置双推（GitHub + cnb.cool）。
- **注意事项**：
  - 6.71 主要解决角色列表不显示/丢失发音人的问题，根源是代码中存在大量重复/冗余函数定义及残缺的 `EditorJS` 覆盖代码。
  - `js/` 目录和 `extract-js.js` 尚未初始化，如需提取 JS 请先生成脚本。
