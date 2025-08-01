# 数据管理功能说明

## 功能概述

数据管理页面提供了对导航数据的完整管理功能，包括：

1. **恢复初始化数据** - 从 `navigation-default.json` 恢复默认数据（带文件存在性检查）
2. **在线JSON编辑** - 直接编辑 `navigation.json` 文件，支持语法验证和错误修复
3. **数据下载** - 将当前数据下载到本地
4. **实时保存** - 保存编辑后的数据到服务器
5. **系统状态监控** - 显示默认文件状态和当前数据统计
6. **键盘快捷键** - 支持 Ctrl+S 保存、Ctrl+R 刷新、Ctrl+D 下载

## 使用方法

### 1. 访问数据管理页面

登录管理后台后，在左侧菜单中点击"数据管理"即可进入。

### 2. 恢复初始化数据

- 点击"恢复初始化数据"按钮
- 在确认对话框中点击"确认恢复"
- 系统会将 `navigation-default.json` 的内容覆盖到 `navigation.json`

### 3. 编辑数据

- 在JSON编辑器中直接修改数据
- 编辑器支持语法高亮和格式化
- 确保JSON格式正确，否则无法保存

### 4. 保存数据

- 编辑完成后点击"保存数据"按钮
- 系统会验证JSON格式
- 保存成功后会显示成功提示

### 5. 下载数据

- 点击"下载到本地"按钮
- 系统会将当前数据以JSON格式下载到本地
- 文件名格式：`navigation-YYYY-MM-DD.json`

## 注意事项

1. **数据格式**：必须保持正确的JSON格式，否则无法保存
2. **权限要求**：需要管理员权限才能访问此功能
3. **备份建议**：在进行重要修改前，建议先下载当前数据作为备份
4. **恢复操作**：恢复初始化数据的操作不可撤销，请谨慎操作

## API接口

### GET /api/navigation
获取当前导航数据

### PUT /api/navigation
更新导航数据

### POST /api/navigation/restore
恢复默认数据（会检查 navigation-default.json 是否存在）

### GET /api/navigation/check-default
检查默认文件状态，返回文件是否存在、格式是否有效、分类数量等信息

## 文件结构

```
navsphere/content/
├── navigation.json          # 当前使用的导航数据
└── navigation-default.json  # 默认导航数据（用于恢复）
```

## 数据结构示例

```json
{
  "navigationItems": [
    {
      "id": "1",
      "title": "分类名称",
      "icon": "图标名称",
      "description": "分类描述",
      "enabled": true,
      "items": [
        {
          "id": "1_1",
          "title": "站点名称",
          "href": "https://example.com",
          "description": "站点描述",
          "icon": "/path/to/icon.png",
          "enabled": true
        }
      ],
      "subCategories": []
    }
  ]
}
```
## 新增
功能特性

### 1. 默认文件检查
- 自动检查 `navigation-default.json` 文件是否存在
- 验证默认文件的JSON格式是否正确
- 显示默认文件中的分类数量
- 如果默认文件不存在或格式错误，恢复按钮会被禁用

### 2. 美化的用户界面
- 现代化的卡片布局设计
- 实时数据统计显示（分类数量、站点数量、数据大小）
- 系统状态面板显示默认文件和当前数据状态
- 彩色状态徽章和图标

### 3. 专业的Monaco Editor JSON编辑器
- 基于VS Code核心的Monaco Editor
- 完整的JSON语法高亮和智能提示
- 实时错误检测和波浪线标记
- 代码折叠和括号匹配
- 自动缩进和格式化
- 查找替换功能 (Ctrl+F)
- 多光标编辑支持
- 主题跟随系统 (亮色/暗色模式)

### 4. 智能错误处理
- 详细的错误信息显示
- 错误位置定位功能
- 常见JSON错误的自动修复
- 友好的用户提示和建议

### 5. 丰富的键盘快捷键支持
- `Ctrl+S` / `Cmd+S`: 保存数据
- `Ctrl+R` / `Cmd+R`: 刷新数据
- `Ctrl+D` / `Cmd+D`: 下载数据
- `Alt+Shift+F`: 格式化JSON代码
- `Ctrl+F` / `Cmd+F`: 查找文本
- `Ctrl+H` / `Cmd+H`: 查找替换
- `Ctrl+/` / `Cmd+/`: 切换注释
- `Alt+Up/Down`: 移动行
- `Shift+Alt+Up/Down`: 复制行

### 6. 数据统计和预览
- 实时显示字符数、行数、文件大小
- 数据结构预览
- 分类和站点数量统计
- 格式验证状态显示

## 安全特性

1. **权限验证**: 所有API操作都需要管理员权限
2. **数据验证**: 严格的JSON格式验证和数据结构检查
3. **错误处理**: 完善的错误捕获和用户友好的错误提示
4. **操作确认**: 危险操作（如恢复默认数据）需要用户确认

## 技术实现

- **前端**: React + TypeScript + Tailwind CSS
- **JSON编辑器**: Monaco Editor (VS Code核心)
- **后端**: Next.js API Routes + Edge Runtime
- **数据存储**: GitHub Repository
- **UI组件**: shadcn/ui 组件库
- **状态管理**: React Hooks
- **错误处理**: 统一的错误处理机制
- **主题支持**: next-themes 自动切换亮色/暗色模式
## Monaco E
ditor 特性

### 智能编辑功能
- **语法高亮**: 完整的JSON语法高亮显示
- **智能提示**: 自动补全和代码建议
- **错误检测**: 实时JSON语法错误检测，错误位置用红色波浪线标记
- **括号匹配**: 自动高亮匹配的括号和大括号
- **代码折叠**: 支持JSON对象和数组的折叠/展开

### 编辑体验
- **多光标**: 支持多光标同时编辑
- **智能缩进**: 自动缩进和格式化
- **行号显示**: 清晰的行号显示
- **查找替换**: 强大的查找替换功能
- **撤销重做**: 完整的编辑历史记录

### 快捷操作
- **格式化**: Alt+Shift+F 一键格式化JSON
- **查找**: Ctrl+F 快速查找文本
- **替换**: Ctrl+H 查找并替换
- **移动行**: Alt+Up/Down 快速移动代码行
- **复制行**: Shift+Alt+Up/Down 快速复制代码行

### 主题支持
- **自动切换**: 根据系统主题自动切换亮色/暗色模式
- **VS Code风格**: 与VS Code编辑器保持一致的视觉体验
- **护眼模式**: 暗色主题减少眼部疲劳

## 使用建议

1. **大文件编辑**: Monaco Editor对大型JSON文件有良好的性能表现
2. **格式化**: 使用 Alt+Shift+F 快捷键可以快速格式化混乱的JSON代码
3. **错误定位**: 编辑器会自动标记JSON语法错误，鼠标悬停可查看详细错误信息
4. **查找替换**: 使用 Ctrl+F 可以快速定位特定内容，Ctrl+H 可以批量替换
5. **代码折叠**: 对于复杂的JSON结构，可以折叠不需要编辑的部分以提高可读性