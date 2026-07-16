 <div align="center">
   <h1>👾 外星人入侵 / Alien Invasion</h1>
   <p><em>基于 Python 和 Pygame 的经典横版太空射击游戏</em><br>
   <em>A classic side-scrolling space shooter built with Python and Pygame</em></p>
 </div>
 
 <p align="center">
   <a href="#chinese">🇨🇳 中文</a> ·
   <a href="#english">🇺🇸 English</a>
 </p>
 
 ---
 
 <a id="chinese"></a>
 # 🇨🇳 中文
 
 ## 📖 简介
 
 **外星人入侵** 是一款 2D 太空射击游戏，源自 Eric Matthes 的《Python 编程：从入门到实践》（Python Crash Course）。玩家控制屏幕底部的飞船，向一波波下落的 aliens（外星人）开火。每清除一波外星人，游戏难度都会提升——外星人移动更快，得分倍率更高。
 
 ## ✨ 功能特性
 
 - **渐进式难度** — 每波外星人清除后，速度和射速都会提升
 - **得分系统** — 实时分数显示、最高分记录（内存中）和关卡进度
 - **生命系统** — 每局 3 艘飞船；被击中后外星人群重置
 - **键盘与鼠标控制** — 方向键移动，空格键开火，鼠标点击开始
 - **干净的模块化代码** — 设置、统计、HUD、游戏对象等均有独立类，便于扩展
 
 ## 🎮 如何游玩
 
 ### 操作方式
 
 | 按键 / 操作          | 功能                     |
 |----------------------|--------------------------|
 | `←` / `→` 方向键     | 向左 / 向右移动飞船      |
 | `Space` 空格键        | 发射子弹                 |
 | `Q`                  | 退出游戏                 |
 | 鼠标点击「Play」按钮  | 开始 / 重新开始游戏      |
 
 ### 游戏规则
 
 1. 击落当前波次的所有外星人即可进入下一关。
 2. 每升一级，外星人和子弹速度都会加快。
 3. 你拥有 **3 艘飞船**。外星人撞到飞船或抵达屏幕底部会损失一艘。
 4. 所有飞船耗尽后游戏结束，点击 **Play** 重新开始。
 5. **最高分** 在本次游戏会话期间持续保留。
 
 ## 📦 环境要求
 
 - **Python** >= 3.6
 - **Pygame** >= 2.0
 
 ## 🚀 安装与运行
 
 ```bash
 # 1. 克隆或下载仓库
 git clone <仓库地址>
 cd alien-invasion-master
 
 # 2. 安装 Pygame（尚未安装时）
 pip install pygame
 
 # 3. 运行游戏
 python alien-invasion.py
 ```
 
 ## 📁 项目结构
 
 ```
 alien-invasion-master/
 ├── alien-invasion.py      # 主入口 — 初始化游戏并运行主循环
 ├── README.md              # 本文件
 ├── src/                   # 源代码目录
 │   ├── __init__.py        # 包初始化
 │   ├── settings.py        # 游戏设置（屏幕、速度、缩放等）
 │   ├── game_stats.py      # 游戏统计数据（分数、关卡、生命值、最高分）
 │   ├── ship.py            # 玩家飞船 — 移动、绘制、居中
 │   ├── alien.py           # 外星人精灵 — 移动、边缘检测
 │   ├── bullet.py          # 子弹精灵 — 创建、移动、绘制
 │   ├── button.py          # 开始按钮 UI
 │   ├── game_functions.py  # 核心游戏逻辑 — 事件处理、碰撞检测、舰队管理
 │   └── scoreboard.py      # HUD 渲染 — 分数、关卡、剩余飞船
 └── images/
     ├── ship.bmp           # 飞船图像
     └── alien.bmp          # 外星人图像
 ```
 
 ## ⚙️ 自定义设置
 
 编辑 **`src/settings.py`** 即可调整游戏参数：
 
 | 设置项                       | 默认值   | 说明                          |
 |------------------------------|---------|-------------------------------|
 | `screen_width`               | 1200    | 窗口宽度（像素）               |
 | `screen_height`              | 800     | 窗口高度（像素）               |
 | `bg_color`                   | (230, 230, 230) | 背景颜色（RGB）         |
 | `ship_speed_factor`          | 1       | 飞船基础移动速度               |
 | `bullet_speed_factor`        | 2.5     | 子弹基础速度                   |
 | `bullet_width` / `bullet_height` | 3 / 15 | 子弹尺寸                    |
 | `bullets_allowed`            | 3       | 同时出现在屏幕上的最大子弹数    |
 | `alien_speed_factor`         | 0.4     | 外星人基础水平移动速度          |
 | `fleet_drop_speed`           | 5       | 外星人撞到边缘时的垂直下降距离  |
 | `ship_limit`                 | 3       | 每局游戏的飞船数量             |
 | `speedup_scale`              | 1.1     | 每关速度倍率（×1.1）           |
 | `score_scale`                | 1.5     | 每关得分倍率（×1.5）           |
 
 ## 🧠 技术要点
 
 - **基于精灵的渲染** — 所有游戏对象（飞船、外星人、子弹）均继承自 `pygame.sprite.Sprite`，利用 Pygame 内置的碰撞检测（`groupcollide`、`spritecollideany`）
 - **无状态事件循环** — `check_event` 将输入处理与游戏逻辑解耦；`update_screen` 将渲染与状态更新分离
 - **动态难度系统** — `Settings.initialize_dynamic_settings()` 管理随时间变化的参数，每局游戏重置
 - **舰队自动排布** — 外星人数量根据屏幕宽度和高度动态计算，非硬编码
 - **游戏状态机** — `GameStats.game_active` 标志控制是否更新游戏逻辑，Play 按钮提供干净的重新开始路径
 
 ## 📄 许可协议
 
 本项目仅供学习交流使用，欢迎自由修改和分享。
 
 ---
 
 <a id="english"></a>
 # 🇺🇸 English
 
 ## 📖 Overview
 
 **Alien Invasion** is a 2D space shooter game originally from the book *Python Crash Course* by Eric Matthes. You control a spaceship at the bottom of the screen, firing bullets at waves of descending aliens. The game gets progressively harder as you clear each wave — aliens move faster, and your score multiplier increases.
 
 ## ✨ Features
 
 - **Progressive difficulty** — each cleared wave increases alien speed and bullet fire rate
 - **Score system** — real-time score display, high-score tracking (in-memory), and level progression
 - **Lives system** — 3 ships per game; the fleet resets after each hit
 - **Keyboard & mouse controls** — arrow keys to move, Space to fire, mouse click to start
 - **Clean, extensible codebase** — modular design with separate classes for settings, stats, HUD, and game objects
 
 ## 🎮 How to Play
 
 ### Controls
 
 | Key / Action        | Function                   |
 |---------------------|----------------------------|
 | `←` / `→` Arrow     | Move ship left / right     |
 | `Space`             | Fire a bullet              |
 | `Q`                 | Quit the game              |
 | Mouse click on Play  | Start / restart the game   |
 
 ### Rules
 
 1. Shoot all aliens in a wave to advance to the next level.
 2. Each level increases alien speed and bullet speed.
 3. You start with **3 ships**. One ship is lost when an alien collides with your ship or reaches the bottom.
 4. When all ships are lost, the game ends. Click **Play** to restart.
 5. Your **high score** is preserved during the session.
 
 ## 📦 Requirements
 
 - **Python** >= 3.6
 - **Pygame** >= 2.0
 
 ## 🚀 Installation & Running
 
 ```bash
 # 1. Clone or download the repository
 git clone <repo-url>
 cd alien-invasion-master
 
 # 2. Install Pygame (if not already installed)
 pip install pygame
 
 # 3. Run the game
 python alien-invasion.py
 ```
 
 ## 📁 Project Structure
 
 ```
 alien-invasion-master/
 ├── alien-invasion.py      # Main entry point — initializes game and runs the main loop
 ├── README.md              # This file
 ├── src/                   # Source code directory
 │   ├── __init__.py        # Package initializer
 │   ├── settings.py        # Game settings (screen, speed, scaling, etc.)
 │   ├── game_stats.py      # Game statistics (score, level, lives, high score)
 │   ├── ship.py            # Player ship — movement, rendering, centering
 │   ├── alien.py           # Alien sprite — movement, edge detection
 │   ├── bullet.py          # Bullet sprite — creation, movement, rendering
 │   ├── button.py          # Play button UI
 │   ├── game_functions.py  # Core game logic — events, collisions, fleet management
 │   └── scoreboard.py      # HUD rendering — score, level, lives
 └── images/
     ├── ship.bmp           # Ship sprite
     └── alien.bmp          # Alien sprite
 ```
 
 ## ⚙️ Customization
 
 You can tune the game by editing **`src/settings.py`**:
 
 | Setting                 | Default | Description                          |
 |-------------------------|---------|--------------------------------------|
 | `screen_width`          | 1200    | Window width (pixels)                |
 | `screen_height`         | 800     | Window height (pixels)               |
 | `bg_color`              | (230, 230, 230) | Background color (RGB)         |
 | `ship_speed_factor`     | 1       | Base ship movement speed             |
 | `bullet_speed_factor`   | 2.5     | Base bullet speed                    |
 | `bullet_width` / `bullet_height` | 3 / 15 | Bullet size                 |
 | `bullets_allowed`       | 3       | Max bullets on screen at once        |
 | `alien_speed_factor`    | 0.4     | Base alien horizontal speed          |
 | `fleet_drop_speed`      | 5       | Vertical drop when aliens hit an edge |
 | `ship_limit`            | 3       | Number of ships per game             |
 | `speedup_scale`         | 1.1     | Speed multiplier per level (×1.1)    |
 | `score_scale`           | 1.5     | Score multiplier per level (×1.5)    |
 
 ## 🧠 Technical Highlights
 
 - **Sprite-based rendering** — all game objects (ship, aliens, bullets) are `pygame.sprite.Sprite` subclasses, leveraging built-in collision detection (`groupcollide`, `spritecollideany`)
 - **Stateless event loop** — `check_event` decouples input handling from game logic; `update_screen` separates rendering from state updates
 - **Dynamic difficulty** — `Settings.initialize_dynamic_settings()` vs static defaults, reset on each new game
 - **Fleet formation** — alien count is computed dynamically based on screen width/height, not hardcoded
 - **Game state machine** — `GameStats.game_active` flag controls whether updates are processed, with a clean Play-button restart path
 
 ## 📚 Credits
 
 Originally inspired by **Alien Invasion** from *Python Crash Course* (3rd Edition) by Eric Matthes.
 
 ## 📄 License
 
 This project is for educational purposes. You are free to modify and share it.
