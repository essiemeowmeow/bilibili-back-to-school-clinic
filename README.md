# 不想开学门诊 H5 编辑说明

## 文件说明

| 文件 | 用途 |
|---|---|
| `index.html` | H5 小游戏主文件，用浏览器打开即可运行 |
| `README.md` | 本说明文件 |
| `策划方案.md` | 完整策划文档 |

## 如何运行

1. 双击 `index.html` 文件，即可在浏览器中打开。
2. 建议用手机浏览器或电脑浏览器的"手机模拟模式"查看，效果更佳。
3. 如果本地打开后点击无反应，可尝试通过本地服务器方式打开（如 `python3 -m http.server 8000`），部分浏览器对本地文件的 JS 执行有限制。

## 如何编辑内容

H5 的所有可配置内容都集中在 `index.html` 文件顶部、标记为 **"可编辑配置区"** 的 `CONFIG` 对象里。

你不需要修改 HTML/JS 代码，只需要改 `CONFIG` 对象里的内容即可。

### 1. 修改首页文案

找到 `CONFIG.home` 部分：

```javascript
home: {
    brand: "哔哩哔哩",                          // 标题上方的品牌标签
    title: "不想开学门诊",                       // 主标题
    subtitle: "专治各种不想上学的疑难杂症",     // 副标题
    showTV: false,                              // 是否显示小电视 emoji：true=显示，false=隐藏
    features: ["挂号免费", "名医坐镇", "现场开方", "立刻重启"],  // 首页特色标签，2x2 排列
    startBtnText: "去挂号",                     // 主按钮文字
    detailLinkText: "👀 看看这门诊什么来头"     // 详情页入口按钮文字
}
```

### 2. 修改科室和症状

找到 `CONFIG.departments` 部分。每个科室的结构如下：

```javascript
{
    id: "knowledge",           // 科室唯一标识，不要重复
    name: "知识蒸发科",         // 科室名称
    icon: "🧠",                // 科室图标（emoji 即可）
    symptoms: [                // 症状列表
        { id: "k1", name: "知识已蒸发", desc: "暑假把脑子格式化了" },
        { id: "k2", name: "CPU冒烟症", desc: "一看到课表CPU开始冒烟" },
        { id: "k3", name: "DDL提前焦虑", desc: "DDL还没开始已经焦虑" }
    ]
}
```

注意：
- 每个症状的 `id` 必须唯一，不能重复。
- 症状 `id` 建议用"科室id + 序号"的形式，例如 `k1`、`k2`、`k3`。

### 3. 修改 UP 主医生

找到 `CONFIG.doctors` 部分。每位医生的结构如下：

```javascript
{
    id: "bdao",                       // 医生唯一标识
    name: "毕导THU",                   // 医生名字
    title: "学习/科研方法科主任",       // 医生职称
    avatar: "🎓",                      // 医生头像（emoji 即可）
    quote: "你的大脑不是被格式化了...", // 医生寄语
    departments: ["knowledge"]        // 主治科室 id，可填多个
}
```

### 4. 修改处方内容

找到 `CONFIG.prescriptions` 部分。每个科室对应一个处方，键名是科室的 `id`：

```javascript
prescriptions: {
    knowledge: {                       // 对应知识蒸发科的 id
        title: "知识重启方",            // 处方标题
        items: [                       // 处方内容列表
            { name: "B站课堂专区《开学第一课》", desc: "由名师带你3小时重构知识体系", usage: "每日1课时，连续服用3天" },
            { name: "取景框看世界《大学如何不虚度》", desc: "从目标管理到时间规划一网打尽", usage: "睡前观看，笔记服用" }
        ],
        doctorNote: "禁止自我怀疑，你只是需要一个'哔'的一声重启。"  // 医师寄语
    }
}
```

如果你新增了科室，记得在 `prescriptions` 里新增对应的处方，否则系统会默认使用知识蒸发科的处方。

### 5. 修改新学期 Flag 清单

找到 `CONFIG.certificate.flags` 部分：

```javascript
flags: [
    "这学期绝不挂科",
    "早八成功起床率提高到 80%",
    "每周坚持看一部纪录片"
]
```

### 6. 修改分享文案

找到 `CONFIG.certificate.shareTextTemplate`：

```javascript
shareTextTemplate: "我在 B 站「不想开学门诊」挂了号，确诊为【{symptom}】。主治医师 {doctor} 给我开了新学期处方单，状态重启中……你也来挂个号吧！"
```

其中 `{symptom}` 会自动替换为用户选择的主要症状，`{doctor}` 会自动替换为医生名字。

### 7. 修改详情页内容

找到 `CONFIG.details.sections` 部分：

```javascript
sections: [
    {
        title: "项目背景",
        paragraphs: ["段落1", "段落2"]   // 纯文本段落
    },
    {
        title: "目标人群",
        list: ["人群1", "人群2", "人群3"]  // 列表项
    }
]
```

## 注意事项

1. **不要删除 `CONFIG` 对象外的 HTML/JS 代码**，除非你确定知道自己在做什么。
2. **所有 id 必须唯一**，否则症状选择会出错。
3. 修改后保存文件，刷新浏览器即可看到效果。
4. 如果要在微信/站内传播，需要把 `index.html` 部署到服务器，获取在线链接。

## 视觉风格

本版 H5 参考年轻涂鸦/插画风格设计，采用：
- 糖果色系（粉色、薄荷绿、天空蓝、薰衣草紫、奶油黄）
- 粗黑边描边、手绘感装饰（星星、云朵、波浪线）
- 圆润卡片 + 涂鸦阴影效果
- 标题使用「站酷快乐体」艺术字，英文使用「Fredoka One」手写风格字体
- 证书页支持生成图片保存/分享

如需调整配色，可修改 `index.html` 中 `:root` 变量（如 `--pink`、`--mint`、`--sky`、`--yellow` 等）。

## 部署上线（如需在线链接）

目前这个 H5 是单个 HTML 文件，零依赖。要生成在线链接，可以：

- 上传到 B站内部 H5 平台
- 上传到任意静态网页托管服务（如 GitHub Pages、Vercel、腾讯云 COS 等）
- 交给前端同事接入现有活动页面框架

部署后，把生成的链接填入首页"查看活动方案详情"或传播渠道即可。
