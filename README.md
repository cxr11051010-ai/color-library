# 🎨 色彩档案 · GIS 配色方案库

> 上传任意图片自动提取主色调，可手动删减颜色、自定义方案名称与分类标签，构建专属配色档案库。支持一键导出 ArcGIS Pro 可用格式（.clr 色板文件、.stylx 样式包）、通用色彩表（.txt）及 Python 脚本（含 matplotlib、geopandas 示例代码），告别手动调色，让每一张 GIS 专题图都拥有精准、可复用的配色方案。

---

## 功能概览

- **图片提取配色**：上传 JPG、PNG、WEBP、GIF、BMP 格式图片，自动提取 4–12 个主色调
- **颜色筛选**：提取后可逐一删除不需要的颜色，保留最合适的组合
- **方案管理**：为每套配色自定义名称和标签，支持搜索与标签过滤
- **本地持久化**：所有方案保存在本地 `color_schemes.json`，重启不丢失
- **一键导出**：支持多种格式，直接导入 ArcGIS Pro 或 Python 环境使用

---

## 导出格式说明

| 格式 | 适用软件 | 使用方法 |
|------|----------|----------|
| `.clr` | ArcGIS Pro / ArcMap | 放入 `%AppData%\Roaming\Esri\ArcGISPro\ColorSchemes`，重启后在符号化面板中选用 |
| `.stylx` | ArcGIS Pro | Insert 标签页 → Styles → Add → Add Style，选择文件导入 |
| `.txt` | 通用色彩表 | 可用于 QGIS 渐变色加载，或作为颜色数值参考 |
| `.py` | Python | 含 `matplotlib` colormap、`seaborn` 色板、`geopandas` 渲染示例，直接复制使用 |

> **注意**：`.stylx` 仅支持 ArcGIS Pro，不适用于旧版 ArcMap；`.clr` 格式新旧版本均可使用，兼容性最好。

---

## 快速开始

### 安装依赖

```bash
pip install streamlit colorthief pillow
```

### 运行

```bash
streamlit run color_library.py
```

浏览器会自动打开 `http://localhost:8501`，无需额外配置。

---

## 使用流程

```
1. 打开工具，切换到「提取配色」标签页
2. 将图片拖拽到上传框，或点击选择文件
   （小红书截图保存后直接拖入即可）
3. 自动提取颜色 → 点击「× 删除」去掉不需要的颜色
4. 填写方案名称（必填）和标签（选填，逗号分隔）
5. 点击「保存到方案库」
6. 切换到「方案库」标签页，选择方案
7. 选择导出格式，点击下载
8. 导入对应软件使用
```

---

## 文件结构

```
color_library.py       ← 主程序，运行这个文件
color_schemes.json     ← 自动生成，存储所有配色方案（请定期备份）
README.md              ← 本说明文件
requirements.txt       ← 依赖列表（部署到云端时使用）
```

---

## 部署为公开网页（可选）

如需让他人通过链接直接访问，可免费部署到 Streamlit Cloud：

1. 将 `color_library.py` 和 `requirements.txt` 上传到 GitHub 公开仓库
2. 前往 [share.streamlit.io](https://share.streamlit.io)，用 GitHub 账号登录
3. 点击 **New app**，选择对应仓库和文件，点击 **Deploy**
4. 约 2–3 分钟后获得公开访问链接

`requirements.txt` 内容：

```
streamlit
colorthief
pillow
```

> **注意**：部署到云端后，本地 `color_schemes.json` 的数据不会同步上去，且云端数据在应用重启后会清空。如需持久化存储，需额外配置云端数据库。

---

## 常见问题

**Q：提取的颜色不准确？**  
调整侧栏「提取颜色数量」滑块，图片色彩对比越鲜明，提取效果越好。建议使用高饱和度、色彩分明的参考图。

**Q：配色数据保存在哪里？**  
保存在与 `color_library.py` 同目录的 `color_schemes.json` 文件中。迁移时备份此文件即可。

**Q：`.stylx` 导入 ArcGIS Pro 失败？**  
请确认使用的是 ArcGIS Pro 而非旧版 ArcMap。旧版 ArcMap 不支持 `.stylx` 格式，请改用 `.clr`。

**Q：导出的 `.txt` 文件在 QGIS 中无法加载？**  
在 QGIS 中通过：图层属性 → 符号化 → 单波段伪彩色 → 颜色渐变 → 从文件加载，选择 `.txt` 文件。

---

## 依赖说明

| 包名 | 用途 |
|------|------|
| `streamlit` | 网页界面框架 |
| `colorthief` | 图片主色提取算法 |
| `pillow` | 图片读取与处理 |
