# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个基于纯 HTML/JavaScript 开发的在线画图工具（类似简易版 Photoshop）。无需构建工具，直接打开 `index.html` 即可运行。

## 技术栈

- **jQuery 1.7.2** - DOM 操作和事件处理
- **jQuery EasyUI** - UI 组件框架（菜单、对话框、选项卡等）
- **Mousetrap** - 键盘快捷键库
- **RulersGuides.js** - 标尺和参考线功能（第三方库）
- **jPicker** - 颜色选择器

## 核心架构

### 双画布系统
应用使用双层 canvas 设计：
- `#showcanvas` - 最终展示层（z-index: 2），存储已完成的绘制内容
- `#tempcanvas` - 临时绘图层（z-index: 1），用于实时预览绘制过程
- `#gridcanvas` - 网格层，可切换显示

每次鼠标移动时先清空 tempcanvas 进行预览绘制，鼠标松开时将内容固化到 showcanvas。

### 核心变量 (main.js:10-90)
```javascript
var showcanvas, show;        // 最终展示画布及上下文
var tempcanvas, temp;         // 临时画布及上下文
var isMouseDown;              // 鼠标状态
var startX, startY;           // 绘制起始坐标
var drawObject;               // 当前选中的工具（如 "btnPencil"）
var imageHistoryList;         // 撤销/重做历史栈
```

### 绘图工具
工具箱位于 `index.html:505-552`，支持 20+ 种工具：
- 基础工具：选择(S)、移动(M)、套索(A)、缩放(Z)、手抓(H)
- 绘图工具：画笔(B)、铅笔(P)、橡皮擦(E)、填充(F)、渐变(N)
- 形状工具：直线(L)、曲线(V)、矩形(R)、椭圆(I)、三角形(G)、多边形(Y)
- 其他：裁剪(C)、文本(T)、图章(X)、透明度(D)

### 图层系统
- 每个图层对应一个独立的 canvas 元素
- `levelList` 数组管理所有图层对象
- 支持新建、删除、复制、上移、下移图层
- 背景图层默认存在且可隐藏

### 撤销/重做系统
- `imageHistoryList` 存储历史状态（保存快照）
- `undo()` / `redo()` 函数实现撤销重做
- 操作后需调用 `saveHistory()` 保存状态

### 快捷键系统
快捷键定义在 `keypressEvent.js`，使用 Mousetrap 库绑定：
- `Ctrl+Z` - 撤销
- `Ctrl+Y` - 重做
- `Ctrl+G` - 打开文件
- `S/M/A/Z...` - 切换工具

## 文件结构

```
zaixianhuatu/
├── index.html              # 主入口文件
├── CSS/
│   └── main.css           # 主样式文件
├── JScript/
│   ├── jquery-1.7.2.min.js
│   ├── jquery-easyui/      # EasyUI 框架
│   ├── jpicker-1.1.6/      # 颜色选择器
│   ├── Mousetrap/          # 快捷键库
│   ├── RulersGuides/       # 标尺参考线（第三方）
│   └── CodeJS/
│       ├── main.js         # 核心逻辑（约 1000+ 行）
│       ├── keypressEvent.js # 快捷键绑定
│       ├── changeTheme.js  # 主题切换
│       └── fullscreen.js   # 全屏功能
├── Images/
│   ├── tools/             # 工具图标
│   └── files/             # 示例图片
└── Code/
    └── SelectImg.html     # 图片选择弹窗
```

## 部署方式

1. 将所有文件上传到服务器
2. 配置 nginx 指向项目目录
3. 配置域名解析（部署示例：zaixianhuatu.itzhouq.cn）

无需任何构建步骤或后端服务（除保存图片功能外）。

## 常见修改位置

- 添加新工具：修改 `index.html` 工具箱区域 + `main.js` 绘图逻辑
- 修改样式：编辑 `CSS/main.css` 或 `index.html` 内联样式
- 添加菜单项：修改 `index.html` 菜单区域 + `main.js` 菜单点击事件
- 主题切换：`changeTheme.js` 处理 EasyUI 主题切换
