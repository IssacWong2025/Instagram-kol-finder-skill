# Instagram KOL Finder - 下载后使用指南

## 🎉 欢迎使用 Instagram KOL Finder Skill！

这是一个帮助你自动查找和筛选 Instagram KOL（关键意见领袖）的强大工具。

## 📥 第一步：导入 Skill 到 Claude

### 方法 1：通过 Claude.ai（推荐）

1. 下载 `instagram-kol-finder-skill.skill` 文件
2. 打开 Claude.ai
3. 在聊天界面中上传该 .skill 文件
4. Claude 会自动导入这个 skill

### 方法 2：通过 Claude Code

如果你使用 Claude Code：
```bash
# 将 .skill 文件解压到你的项目目录
unzip instagram-kol-finder-skill.skill -d ./instagram-kol-finder
cd instagram-kol-finder
```

## ⚙️ 第二步：配置（10分钟）

### 1. 注册 Apify 账号（3分钟）

**为什么需要 Apify？**
- Apify 提供稳定的 Instagram 数据抓取服务
- 成功率 95%+，远超免费方案
- 有 $5 免费额度用于测试

**注册步骤：**
1. 访问 https://apify.com
2. 点击 "Sign up" 注册
3. 验证邮箱
4. ✅ 自动获得 $5 免费额度

### 2. 获取 API Token（2分钟）

1. 登录 Apify
2. 点击右上角头像 → **Settings**
3. 左侧菜单选择 **Integrations**
4. 找到 "Personal API token"
5. 点击 **Copy** 复制

⚠️ **重要**：妥善保管这个 Token，不要分享给任何人！

### 3. 配置 Token（2分钟）

找到并编辑文件：`scripts/apify_config.py`

找到这一行：
```python
APIFY_API_TOKEN = "YOUR_APIFY_API_TOKEN_HERE"
```

替换为你复制的 Token：
```python
APIFY_API_TOKEN = "apify_api_你的实际token"
```

**保存文件**（Ctrl+S 或 Cmd+S）

### 4. 自定义配置（可选，2分钟）

编辑文件：`scripts/kol_finder_config.py`

```python
# 修改要抓取的 hashtags
HASHTAGS = [
    'fashion',      # 改成你的行业相关标签
    'beauty',
    'lifestyle',
]

# 调整筛选条件
MIN_FOLLOWERS = 5000        # 最小粉丝数
MAX_FOLLOWERS = 50000       # 最大粉丝数
MIN_ENGAGEMENT_RATE = 2.0   # 最低互动率（%）

# 设置目标地区
TARGET_LOCATIONS = ['US', 'UK']  # 国家代码
```

### 5. 安装依赖（1分钟）

在终端运行：
```bash
pip install -r scripts/requirements.txt
```

等待安装完成。

## 🚀 第三步：开始使用

### 方式 1：快速测试（推荐新手）

```bash
python scripts/instagram_kol_finder_apify.py
```

按提示输入：
- **Hashtag**: `fashion` （不需要 # 号）
- **抓取数量**: `20`
- **粉丝范围**: `5000-50000`
- **互动率**: `2.0`

等待 1-2 分钟，完成！

### 方式 2：批量处理（推荐老手）

```bash
python scripts/kol_finder_optimized.py
```

这个版本会：
- ✅ 根据配置文件批量处理多个 hashtag
- ✅ 自动去重（避免重复处理同一用户）
- ✅ 成本优化（自动控制花费）
- ✅ 自动导出 Excel 报表

## 📊 查看结果

### Excel 报表

打开 `data/` 目录，找到最新的 Excel 文件：
```
data/kols_合集_20241104_143022.xlsx
```

**包含内容：**
- 用户名
- 粉丝数
- 互动率
- Instagram 主页链接（可点击）
- 地区信息
- Bio 简介

### SQLite 数据库

如果需要程序化处理数据：
```
data/kol_database.db
```

可以用 SQLite 工具打开查询。

## 💰 成本说明

### Apify 定价
- **免费额度**: $5（测试用）
- **个人套餐**: $49/月（适合日常使用）
- **团队套餐**: $499/月（大规模使用）

### 实际成本
- **抓取 100 个帖子** ≈ $0.05
- **获取 100 个用户资料** ≈ $0.10

### 使用建议

**日常使用（每天 30 个帖子）：**
- 成本：约 $0.035/天
- $5 可用：约 143 天（近 5 个月）

**建立 KOL 库（每天 100 个帖子）：**
- 成本：约 $0.11/天
- $5 可用：约 45 天（1.5 个月）

**建议：**
1. 先用 $5 免费额度充分测试
2. 确认 ROI（投资回报率）后再升级
3. 设置成本限制避免超支

## 🎯 使用技巧

### 技巧 1：选择合适的 Hashtag

❌ **太宽泛**：`#love`, `#instagood`（竞争激烈）
✅ **刚刚好**：`#hairstylist`, `#beautytips`（精准定位）

**建议策略：**
- 混合使用 2-3 个热门标签
- 加上 2-3 个细分标签

### 技巧 2：合理设置粉丝范围

**新品牌（预算有限）：**
```python
MIN_FOLLOWERS = 1000
MAX_FOLLOWERS = 10000
```
特点：性价比高，容易合作

**成长品牌（有一定预算）：**
```python
MIN_FOLLOWERS = 10000
MAX_FOLLOWERS = 50000
```
特点：平衡曝光和成本（**推荐**）

**成熟品牌（追求影响力）：**
```python
MIN_FOLLOWERS = 50000
MAX_FOLLOWERS = 200000
```
特点：影响力大，成本较高

### 技巧 3：提高互动率阈值

**一般筛选：**
```python
MIN_ENGAGEMENT_RATE = 2.0
```

**优质筛选：**
```python
MIN_ENGAGEMENT_RATE = 5.0
```

**顶级筛选：**
```python
MIN_ENGAGEMENT_RATE = 10.0
```

互动率越高，KOL 质量越好！

### 技巧 4：成本控制

在配置文件设置：
```python
MAX_COST_PER_RUN = 0.5  # 单次最多花 $0.5
```

程序会在接近限制时自动停止。

### 技巧 5：增量抓取

程序会自动记录已处理的用户，下次运行会跳过重复：

```
第 1 次运行：处理 50 个用户
第 2 次运行：只处理新的用户（自动跳过已处理的）
第 3 次运行：继续只处理新用户
```

节省成本和时间！

## ⚠️ 常见问题

### Q1: 提示 "API Token 无效"？

**检查：**
1. Token 是否完整复制（没有多余空格）
2. 文件是否保存（Ctrl+S）
3. Apify 账号是否有余额

**解决：**
重新复制 Token，确保完整。

### Q2: 找不到任何 KOL？

**可能原因：**
1. Hashtag 太冷门
2. 筛选条件太严格

**解决：**
- 尝试更热门的 hashtag（如 `fashion`、`beauty`）
- 放宽筛选条件（降低粉丝数下限）

### Q3: 成本太高？

**优化方法：**
1. 减少每次抓取数量：
   ```python
   POSTS_PER_HASHTAG = 20  # 改为 20
   ```

2. 限制每次运行的 hashtag 数：
   ```python
   HASHTAGS_PER_RUN = 2  # 每次只处理 2 个
   ```

3. 设置成本上限：
   ```python
   MAX_COST_PER_RUN = 0.5
   ```

### Q4: Excel 文件中文乱码？

**Windows 用户：**
1. 用 Excel 打开
2. 数据 → 获取数据 → 从文件 → 从文本/CSV
3. 选择文件编码：UTF-8

**Mac 用户：**
直接用 Excel 打开，通常没问题。

### Q5: 如何提高地区检测准确率？

**方案 1：免费方案（70-80% 准确率）**
保持默认配置，使用关键词检测。

**方案 2：付费方案（85-95% 准确率）**
启用 LLM 增强检测：

```python
USE_LLM_LOCATION_DETECTION = True
LLM_PROVIDER = 'openai'
OPENAI_API_KEY = "你的OpenAI密钥"
OPENAI_MODEL = 'gpt-3.5-turbo'  # 最便宜
```

成本：约 $0.002/用户

## 📚 进阶使用

### 批量处理多个 Hashtag

编辑 `scripts/kol_finder_config.py`：

```python
HASHTAGS = [
    # 美发相关
    'hairstyle',
    'haircare',
    'hairtutorial',
    
    # 美妆相关  
    'makeup',
    'beauty',
    'skincare',
    
    # 时尚相关
    'fashion',
    'ootd',
    'style',
]

HASHTAGS_PER_RUN = 3  # 每次处理 3 个
```

然后运行优化版：
```bash
python scripts/kol_finder_optimized.py
```

### 定时自动运行

**Linux/Mac（使用 cron）：**
```bash
# 编辑 crontab
crontab -e

# 添加每天早上 9 点运行
0 9 * * * cd /path/to/skill && python scripts/kol_finder_optimized.py
```

**Windows（使用任务计划程序）：**
1. 打开"任务计划程序"
2. 创建基本任务
3. 设置触发器（每天、每周等）
4. 操作：运行 Python 脚本

### 导出到 Google Sheets

可以使用 `gspread` 库将数据导出到 Google Sheets：

```bash
pip install gspread oauth2client
```

参考 Google Sheets API 文档实现。

## 🔐 安全提示

### ✅ 必须做：
- 定期更换 Apify Token（建议每月）
- 不要把配置文件上传到公开 GitHub
- 监控 Apify 账单，避免意外超支
- 只用于合法商业合作联系

### ❌ 不要做：
- 分享 API Token 给他人
- 用于骚扰或垃圾信息
- 违反 Instagram 服务条款
- 大量抓取后不删除敏感数据

## 📞 获取帮助

### 查看文档

1. **主文档**: `SKILL.md`
2. **快速开始**: `references/quick-start.md`
3. **配置指南**: `references/configuration-guide.md`

### 测试工具

```bash
# 测试 Apify 连接
python scripts/apify_instagram_client.py

# 查看当前配置
python scripts/kol_finder_config.py
```

### 官方资源

- Apify 文档：https://docs.apify.com
- Instagram Scraper：https://apify.com/apify/instagram-hashtag-scraper
- Profile Scraper：https://apify.com/apify/instagram-profile-scraper

## 🎉 开始你的 KOL 营销之旅！

**准备好了吗？**

✅ 已注册 Apify
✅ 已配置 Token
✅ 已安装依赖
✅ 已阅读使用技巧

**立即开始：**
```bash
python scripts/kol_finder_optimized.py
```

**几分钟后，你将拥有第一批精心筛选的 KOL 列表！** 🚀

---

**祝使用顺利！有问题随时查看文档。**
