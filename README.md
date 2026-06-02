
# PomodoroClock

一个本地 Windows 桌面番茄钟工具。程序已打包为 PyInstaller `onedir` 形式，下载发布包后双击 `PomodoroClock.exe` 即可运行，不需要打开命令行，也不需要安装 Python。

## 下载方式

请前往本项目右侧的 **Releases** 页面，下载最新版本中的：

```text
PomodoroClock.zip
```

不要直接点击 GitHub 自动生成的：

```text
Source code (zip)
Source code (tar.gz)
```

这些不是完整运行包，不能直接运行程序。

## 运行方式

下载 `PomodoroClock.zip` 后，完整解压。解压后的目录结构应类似：

```text
PomodoroClock/
├─ PomodoroClock.exe
├─ _internal/
├─ README.md
└─ .gitignore
```

双击运行：

```text
PomodoroClock.exe
```

注意：`PomodoroClock.exe` 不能脱离 `_internal/` 单独运行。`_internal/` 中包含 PySide6、Qt 插件和 Python 运行时依赖。删除、改名、移动 `_internal/` 后，程序会无法启动。

## 功能概览

- 番茄钟计时：开始 / 暂停、重置、跳过当前阶段。
- 专注与休息时长设置：默认专注 25 分钟，休息 5 分钟，可在设置中修改。
- 当前时间与日期显示：可单独开启或关闭。
- 卡片模式：半透明悬浮卡片，支持置顶、拖动和缩放。
- 极简模式：透明卡片区域，核心文字常显，鼠标悬停时显示操作按钮。
- 点击倒计时编辑：点击 `25:00` 这类倒计时文本，可直接修改当前阶段计时。
- 外观设置：支持透明度、字体、字号、文字颜色、显示样式和布局密度。
- 本地配置保存：关闭后再次打开会恢复上次设置。

## 基本操作

启动后默认显示卡片模式。常用操作如下：

- 点击 `开始`：开始或暂停当前计时。
- 点击 `重置`：重置当前阶段计时。
- 点击 `跳过`：切换到下一阶段。
- 点击倒计时数字：编辑当前阶段剩余时间。
- 右键窗口：打开快捷菜单。
- 拖动窗口空白区域：移动窗口。
- 拖动窗口边缘或角落：调整窗口大小。
- 点击 `设置`：修改时长、透明度、字体、颜色、显示模式等。

倒计时编辑支持以下输入格式：

```text
25      -> 25 分钟
90      -> 90 分钟
25:00   -> 25 分 0 秒
1:30    -> 1 分 30 秒
00:30   -> 30 秒
```

## 显示模式说明

### 卡片模式

卡片模式用于常规桌面悬浮显示，包含完整卡片背景、状态文字、倒计时、当前时间、日期、设置按钮和控制按钮。

### 极简模式

极简模式保留透明卡片区域，默认主要显示倒计时、当前时间和日期。鼠标移入窗口区域时显示开始、重置、跳过等操作按钮；鼠标移出后按钮自动隐藏。

## 配置文件位置

Windows 打包版的配置文件保存在：

```text
%APPDATA%\PomodoroClock\config.json
```

如果窗口位置、透明度或显示模式被误设置，导致界面不可见或难以操作，可以关闭程序后删除该配置文件。下次启动时程序会自动生成默认配置。

## 常见问题

### 双击 exe 没反应或提示缺少 DLL

请确认 `PomodoroClock.exe` 和 `_internal/` 在同一个目录下，并且 `_internal/` 没有被删除、改名或移动。

### 运行时报错 `No module named PySide6.QtCore`

这通常说明下载的不是完整发布包，或者只移动了 `PomodoroClock.exe`。

请重新前往 **Releases** 页面下载 `PomodoroClock.zip`，完整解压后运行。不要下载 GitHub 自动生成的 `Source code (zip)` 来运行程序。

### 运行时报错 `No module named shiboken6.Shiboken`

原因同上。`shiboken6` 是 PySide6 的运行依赖，必须包含在 `_internal/` 目录中。请重新下载 Releases 中的完整 `PomodoroClock.zip`。

### Windows 安全提示未知发布者

这是因为该程序没有代码签名证书。可以选择“更多信息”后继续运行。请只运行来自可信来源的压缩包。

### 程序窗口显示异常或无法找到

关闭程序后删除配置文件：

```text
%APPDATA%\PomodoroClock\config.json
```

然后重新启动程序。程序会自动恢复默认窗口大小、位置和显示配置。

### 透明度修改没有效果

透明度作用于卡片背景，不会让文字和按钮整体变透明。修改后请在设置窗口点击“应用”或“确定”。

## 给普通用户的下载说明

如果你只是想使用这个程序，请按以下步骤操作：

1. 打开本项目的 Releases 页面。
2. 下载最新版本中的 `PomodoroClock.zip`。
3. 解压整个压缩包。
4. 双击 `PomodoroClock.exe`。
5. 不要单独移动 `PomodoroClock.exe`，也不要删除 `_internal/` 文件夹。

## 给开发者的说明

当前仓库主要用于发布 Windows 打包版本，不是完整源码开发仓库。

PyInstaller `onedir` 版本依赖目录较多，因此不建议把 `_internal/` 展开上传到 GitHub 主分支。推荐做法是：

- 仓库主页保留 `README.md`。
- 完整运行包以 `PomodoroClock.zip` 的形式上传到 GitHub Releases。
- 用户从 Releases 下载完整压缩包运行。

如果需要继续开发、修改源码或重新打包，请使用源码版本项目，而不是仅包含 `PomodoroClock.exe` 和 `_internal/` 的发布目录。

## 版本说明

这是 Windows PyInstaller `onedir` 打包版本。相较单文件 exe，`onedir` 目录体积较大，但启动更稳定，也更适合 PySide6 / Qt 桌面程序。
