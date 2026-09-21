

<p align="center">
  <img src="https://img.shields.io/badge/FramelabWorks-3ecf8e?style=for-the-badge&labelColor=0c0d11" alt="FramelabWorks">
  <img src="https://img.shields.io/badge/-%E7%BA%AF%E6%9C%AC%E5%9C%B0%E7%A6%BB%E7%BA%BF-3ecf8e?style=for-the-badge&labelColor=0c0d11" alt="纯本">
  <img src="https://img.shields.io/badge/-%E5%8D%95%E6%96%87%E4%BB%B6-3ecf8e?style=for-the-badge&labelColor=0c0d11" alt="单文件">
  <img src="https://img.shields.io/badge/-%E4%B8%8D%E4%B8%8A%E4%BC%A0-3ecf8e?style=for-the-badge&labelColor=0c0d11" alt="不上传">
  <br>
  <img src="https://img.shields.io/github/license/Lyajjyurot/FramelabWorks?style=flat-square&labelColor=15171f&color=8b93a3" alt="License">
</p>

<br>

<p align="center">
  <b>把一段视频变成一帧帧透明精灵图 —— 全程本地，开箱即用，一个浏览器搞定。</b>
</p>

<br>

<p align="center">
  <i>导入视频 → 裁时间 → 抽帧 → 选帧 → 框裁 → 抠图 → 导出</i>
</p>

<br>

---
<img width="376" height="140" alt="logo" src="https://github.com/user-attachments/assets/e75eaf16-2d32-4b83-8d82-11b48584935c" />

## 为什么做这个

做游戏、做动效、做表情包的时候，经常需要把一段视频拆成带透明背景的逐帧图片。

现有的方案要么要装软件、要么要上传到服务器、要么导出格式不满意。

**FramelabWorks** 就是为了解决这个问题：

> 打开一个 HTML 文件，拖入视频，点几下，就能拿到透明 GIF 、WebP或 PSD 分层文件。
>
> **你的视频永远不会离开你的电脑。**

---

## 一览

| 步骤 | 做什么 | 细节 |
|:---:|--------|------|
| **①** | 时间裁剪 | 精确到毫秒，一键定位当前播放位置 |
| **②** | 间隔抽帧 | 每 N 帧抽 1 帧，可选 ffmpeg.wasm 精确模式 |
| **③** | 帧筛选 | 缩略图网格，全选 / 反选 / 单帧点选 |
| **④** | 画布框裁 | 拖拽画框 + 八把手缩放 + 九宫格辅助线 |
| **⑤** | 批量抠图 | YCbCr 色差抠图，吸管取色 + 橡皮擦手动微调 |
| **⑥** | 导出 | 透明 GIF（可压缩至 ≤1MB / 256KB / 128KB）· ZIP（PSD 分层 + 每帧 PNG）· WebP（可压缩至 ≤1MB / 256KB / 128KB） |


---


## 演示

- 时间裁剪
<img width="1056" height="538" alt="1" src="https://github.com/user-attachments/assets/034e282a-1fc5-4842-80e2-38695a3fd4ed" />

- 间隔抽帧
<img width="651" height="292" alt="间隔" src="https://github.com/user-attachments/assets/793325aa-f500-4c97-897f-e5b0c67e7061" />


- 帧筛选
<img width="1052" height="597" alt="2" src="https://github.com/user-attachments/assets/d0e2c5fa-9566-4bac-bc49-d12d53a213f7" />


- 画布裁切
<img width="997" height="568" alt="裁切" src="https://github.com/user-attachments/assets/c3d49430-fb9f-488a-a363-7c8ee11f230d" />

- 批量抠图
<img width="1012" height="541" alt="抠像" src="https://github.com/user-attachments/assets/ad147b3f-89cb-4ce5-9721-73c54f4d6eda" />

- 导出【未抠像仅示范】
<img width="958" height="488" alt="123" src="https://github.com/user-attachments/assets/27cf89c9-f875-422d-b271-0c6db75914d4" />



## 亮点

- 100% 本地离线 — 所有处理在浏览器内存中完成，视频不上传、不留痕
- 支持至多10个文件导入 — 一次性批量导入素材，浏览器中直接选择操作
- 画布裁剪 -便于去除不必要的水印
- 单文件即用 — 一个 `.html` 文件，双击打开，零安装零配置
- 全流程覆盖 — 从导入到导出，六个步骤一气呵成
- 专业抠图 — YCbCr 色度差算法 + 抗锯齿羽化 + 去白边溢色，效果不输专业工具
- 双格式导出 — 透明 GIF 直接用，PSD 分层进 PS 继续编辑
- 零依赖 — 纯原生 HTML / CSS / JS，不依赖任何框架和构建工具

---

## 快速开始

```bash
# 无需安装，直接用浏览器打开
# 双击文件
FramelabWorks.html

```

推荐 **Chrome / Edge** 等现代浏览器。

---

## 抠图算法说明

### 色差抠图（默认）

基于 **YCbCr 色度空间**计算像素与背景色的距离，而非简单的 RGB 混合距离。

- 对白/灰/绿幕/蓝幕背景均有效
- 自动识别背景主通道，智能保护主体彩色边缘
- 容差滑块实时调节，所见即所得

---

## 技术实现

```
FramelabWorks.html
├── 视频解码：浏览器原生 <video> + canvas 截帧
├── 可选增强：ffmpeg.wasm（按需从 CDN 加载）
├── 抠图引擎：YCbCr 色度差（吸管取色 + 橡皮擦微调）
├── GIF 编码：纯 JS LZW 编码器
├── PSD 写入：自实现 PSD 二进制格式
└── ZIP 打包：自实现 ZIP + deflate
```

全部逻辑在一个文件内，可离线使用。

---

## 局限

- GIF 格式最大 256 色，复杂渐变画面会有色阶
- 超长视频（>10 分钟全帧率）可能占用较多内存，建议先裁剪时间区间
- 部分浏览器（Safari）对 `requestVideoFrameCallback` 支持不完整，帧率检测可能回退到默认值

---

## 贡献

欢迎提交 Issue 和 Pull Request。



---

## 许可证

[MIT License]
