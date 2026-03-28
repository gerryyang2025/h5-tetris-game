# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [1.1.1] - 2026-03-29

### Fixed

- 修复 `togglePause` 函数重复定义问题（JavaScript 中后定义的版本覆盖先定义的版本）
- 修复 `startGame` 函数重复定义问题
- 修复 `gameOver` 函数重复定义问题
- 确保暂停/音乐状态在游戏恢复时正确同步

### Changed

- 简化代码结构，移除冗余函数定义

---

## [1.1.0] - 2026-03-28

### Added

- **掌机风格界面**：圆角矩形外壳，深色渐变背景
- **屏幕区域**：位于上方，带有内阴影效果
- **虚拟十字方向键**：上下左右四个方向按钮，中间有凹陷圆形基准点
- **虚拟功能按钮**：
  - 旋转按钮（↺ 逆时针 / ↻ 顺时针）
  - A 按钮：快速落底
  - B 按钮：暂停/继续
  - M 按钮：音乐开关（默认开启）
- **暂停遮罩点击恢复**：点击暂停界面可继续游戏
- **移动端适配**：固定掌机大小，自动缩放适配不同屏幕
- **触摸优化**：添加 touch-action 和 -webkit-tap-highlight-color
- **内置帮助弹窗**：开始界面有玩法说明按钮，无需跳转页面

### Changed

- **音乐播放**：改用 Web Audio API，点击开始游戏后自动播放
- **方向键尺寸**：30px → 40px，提升触屏操作体验
- **配色保持**：GitHub 风格深色主题不变
- **排行榜页面**：新增统计面板（总游戏次数、最高分数、最佳用时）
- **排行榜页面**：前三名显示🥇🥈🥉奖牌

### Fixed

- 开始游戏后不再显示暂停状态
- 暂停后可以点击屏幕恢复游戏
- 音乐开关按钮状态和实际播放状态一致
- 排行榜链接正确跳转到 leaderboard.html

---

## [1.0.0] - 2026-03-28

### Added

- 7 standard tetrominoes (I, O, T, S, Z, J, L) with neon colors
- Keyboard controls (arrow keys, WASD, Space, P)
- Touch controls with swipe gestures
- Ghost piece showing drop position
- Next piece preview
- Scoring system with level multiplier
- Level progression (speed increases every 10 lines cleared)
- Particle effects on line clear
- Sound effects via Web Audio API (rotate, move, drop, hard drop, line clear)
- Background music (tetris.mp3)
- Game timer
- Leaderboard with localStorage (Top 10)
- Game rank display after game over
- Pause / resume functionality
- Responsive design for mobile and desktop
- Neon dark theme (GitHub-style)

### Pages

- `index.html` — main game
- `leaderboard.html` — ranking display
- `help.html` — how to play guide
