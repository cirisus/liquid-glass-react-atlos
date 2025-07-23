# Positioning Mode Feature

## 概述

新增的 `positioning` 属性允许 LiquidGlass 组件支持不同的定位模式，解决了之前只能使用 `top: 50%; left: 50%` 居中定位的限制。

## 支持的定位模式

- `center` (默认): 使用 `translate(-50%, -50%)` 进行居中定位
- `top-left`: 使用 `translate(0, 0)` 从左上角定位
- `top-right`: 使用 `translate(-100%, 0)` 从右上角定位  
- `bottom-left`: 使用 `translate(0, -100%)` 从左下角定位
- `bottom-right`: 使用 `translate(-100%, -100%)` 从右下角定位

## 使用方法

```tsx
import LiquidGlass from 'liquid-glass-react'

// 居中定位 (默认)
<LiquidGlass positioning="center">
  Content
</LiquidGlass>

// 左上角定位
<LiquidGlass 
  positioning="top-left"
  style={{ position: "absolute", top: "20px", left: "20px" }}
>
  Content
</LiquidGlass>

// 右下角定位
<LiquidGlass 
  positioning="bottom-right"
  style={{ position: "absolute", bottom: "20px", right: "20px" }}
>
  Content
</LiquidGlass>
```

## 实现细节

新增了 `calculateTransformByPositioning` 函数，根据不同的定位模式计算正确的 transform 字符串：

- 对于 `center` 模式：保持原有的 `-50%` 偏移
- 对于 `top-left` 模式：不使用百分比偏移，直接应用像素偏移
- 对于 `top-right` 模式：使用 `-100%` 的 X 轴偏移
- 对于 `bottom-left` 模式：使用 `-100%` 的 Y 轴偏移
- 对于 `bottom-right` 模式：使用 `-100%` 的 X 和 Y 轴偏移

同时，`getDefaultPositionStyles` 函数会根据定位模式提供相应的默认 CSS 定位属性。

## 兼容性

- 向后兼容：默认使用 `center` 模式，现有代码无需修改
- 可以与现有的 style 属性结合使用
- 支持所有现有的 LiquidGlass 功能（elasticity、blur、saturation 等）
