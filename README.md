# FloorLED 完整地砖屏 · 大澳渔庄灯光工作台

版本：0.3.0。基于用户提供的 MIT 授权 dsh-swf-studio 0.2.1 扩展，保留 60 个主题并固定使用 FloorLED 完整走道模式。安装后侧栏入口为「大澳渔庄灯光工作台」。本插件本地生成图形与 SWF，不调用模型。

## 功能定位

- 面向餐厅、宴会厅、婚礼、升学宴、生日宴、年会和庆典的地砖屏内容制作。
- 内置 60 个主题和 11 个分类，可填写姓名、标题、日期、地点、祝福语及双方向文案。
- 支持 FloorLED 完整走道、A/B 旋转方向、画布尺寸、偏移、字体、颜色、装饰和动画密度。
- 本地导出 SWF、预览 PNG 和可继续编辑的 `project.json`。
- 全程在本机生成，不调用模型，也不产生模型 token 费用。

## 与桌面端和插件市场的关系

本仓库是独立的 DSH 插件仓库，插件不会编译进 [desktop-ipzsk](https://github.com/ipzsk/desktop-ipzsk) 安装包。发布新版本时在本仓库创建 GitHub Release；开发者再通过 [IPZSK 开发者中心](https://www.ipzsk.com/developer) 提交版本。审核通过后，[token-ipzsk](https://github.com/ipzsk/token-ipzsk) 将该版本加入 `/api/me/plugin-market`，桌面端据此安装或更新。

插件市场安装前会核对审核版本、包名、版本、文件大小和 SHA-256。桌面端更新与本插件更新相互独立，升级插件无需重新安装客户端。仓库创建或发布 Release 不会自动上架，最终状态以 IPZSK 插件市场审核目录为准。

当前版本：[v0.3.0](https://github.com/ipzsk/plugin-dsh-swf-studio/releases/tag/v0.3.0)。

## 六个仓库如何协作

| 仓库 | 职责 |
| --- | --- |
| [web-ipzsk](https://github.com/ipzsk/web-ipzsk) | 官网、账户、开发者中心和 Web 创作工作台 |
| [desktop-ipzsk](https://github.com/ipzsk/desktop-ipzsk) | DeepSeek 官方底座、IPZSK 登录和插件市场宿主 |
| [token-ipzsk](https://github.com/ipzsk/token-ipzsk) | 账户、号池、计费、插件审核和市场目录 |
| [plugin-dsh-imagegen](https://github.com/ipzsk/plugin-dsh-imagegen) | AI 生图与改图插件 |
| [plugin-dsh-doc-to-excel](https://github.com/ipzsk/plugin-dsh-doc-to-excel) | Word/PDF 转分类 Excel 插件 |
| [plugin-dsh-swf-studio](https://github.com/ipzsk/plugin-dsh-swf-studio) | 当前仓库，FloorLED 与 SWF 场景制作插件 |

## 可定制内容

- 新郎、新娘姓名，可选择显示姓名或副标题；其他活动可隐藏姓名。
- 酒席方向主标题、副标题、日期地点、祝福语。
- 主席台方向主标题、副标题和祝福语，文字栏支持换行。
- 单一竖向预览同时显示酒席区域和主席台区域，不提供分区预览选项。
- A/B 整体朝向相差 180°，用于适配现场播放方向。
- 导出画面大小、可见走道像素长度/宽度、X/Y 偏移。
- 丰富/轻柔/关闭动效、密度、字体和文字颜色；动画固定为 20 秒、24 FPS 循环。
- JSON 工程保存和重新导入，保存全部定制参数。切换主题可选择保留文案；姓名与现场参数默认保留。

## 本现场默认值

地砖屏 32×7 块，每块 25×25 厘米，实物约 8×1.75 米。实物厘米数不能用于推算像素。

沿用此前已验证的 FloorLED 窗口：2408×512；关键画面在左侧 2048×512，剩余 360 像素留作同色背景。动画固定为 24 FPS、20 秒循环。完整走道包含 3/4 酒席区域和 1/4 主席台区域，两区文字相向摆放。

## 使用

1. 在兼容的 DeepSeek Harness 桌面宿主中安装本目录外的 tgz 插件包，参考 WINDOWS.md。
2. 打开侧栏「大澳渔庄灯光工作台」，选择主题。默认开启 FloorLED 模式。
3. 填写姓名、酒席文案和主席台文案，选择 A/B 朝向，在右侧完整竖向走道预览中检查可读性。
4. 点击「生成 SWF 文件」。默认保存至用户 Downloads/IPZSK-SWF 下独立子目录，包含 SWF、project.json、preview.png。
5. 在 FloorLED 素材列表添加生成的 SWF，沿用已有输出窗口设置；方向相反时将插件切到 B 方向重新导出。
6. 后续导入 project.json，可继续修改任何参数并重新生成。

## 技术与验证范围

FloorLED 输出为 CWS v9，中文与静态装饰嵌入位图，整条走道使用连续边缘粒子循环，不含 ActionScript。背景与文字图层在整段时间轴只放置一次，动画只更新粒子对象。透明图片使用预乘 ARGB，矩阵支持旋转、缩放和透明度。

自动化检查覆盖编辑、主题切换、导出、工程导入与分类筛选。60 个主题均可按 A/B 朝向生成包含酒席和主席台区域的 SWF。

新插件包尚未在实际 DeepSeek Harness 宿主内运行验证；新生成的 120 个 SWF 也尚未逐个在 FloorLED/实体屏幕试播。此前同尺寸婚礼 SWF 已由用户确认正常，但这不等于新导出器已经得到硬件验证。

本插件不直接控制传感器、发送卡或 FloorLED 进程；脚踏互动继续由现有 FloorLED 负责。尚未封装硬件协议或传感器网页桥接服务。

## 开发

Node.js ≥22.19。源码无运行时 npm 依赖，React 由宿主提供。

```sh
node scripts/build.mjs
node --test tests/*.test.mjs
```

build.mjs 为本项目固定命名 ESM 模块生成宿主的 __ModuleLoader__ 客户端包，不使用在线编译器。保留原作者 LICENSE。
