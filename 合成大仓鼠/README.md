# 合成大仓鼠 🐹

一个类似「合成大西瓜」的休闲小游戏。

## 玩法

1. 点击/触摸屏幕投放仓鼠宝宝
2. 两个相同的仓鼠碰撞会合成更大的仓鼠
3. 合成到黄金仓鼠即为胜利！
4. 如果仓鼠堆得太高超过警戒线，游戏结束

## 合成路线

| 等级 | 动物 | 分值 |
|------|------|------|
| 1 | 🐹 仓鼠宝宝 | 1 |
| 2 | 🐹 小仓鼠 | 2 |
| 3 | 🐹 圆仓鼠 | 4 |
| 4 | 🐹 肥仓鼠 | 8 |
| 5 | 🐹 大仓鼠 | 16 |
| 6 | 🐹 巨型仓鼠 | 32 |
| 7 | ⭐ 黄金仓鼠 | 64 |

## 本地运行

直接用浏览器打开 index.html 即可。

或者用本地服务器：
`ash
# Python
python -m http.server 8000

# Node.js
npx serve .
`

然后访问 http://localhost:8000

## 适配微信小游戏

### 步骤

1. **下载微信开发者工具**
   - https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html

2. **创建小游戏项目**
   - 选择「小游戏」项目类型
   - AppID 在微信公众平台注册获取

3. **文件结构调整**
   `
   你的项目/
   ├── game.js          # 入口文件（小游戏需要）
   ├── game.json        # 项目配置
   ├── project.config.json
   ├── js/
   │   ├── main.js      # 主游戏逻辑
   │   ├── physics.js   # 物理引擎
   │   └── renderer.js  # 渲染器
   └── assets/
       └── sounds/      # 音效文件
   `

4. **关键修改**
   - 将 document.getElementById 改为 canvas
   - 使用 wx.createCanvas() 获取画布
   - 事件监听改用 wx.onTouchStart 等接口
   - 音效使用 wx.createInnerAudioContext()
   - 分享使用 wx.onShareAppMessage()

5. **game.json 配置**
   `json
   {
     "deviceOrientation": "portrait",
     "showStatusBar": false,
     "networkTimeout": {
       "request": 5000,
       "connectSocket": 5000,
       "uploadFile": 5000,
       "downloadFile": 5000
     }
   }
   `

6. **打包优化**
   - 首包大小控制在 4MB 以内
   - 使用分包加载
   - 图片压缩（WebP 格式）
   - 代码混淆压缩

### 注意事项

- 微信小游戏不支持 DOM 操作
- 网络请求需要使用 wx.request
- 存储使用 wx.setStorageSync / wx.getStorageSync
- 广告接入使用 wx.createRewardedVideoAd

## 技术栈

- 纯 HTML5 Canvas + JavaScript
- 零依赖
- 兼容桌面和移动端

## 许可证

MIT License
