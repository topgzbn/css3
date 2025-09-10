# 1.变换
transform：2D/3D变换的核心属性，支持平移，旋转，缩放，倾斜等效果，不破坏文档流布局

- 平移：translate(x,y)，沿x/y轴移动，像素或百分比
- 旋转：rotate(angle) 以元素中心为基点顺时针旋转，需加单位deg(负值为逆时针)
- 缩放：scale(sx,sy)
- 倾斜：skew(xangle,yangle)沿x/y轴扭曲形状，参数为倾斜角度(支持负值)
## 1.1平移
例：transform: translateY(100px)

**补充**：

添加鼠标经过元素移动，优先transform而不是通过left、top等，性能更佳。如果单位是百分比，相对于元素自身尺寸，而非父容器

## 1.2旋转
例：
- transform: rotate(180deg);
- transform-origin: left；设置旋转中心点，属性值为left、top等，也可以设置像素或者百分比等
行内元素的布局特性（无法设置宽高、盒模型限制、transform 基准异常）会破坏旋转效果的稳定性和精确性，所以文字类要转换行内块或者块级元素。 比如字体图标需要转换。
## 1.3缩放
例： transform: scale(1.5);放大1.5倍
## 1.4倾斜
例： transform: skewY(8deg);
## 1.5过渡
完整写法：transition: 过渡属性 持续时间 速度曲线 延迟时间;
例：transition: all 1s linear 1s;(所有属性添加过渡效果，过渡持续1s，匀速，延迟1s执行)

速度曲线：ease linear 贝塞尔曲线等

## 变换复合写法
transform: A() B() C() 先执行C再执行B最后执行A
## 1.6透视
- 给父元素添加，里面所有子元素都会添加透视效果。（常用）perspective: 1000px;
- 给子元素添加，当前元素添加透视效果。注意：perspective()必须作为 transform属性的第一个函数（否则无效） transform:perspective(400px) rotateX(45deg);
- 控制元素背面的可见性（默认镜像显示），常用于隐藏背面（如扑克牌翻转效果）backface-visibility: hidden;
## 1.7 3D位移
transform: translate3d(0, 0, 60px);transform: translateZ(60px);

注意：
- 正值元素靠近观察者（放大），负值远离观察者（缩小）
- 需父容器设置 perspective 属性才能生效，否则无视觉变化
- 父容器需设置 transform-style: preserve-3d; 使子元素保留3D位置（如 3D 卡片翻转）。

# 2.动画
定义动画+使用动画
animation: 动画名称  动画时长

```css
    /* 第一定义动画 */

    @keyframes rotate {

      0% {

        transform: rotate(0deg);

      }

  

      100% {

        transform: rotate(360deg);

      }

    }

  

    /* 第二调用动画 */

    .circle {

      /* 动画匀速并且无限次播放 */

      animation: rotate 1s linear infinite;

    }
```
动画属性详解：
- animation: 动画名称 动画时长 速度曲线 延迟时间 播放次数 播放方向 执行完毕状态；

- 动画属性animation-play-state：暂停或者继续动画，需单独设置
- 速度曲线：linear ease cubic-bezier等还有steps(用于控制动画分段执行的计时函数，它通过将动画分割为离散的步骤，实现类似传统帧动画（逐帧动画）的跳跃效果。)
-  animation: move 1s steps(25) infinite;

**补充**：
- inset: 3px; 针对于定位，写法更简单等价于 top: 3px; left: 3px right: 3px; bottom: 3px
- :has() 选择器; :has() 允许你“根据子元素的特征反向选择父元素”也被称为“父选择器”或“存在选择器”
- box-reflect: 倒影方向(above below left right) 倒影距离 倒影图像;
- :not(); 否定选择器作用是“排除”符合某些条件的元素，让样式作用于剩余元素。