# 云序中心 · 办公楼园区建造演示

**云序中心**是一个基于 Three.js 的交互式办公园区沙盘。场景包括两栋办公塔楼、入口裙楼、广场水景、园区道路和绿化。可播放五阶段建造动画，拖动时间轴查看任意进度，也可一键查看竣工全景。

**Yunxu Office Campus** is an interactive office campus diorama built with Three.js. The scene includes two office towers, a shared entrance podium, a plaza and reflecting pool, roads, and landscaped areas. Play the five-stage construction sequence, scrub to any point, or jump straight to the completed campus.

## 运行 / Run locally

项目是纯静态页面，无需安装 npm 依赖。需要联网加载 Three.js ES modules。

This is a static page with no npm installation. Internet access is required to load the Three.js ES modules.

```bash
python -m http.server 8000
```

打开 / Open: `http://localhost:8000`

也可以用 VS Code 的 Live Server 打开 `index.html`。建议通过本地 HTTP 服务访问，以确保浏览器正确加载 ES modules。

You can also open `index.html` through VS Code Live Server. Serve it over local HTTP so the browser can load ES modules reliably.

## 操作 / Controls

| 功能 | 中文说明 | English |
| --- | --- | --- |
| 播放 / 暂停 | 控制建造动画 | Play or pause construction |
| 从头播放 | 重置到地基阶段并开始播放 | Restart from the foundation stage |
| 查看全景 | 直接跳到竣工园区 | Jump to the completed campus |
| 时间轴 | 拖动查看任意施工进度 | Scrub to any construction progress |
| 鼠标左键 / 触摸拖动 | 旋转视角 | Orbit camera |
| 滚轮 / 双指 | 缩放场景 | Zoom in or out |
| 鼠标右键 | 平移视角 | Pan camera |

## 技术路线 / Technical approach

1. **参数化建模 / Parametric modeling**：以 Three.js 原生 `BoxGeometry`、`CylinderGeometry` 和 `IcosahedronGeometry` 组合楼板、柱、幕墙、机电设备、树木及园区设施；尺寸和楼层数由代码参数控制。The campus is assembled from native Three.js geometries, with dimensions and floor counts controlled in code.
2. **阶段组织 / Stage organization**：施工内容按地基、主体结构、玻璃幕墙、屋顶机电、园区景观分入五个 `THREE.Group`。Five scene groups represent the foundation, structure, curtain wall, roof and equipment, and landscaping.
3. **建造动画 / Construction animation**：时间轴映射为各阶段进度，结合对象显隐与水平裁切面，让构件随进度自下而上出现。The timeline maps to stage progress; visibility and horizontal clipping reveal geometry from bottom to top.
4. **渲染与交互 / Rendering and interaction**：使用 WebGLRenderer、物理材质、阴影、雾、色调映射和 OrbitControls，支持自由查看；HTML/CSS 负责响应式控制面板。WebGL rendering, physical materials, shadows, fog, tone mapping, and OrbitControls provide the interactive view; HTML/CSS powers the responsive controls.

## 视觉风格 / Visual style

- **现代建筑沙盘 / Modern architectural diorama**：双塔与低层裙楼围合中央广场，突出办公园区的整体规划关系。Two towers and a low-rise podium frame the central plaza.
- **冷色科技感 / Cool architectural palette**：蓝灰色玻璃、浅色混凝土、金属框架与深色背景，搭配暖色日光和蓝色补光。Blue-gray glazing, pale concrete, metallic frames, a dark backdrop, warm daylight, and cool fill light.
- **展示型界面 / Presentation UI**：左侧项目叙述，底部施工时间轴，画面主体留给可旋转的 3D 模型。Project context sits on the left while the timeline stays at the bottom, leaving the 3D model in focus.

## 项目结构 / Project structure

```text
office-campus-threejs/
├── index.html   # Three.js 场景、动画和界面 / Scene, animation, and UI
└── README.md    # 使用与技术说明 / Usage and technical notes
```

## 定制与边界 / Customization and scope

在 `index.html` 中修改 `levels` 可调整塔楼位置、平面尺寸、层数及层高；修改 `mats` 可调整材质；`groups` 与 `bounds` 控制施工阶段及裁切范围。

Edit `levels` in `index.html` to change tower positions, footprints, floor counts, and floor heights. Adjust `mats` for materials, and `groups` / `bounds` for the construction stages and clipping ranges.

这是概念展示模型，建筑和施工顺序并非真实工程 BIM 数据，也未包含实际施工机械、结构验算或地理坐标。This is a conceptual visualization rather than an engineering BIM model; it does not include real construction machinery, structural calculations, or georeferenced data.
