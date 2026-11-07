# 淘宝用户行为分析

本项目使用 Python、Pandas 和 Matplotlib 分析淘宝用户的浏览、加购、收藏和购买行为。[分析 Notebook](code.ipynb) 保留了汇总结果和图表，可直接预览。

## 分析范围

从原始文件读取前 10 万条记录，将时间转换为北京时间，保留 2017 年 11 月 25 日至 12 月 3 日的行为。有效样本包含 99,956 条行为、983 位用户和 64,440 件商品。原始文件中的记录按用户集中排列，样本统计仅描述这批记录。

| 分析内容 | 样本结果 |
| --- | --- |
| 行为分布 | 分别统计浏览、加购、收藏和购买的次数 |
| 小时活跃度 | 21 点的去重活跃用户最多，共 708 人 |
| 固定用户组回访 | 11 月 25 日活跃的 695 人中，685 人于 12 月 3 日再次活跃（98.56%） |
| 活跃度分层 | 按活跃天数分组，比较各组人数占比和购买行为贡献 |
| 加购用户的购买行为 | 723 位加购用户中，有 196 位在观察期内无购买记录（27.11%） |

回访按首日活跃的固定用户组统计。加购与购买按用户统计，适用于描述观察期内是否出现过这两种行为。

## 本地复现

1. 从 [阿里云天池的淘宝用户购物行为数据集](https://tianchi.aliyun.com/dataset/649) 下载并解压 `UserBehavior.csv`，放到 `code.ipynb` 所在目录。CSV 无表头，字段依次为用户 ID、商品 ID、类目 ID、行为类型和 Unix 时间戳。
2. 在项目目录安装依赖并启动 Jupyter。

   ```bash
   python -m pip install -r requirements.txt
   python -m notebook
   ```

3. 打开 `code.ipynb` 并运行全部单元。图表中文可使用黑体或微软雅黑。
4. Notebook 的导出单元会生成 `powerbi_data.csv`，可在 Power BI 中导入。原始数据、逐条行为导出和本地 Power BI 报表均保留在本地。

## 可选的 MySQL 入库

如需将样本写入 MySQL，先安装 `sqlalchemy` 和 `pymysql`，再在启动 Jupyter 的环境中设置 `TAOBAO_MYSQL_USER` 和 `TAOBAO_MYSQL_PASSWORD`。可通过 `TAOBAO_MYSQL_HOST` 指定服务器，默认使用 `localhost`。所用账户需有创建 `taobao_db` 及写表的权限。写入单元会替换项目库中的 `user_behavior` 表。
