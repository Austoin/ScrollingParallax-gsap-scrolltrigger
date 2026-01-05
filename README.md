# Scrolling Parallax Effect - GSAP & ScrollTrigger 教程

一个使用 GSAP 和 ScrollTrigger 实现的滚动视差效果网页项目。

## 演示视频

<video src="0.mp4" controls width="600"></video>

## 项目结构

```
ScrollingParallax-gsap-scrolltrigger/
├── index.html              # 主页面
├── 0.mp4                   # 演示视频
├── img/                    # 图片资源
│   ├── 1.jpg ~ 8.jpg       # 展示图片
│   ├── arrow.svg           # 箭头图标
│   └── star.svg            # 星星图标
├── js/
│   ├── js.js               # 主要动画逻辑
│   ├── luxy.js             # 平滑滚动库
│   └── splitting.min.js    # 文字分割库
└── style/
    ├── style.css           # 主样式
    └── normalize.css       # CSS重置
```

## 技术栈

- **GSAP 3.11.4** - 动画引擎
- **ScrollTrigger** - GSAP 滚动触发插件
- **Luxy.js** - 平滑滚动效果
- **Splitting.js** - 文字分割动画

## 核心概念

### 1. 初始化

```javascript
Splitting();           // 将文字拆分为单个字符
luxy.init();           // 启用平滑滚动
gsap.registerPlugin(ScrollTrigger);  // 注册滚动触发器
```

### 2. 入场动画

```javascript
const gTl = gsap.timeline();
gTl.from(".title .char", 1, { 
    opacity: 0, 
    yPercent: 130, 
    stagger: 0.06,      // 每个字符延迟0.06秒
    ease: "back.out" 
});
```

### 3. ScrollTrigger 基本用法

```javascript
gsap.to('.element', {
    scrollTrigger: {
        trigger: '.trigger-element',  // 触发元素
        start: 'top top',             // 开始位置
        scrub: 1.9                    // 平滑跟随滚动
    },
    yPercent: -150                    // 动画属性
});
```

### 4. data-speed 属性实现差速滚动

HTML 中设置速度值：
```html
<span class="benefits__num" data-speed="-200">/01</span>
```

JS 中读取并应用：
```javascript
gsap.from('.benefits__num', {
    x: (i, el) => (1 - parseFloat(el.getAttribute('data-speed'))),
    scrollTrigger: {
        trigger: '.benefits__list',
        start: 'top bottom',
        scrub: 1.9
    }
});
```

## 页面区块动画

| 区块 | 效果 |
|------|------|
| Header | 标题上移、图片左移+缩放、跑马灯横移、星星旋转 |
| About | 图片视差上移、文字下移 |
| Benefits | 数字差速横移 |
| Portfolio | 卡片差速纵移、图片缩放 |
| Services | 箭头差速横移 |
| Footer | 字母差速纵移+淡入 |

## 关键 CSS 技巧

### clip-path 裁剪动画

```css
.header__img {
    clip-path: polygon(0% 0%, 0% 0%, 0% 100%, 0% 100%);  /* 初始隐藏 */
}
```

```javascript
gTl.to(".header__img", 2, { 
    clipPath: "polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)",  /* 展开 */
    scale: 1 
});
```

### 描边文字

```css
.stroke {
    color: transparent;
    -webkit-text-stroke: 1px #fff;
}
```

### 混合模式

```css
.title {
    mix-blend-mode: difference;  /* 与背景色差混合 */
}
```

## 快速开始

1. 克隆项目
2. 用浏览器打开 `index.html`

无需构建工具，直接运行。

## 依赖 CDN

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.4/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.4/ScrollTrigger.min.js"></script>
```

## License

MIT