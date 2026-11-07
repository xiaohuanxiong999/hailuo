# hailu0（海螺）

一个以「搜索—线索—身份」为核心的悬疑解谜网页游戏。纯静态站点，零构建、零依赖：每个页面都是独立的单文件 HTML（内联 CSS/JS），可以直接双击打开，也可以部署到任意静态托管。

> 站点含剧透，源码请勿公开分享。

## 目录结构

```
index.html                入口（带 sharecode 转发）
search/                   搜索引擎（关键词 → 结果，全部谜题索引都在这里）
haiou/group/              论坛帖：jj（主线索）+ xingqiu + cusi
item/                     海螺百科词条：毁神星 / 阿佩普
news/                     紫薇经济（定时自我删除）、天文观察
xinzhi/ cike/ taosheng/   三家新闻站（新知网 / 此刻网 / 涛声时报）
apophis/                  论坛入口 → 留言板（登录）→ 两位身份的日志
truth/one/                真相一页（登录密码在此）
infuse/                   医药公司官网（关于 / 联系我们）
ending/                   通关页面
assets/                   公共素材
links.json                页面清单
```

## 玩法链路（剧透）

1. `search` 是唯一入口，关键词命中不同站点
2. Infuse 官网留言板输入关键词 → 真相一
3. 真相一给出登录密码 → APOPHIS 留言板
4. 两个身份（prophet / disciple）看到不同日志
5. prophet 日志下方可进入通关页；disciple 会触发演出，演出结束后自动进入通关页

## 状态存储

全部使用 `localStorage`，无后端：

| key | 含义 |
| --- | --- |
| `hl_unlock_apophis` | 解锁 APOPHIS 相关搜索结果 |
| `hl_saw_pwd_article` | 看过密码页 |
| `hl_apo_user` | 当前登录身份 |
| `hl_apo_seen` | 实际登录过的身份列表（防污染） |
| `hl_ziwei_gone` | 紫薇报道已永久消失 |
| `hl_ziwei_seen` | 已看过紫薇报道 |

## 本地预览

```bash
python3 -m http.server 8080     # 然后访问 http://localhost:8080/
```

直接 `file://` 打开也可以，页面内部已对 `file:` 协议做了路径兼容。

## 素材与版权

- 游戏内图片除壁画外均来自 pexels 等免费图像网站
- 壁画原图：“Cat and snake. Book of the Dead Tomb TT 359.jpg”，作者 Ismoon，来源 Wikimedia Commons，许可 CC BY-SA 4.0；本项目对其做了滤镜调色与添加文字处理
- `haiou/group/jj/ad.png` 为该壁画的像素级无损原图，`ad.webp` 为同源无损压缩版，用于页面显示与下载
