# MP3_OnlineMusicPlayerSearch (Qt在线MP3音乐播放器搜索引擎)

[![Qt](https://img.shields.io/badge/Qt-5.x-green.svg)](https://www.qt.io/)
[![Language](https://img.shields.io/badge/Language-C++11-blue.svg)](https://en.cppreference.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

这是一个基于 **C++** 和 **Qt Widgets** 开发的轻量级桌面在线音乐播放器。

项目集成了**HTTP 网络通信**、**JSON 数据解析**、**SQLite 数据库存储**以及**多媒体播放**功能，实现了从云端搜索音乐到本地播放的全流程，并具备自定义 UI 换肤与系统托盘管理等桌面应用特性。

## 📸 项目预览
因为API原因，歌词显示没有完成
<img width="846" height="647" alt="image" src="https://github.com/user-attachments/assets/d64036c1-4822-4036-af13-f8896eb4a11e" />



## ✨ 核心功能

* **🔍 在线音乐搜索**：通过 HTTP 请求对接第三方音乐搜索接口，支持关键字模糊搜索，实时解析 JSON 数据并显示结果列表。
* **🎵 流媒体播放**：支持在线音乐的实时流式播放，包含播放/暂停、上一曲/下一曲、进度拖拽及音量调节功能。
* **🔂 播放模式控制**：支持单曲循环/列表循环模式切换，自动监听媒体状态进行逻辑跳转。
* **💾 本地数据持久化**：
    * **历史记录**：自动将播放过的歌曲信息存储至本地 SQLite 数据库 (`mp3listdatabase.db`)，软件重启后数据不丢失。
    * **搜索缓存**：使用数据库暂存搜索结果，减少内存占用并优化数据管理。
* **🎨 UI 个性化与交互**：
    * **无边框窗口**：自定义窗口标题栏，重写鼠标事件 (`mouseMoveEvent`) 实现窗口拖拽移动。
    * **动态换肤**：支持切换默认背景或加载本地图片作为皮肤，自动进行平滑缩放适配。
* **💻 系统集成**：支持最小化到系统托盘，提供托盘右键菜单（退出/显示）及双击还原功能。

## 🛠 技术栈

| 模块 | 技术点 | 用途 |
| :--- | :--- | :--- |
| **Language** | C++11 | 核心开发语言 |
| **GUI Framework** | Qt Widgets (Qt5/Qt6) | 界面开发、信号与槽机制、事件循环 |
| **Network** | QNetworkAccessManager | 处理 HTTP GET 请求，模拟 User-Agent |
| **Data Format** | QJsonDocument / QJsonObject | 解析服务端返回的复杂 JSON 数据 |
| **Database** | QSqlDatabase (SQLite) | 存储播放历史 (`historysong`) 和搜索列表 (`searchlist`) |
| **Multimedia** | QMediaPlayer / QMediaPlaylist | 音频解码与播放控制 |
| **Utils** | QSettings / QSystemTrayIcon | 系统配置与桌面集成 |

## 🚀 快速开始

### 1. 环境依赖
* **Qt 版本**：建议 Qt 5.12 或更高版本 (支持 Qt6)。
* **编译器**：MSVC 2017+ 或 MinGW 64-bit。
* **多媒体解码器**：
    * **Windows**: 需要安装系统的 DirectShow 解码器（推荐安装 [LAV Filters](https://github.com/Nevcairiel/LAVFilters) 以确保能播放 MP3/MP4 流）。
    * **Linux**: 需要安装 `gstreamer` 相关插件 (`libgstreamer-plugins-base`, `good`, `bad`, `ugly`)。

### 2. 构建步骤

**使用 Qt Creator:**
1.  打开 `MusicPlayer.pro`。
2.  配置项目构建套件 (Kit)。
3.  点击 **运行 (Run)** 或按 `Ctrl+R`。


### 3. 项目结构说明

├── main.cpp                # 程序入口                    
├── mainwidget.h/.cpp       # 主窗口逻辑 (网络请求、数据库操作、播放控制)                           
├── mainwidget.ui           # 界面布局文件                              
├── mp3listdatabase.db      # SQLite 数据库文件                                  
└── resources/              # 图标与默认皮肤资源       




⚠️ 注意事项
API 说明：本项目中使用的音乐搜索与播放API仅供学习与研究网络编程使用，接口可能随时变动，不保证长期有效。
HTTPS 支持：代码中已包含将 HTTP 链接转换为 HTTPS 的逻辑，以适应现代网络安全策略。
SSL 库：如果是 Windows 环境下运行，可能需要将 OpenSSL 的动态库 (libcrypto-1_1.dll, libssl-1_1.dll) 复制到可执行文件同级目录下，以支持 HTTPS 请求。
