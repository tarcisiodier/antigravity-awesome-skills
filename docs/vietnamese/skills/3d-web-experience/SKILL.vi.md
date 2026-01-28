---
name: 3d-web-experience
description: "Chuyên gia xây dựng trải nghiệm 3D cho web - Three.js, React Three Fiber, Spline, WebGL, và các bối cảnh 3D tương tác. Bao gồm các cấu hình sản phẩm (product configurators), danh mục đầu tư 3D (3D portfolios), website nhập vai (immersive websites), và mang lại độ sâu cho trải nghiệm web. Sử dụng khi: Làm website 3D, three.js, WebGL, react three fiber, trải nghiệm 3D."
source: vibeship-spawner-skills (Apache 2.0)
---

# 3D Web Experience

**Vai trò**: Kiến trúc sư Trải nghiệm Web 3D

Bạn mang chiều không gian thứ ba lên web. Bạn biết khi nào 3D nâng tầm trải nghiệm và khi nào nó chỉ là "khoe mẽ". Bạn cân bằng giữa tác động thị giác và hiệu năng. Bạn làm cho 3D trở nên dễ tiếp cận với những người dùng chưa từng chạm vào ứng dụng 3D. Bạn tạo ra những khoảnh khắc kỳ diệu mà không hy sinh khả năng sử dụng (usability).

## Khả năng

- Triển khai Three.js
- React Three Fiber
- Tối ưu hóa WebGL
- Tích hợp mô hình 3D
- Quy trình làm việc với Spline
- Cấu hình sản phẩm 3D (3D product configurators)
- Các bối cảnh 3D tương tác
- Tối ưu hóa hiệu năng 3D

## Các Mẫu (Patterns)

### Lựa chọn 3D Stack

Chọn cách tiếp cận 3D phù hợp

**Khi nào dùng**: Khi bắt đầu một dự án web 3D

```python
## 3D Stack Selection

### So sánh các Tùy chọn
| Công cụ | Tốt nhất cho | Đường cong học tập | Khả năng kiểm soát |
|------|----------|----------------|---------|
| Spline | Prototypes nhanh, designers | Thấp | Trung bình |
| React Three Fiber | React apps, bối cảnh phức tạp | Trung bình | Cao |
| Three.js vanilla | Kiểm soát tối đa, non-React | Cao | Tối đa |
| Babylon.js | Games, 3D hạng nặng | Cao | Tối đa |

### Cây quyết định (Decision Tree)
```
Cần yếu tố 3D nhanh gọn?
└── Có → Spline
└── Không → Tiếp tục

Đang dùng React?
└── Có → React Three Fiber
└── Không → Tiếp tục

Cần hiệu năng/kiểm soát tối đa?
└── Có → Three.js vanilla
└── Không → Spline hoặc R3F
```

### Spline (Khởi đầu Nhanh nhất)
```jsx
import Spline from '@splinetool/react-spline';

export default function Scene() {
  return (
    <Spline scene="https://prod.spline.design/xxx/scene.splinecode" />
  );
}
```

### React Three Fiber
```jsx
import { Canvas } from '@react-three/fiber';
import { OrbitControls, useGLTF } from '@react-three/drei';

function Model() {
  const { scene } = useGLTF('/model.glb');
  return <primitive object={scene} />;
}

export default function Scene() {
  return (
    <Canvas>
      <ambientLight />
      <Model />
      <OrbitControls />
    </Canvas>
  );
}
```
```

### Quy trình Mô hình 3D (3D Model Pipeline)

Chuẩn bị mô hình sẵn sàng cho web (web-ready)

**Khi nào dùng**: Khi chuẩn bị tài sản 3D (assets)

```python
## 3D Model Pipeline

### Lựa chọn Định dạng
| Định dạng | Trường hợp sử dụng | Kích thước |
|--------|----------|------|
| GLB/GLTF | Chuẩn web 3D | Nhỏ nhất |
| FBX | Từ phần mềm 3D | Lớn |
| OBJ | Mesh đơn giản | Trung bình |
| USDZ | Apple AR | Trung bình |

### Quy trình Tối ưu hóa
```
1. Tạo model trong Blender/công cụ khác
2. Giảm số lượng polygon (< 100K cho web)
3. Bake textures (gộp vật liệu)
4. Xuất ra GLB
5. Nén với gltf-transform
6. Kiểm tra kích thước file (< 5MB là lý tưởng)
```

### Nén GLTF
```bash
# Cài đặt gltf-transform
npm install -g @gltf-transform/cli

# Nén mô hình
gltf-transform optimize input.glb output.glb \
  --compress draco \
  --texture-compress webp
```

### Loading trong R3F
```jsx
import { useGLTF, useProgress, Html } from '@react-three/drei';
import { Suspense } from 'react';

function Loader() {
  const { progress } = useProgress();
  return <Html center>{progress.toFixed(0)}%</Html>;
}

export default function Scene() {
  return (
    <Canvas>
      <Suspense fallback={<Loader />}>
        <Model />
      </Suspense>
    </Canvas>
  );
}
```
```

### 3D Điều khiển bởi Cuộn (Scroll-Driven 3D)

3D phản hồi theo hành động cuộn trang

**Khi nào dùng**: Khi tích hợp 3D với cuộn trang

```python
## Scroll-Driven 3D

### R3F + Scroll Controls
```jsx
import { ScrollControls, useScroll } from '@react-three/drei';
import { useFrame } from '@react-three/fiber';

function RotatingModel() {
  const scroll = useScroll();
  const ref = useRef();

  useFrame(() => {
    // Xoay dựa trên vị trí cuộn
    ref.current.rotation.y = scroll.offset * Math.PI * 2;
  });

  return <mesh ref={ref}>...</mesh>;
}

export default function Scene() {
  return (
    <Canvas>
      <ScrollControls pages={3}>
        <RotatingModel />
      </ScrollControls>
    </Canvas>
  );
}
```

### GSAP + Three.js
```javascript
import gsap from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';

gsap.to(camera.position, {
  scrollTrigger: {
    trigger: '.section',
    scrub: true,
  },
  z: 5,
  y: 2,
});
```

### Hiệu ứng Cuộn Phổ biến
- Camera di chuyển qua bối cảnh
- Model xoay khi cuộn
- Hiện/ẩn các phần tử
- Thay đổi màu sắc/vật liệu
- Exploded view animations (hiệu ứng "nổ" các chi tiết)
```

## Anti-Patterns (Nên tránh)

### ❌ 3D chỉ để cho có

**Tại sao tệ**: Làm chậm trang web.
Gây bối rối cho người dùng.
Tốn pin trên mobile.
Không giúp ích cho chuyển đổi (conversion).

**Thay vào đó**: 3D nên phục vụ một mục đích.
Trực quan hóa sản phẩm = tốt.
Các hình khối bay lơ lửng ngẫu nhiên = có lẽ không nên.
Hãy hỏi: một bức ảnh tĩnh có giải quyết được không?

### ❌ 3D Chỉ dành cho Desktop

**Tại sao tệ**: Hầu hết lưu lượng truy cập là mobile.
Giết chết pin điện thoại.
Crash trên các thiết bị yếu.
Người dùng ức chế.

**Thay vào đó**: Test trên thiết bị mobile thật.
Giảm chất lượng trên mobile.
Cung cấp fallback tĩnh (ảnh/video).
Cân nhắc tắt 3D trên thiết bị yếu.

### ❌ Không có Trạng thái Loading

**Tại sao tệ**: Người dùng tưởng web bị lỗi.
Tỷ lệ thoát (bounce rate) cao.
3D tốn thời gian để tải.
Ấn tượng đầu tiên tồi tệ.

**Thay vào đó**: Chỉ báo tiến trình loading.
Skeleton/placeholder.
Tải 3D sau khi trang đã tương tác được.
Tối ưu hóa kích thước model.

## Kỹ năng Liên quan

Hoạt động tốt với: `scroll-experience`, `interactive-portfolio`, `frontend`, `landing-page-design`
