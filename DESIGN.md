# 俄罗斯方块游戏界面改造设计方案

## 一、方案要求

### 1. 整体外观
- 掌机造型：圆角矩形外壳，深色渐变背景
- 屏幕区域：位于上方，带有内阴影效果
- 控制区域：位于下方，分为左右两部分

### 2. 开始界面
- 标题：TETRIS（大字体，蓝色）
- 副标题：TETRIS BLITZ
- 按钮：
  - "开始游戏" 绿色按钮
  - "玩法说明" 灰色按钮
- 排行榜链接
- 底部：作者信息（Gerry | v1.1.1）

### 3. 游戏过程中界面
- 标题：TETRIS（蓝色小字在最上方）
- 左侧：游戏棋盘（10x20格子，方块下落中）
- 右侧信息栏：
  - SCORE: 0（分数显示）
  - LEVEL: 1（等级显示）
  - NEXT: 下一个方块预览

### 4. 控制区域
- 左侧：十字方向键（D-Pad）
  - 上下左右四个方向按钮
  - 中间有凹陷圆形作为基准点
- 右侧：功能按钮
  - 上方：两个旋转按钮（↺ 逆时针 / ↻ 顺时针）
  - 下方：两个圆形按钮
    - A 按钮：快速落底
    - B 按钮：暂停/继续
  - 右侧最下方：M 按钮（音乐开关）

### 5. 配色风格
- 主色调：GitHub 风格深色（#1a1a2e, #0d1117）
- 主题色：蓝色（#58a6ff）
- 按钮：渐变色，带有立体感阴影

---

## 二、最终实现

### 1. HTML 结构

```html
<div class="console">
    <!-- 屏幕区域 -->
    <div class="screen-area">
        <!-- 开始界面 -->
        <div class="start-screen" id="startScreen">
            <!-- 标题、按钮、排行榜链接 -->
        </div>

        <!-- 游戏界面 -->
        <div class="game-screen" id="gameScreen">
            <!-- 标题、游戏棋盘、信息栏 -->
        </div>
    </div>

    <!-- 控制区域 -->
    <div class="controls-area">
        <!-- 左侧十字方向键 -->
        <div class="dpad">
            <div class="dpad-center"></div>
            <button class="dpad-btn dpad-up" onclick="movePiece('up')"></button>
            <button class="dpad-btn dpad-down" onclick="movePiece('down')"></button>
            <button class="dpad-btn dpad-left" onclick="movePiece('left')"></button>
            <button class="dpad-btn dpad-right" onclick="movePiece('right')"></button>
        </div>

        <!-- 右侧功能按钮 -->
        <div class="function-btns">
            <div class="rotate-btns">
                <button class="btn-rotate" onclick="rotatePiece('ccw')">↺</button>
                <button class="btn-rotate" onclick="rotatePiece('cw')">↻</button>
            </div>
            <div class="action-btns">
                <button class="btn-action btn-a" onclick="hardDrop()">A</button>
                <button class="btn-action btn-b" onclick="togglePause()">B</button>
            </div>
            <div class="music-btn">
                <button class="btn-rotate playing" id="musicBtn" onclick="toggleMusic()">M</button>
            </div>
        </div>
    </div>

    <!-- 背景音乐 -->
    <audio id="bgMusic" loop preload="auto">
        <source src="audio/tetris.mp3" type="audio/mpeg">
    </audio>
</div>
```

### 2. CSS 样式
- 掌机外壳：深色渐变 + 圆角 + 阴影效果
- 屏幕区域：内阴影 + 圆角边框
- 虚拟按钮：渐变色背景 + 立体阴影 + 触摸优化
- 响应式适配：移动端自动缩放（scale 0.85 → 0.65）

### 3. 功能实现
- 十字方向键：控制方块移动（←→左右移动，↓↑加速下落）
- 旋转按钮：逆时针/顺时针旋转
- A 按钮：快速落底（每格+2分）
- B 按钮：暂停/继续（点击屏幕也可恢复）
- M 按钮：音乐开关（默认开启，绿色表示播放中）
- 排行榜功能：游戏结束后自动保存成绩

### 4. 音乐系统
- 使用 Web Audio API 播放背景音乐
- 点击"开始游戏"后自动初始化音频并播放
- 暂停时音乐暂停
- 游戏结束时音乐停止

### 5. 音效系统
使用 Web Audio API 程序化生成 5 种音效：

| 音效函数 | 触发时机 | 音色特点 |
|----------|----------|----------|
| `playMoveSound()` | 左右移动方块 | 220Hz 正弦波，短促 50ms |
| `playRotateSound()` | 旋转方块 | 440→550Hz 正弦波，上升音 100ms |
| `playDropSound()` | 方块触底锁定 | 150→80Hz 方波，低沉 100ms |
| `playClearSound()` | 消除一行或多行 | 523→1047Hz 方波，四音符旋律 400ms |
| `playGameOverSound()` | 游戏结束 | 400→100Hz 锯齿波，下降音 500ms |

### 6. 排行榜页面 (leaderboard.html)
- 统计面板：总游戏次数、最高分数、最佳用时
- 排行榜表格：显示前10名
- 前三名显示🥇🥈🥉奖牌
- 支持清空排行榜功能

---

## 三、验证清单

- [x] 点击"开始游戏"按钮能正常开始游戏
- [x] 方块能正常自动下落
- [x] 虚拟方向键能控制方块移动
- [x] 虚拟旋转按钮能旋转方块
- [x] 虚拟 A 按钮能快速落底
- [x] 虚拟 B 按钮能暂停/继续
- [x] 点击暂停遮罩能恢复游戏
- [x] M 按钮能开关音乐
- [x] 排行榜能正常记录成绩
- [x] 排行榜页面显示统计信息
- [x] 移动端适配正常（自动缩放）
- [x] 键盘控制仍然有效
- [x] 内置帮助弹窗能正常显示

---

## 四、技术实现要点

### 游戏循环
- 使用 `setInterval` 实现 1000ms 基础下落间隔
- 等级提升后速度加快：`Math.max(100, 1000 - (level - 1) * 100)`
- 暂停时清除 interval，恢复时重新设置

### 音效系统
使用 Web Audio API 的 `OscillatorNode` 和 `GainNode` 程序化生成音效：

```javascript
function playRotateSound() {
    const osc = audioCtx.createOscillator();
    const gain = audioCtx.createGain();
    osc.type = 'sine';
    osc.connect(gain);
    gain.connect(audioCtx.destination);
    osc.frequency.setValueAtTime(440, audioCtx.currentTime);
    osc.frequency.setValueAtTime(550, audioCtx.currentTime + 0.05);
    gain.gain.setValueAtTime(0.15, audioCtx.currentTime);
    gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.1);
    osc.start(audioCtx.currentTime);
    osc.stop(audioCtx.currentTime + 0.1);
}
```

### 方块系统
- 7 种标准方块形状（I、O、T、S、Z、J、L）
- 旋转使用矩阵转置算法
- 碰撞检测：边界检查 + 棋盘占用检查

### 计分系统
- 单行：100 × 等级
- 双行：300 × 等级
- 三行：500 × 等级
- 四行：800 × 等级
- 硬降：每格 2 分

### 数据存储
- localStorage 存储排行榜数据
- 键名：`tetris_leaderboard`
- 格式：`[{score, time, date}, ...]`
- 排序后取前10名
