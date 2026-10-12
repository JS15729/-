# 大数据技术栈综合实战项目

> 基于 **HDFS + Hive + Spark SQL + MySQL + ECharts** 五种技术栈，实现从数据采集、离线存储、数据清洗、离线分析到可视化展示的大数据全流程成果。

---

## 一、项目简介

<!-- 请在此补充：项目要解决的业务问题、面向的使用场景与目标用户 -->

本项目是一个覆盖大数据处理全链路的综合实战项目，用于实践分布式存储、离线 SQL 计算、内存计算引擎与前端可视化的协同工作，形成一套可复用的大数据分析解决方案。

---

## 二、技术栈

| 技术 | 版本 | 职责 |
|------|------|------|
| Hadoop / HDFS | 3.3.x | 分布式存储层，原始数据落地 |
| Hive | 3.1.x | 离线数据仓库，SQL 建表与 ETL |
| Spark SQL | 3.3.x | 内存计算引擎，聚合分析与计算 |
| MySQL | 8.0.x | 结果数据存储，供上层查询 |
| ECharts | 5.x | 前端数据可视化展示 |

---

## 三、架构流程

```
原始数据源
     ↓
[数据采集/预处理]  Python 脚本清洗整理
     ↓
[ODS 层] HDFS + Hive  原始数据存储
     ↓
[DWD 层] Hive SQL    数据清洗（去重/脱敏/补缺/过滤异常）
     ↓
[DWS 层] Spark SQL   聚合宽表（统计指标/衍生字段）
     ↓
[结果层] MySQL        业务统计表
     ↓
[可视化] ECharts      图表大屏
```

---

## 四、目录结构

```
project_root/
├── README.md                ← 本说明文件
├── data/                    ← 数据准备与预处理脚本
│   └── preprocess.py        ← 数据清洗 / 标准化脚本
├── hive/                    ← Hive SQL 脚本
│   ├── create_ods.sql       ← ODS 层建表
│   └── dwd_etl.sql          ← DWD 层清洗 ETL
├── spark/                   ← Spark 计算脚本
│   ├── dws_aggregate.py     ← DWS 层聚合分析
│   └── export_to_mysql.py   ← 结果导出到 MySQL
├── mysql/                   ← MySQL 建表脚本
│   └── create_tables.sql    ← 业务结果表
└── frontend/                ← 前端可视化
    └── dashboard.html       ← ECharts 数据大屏
```

---

## 五、执行步骤

### Step 1：数据准备
```bash
python data/preprocess.py
```

### Step 2：上传 HDFS 并建表
```bash
hdfs dfs -mkdir -p /warehouse/your_project/{ods,dwd,dws}
hdfs dfs -put data/xxx.csv /warehouse/your_project/ods/
hive -f hive/create_ods.sql
```

### Step 3：DWD 层清洗
```bash
hive -f hive/dwd_etl.sql
```

### Step 4：DWS 层聚合分析
```bash
spark-submit --master yarn \
  --executor-memory 4g --num-executors 3 \
  spark/dws_aggregate.py
```

### Step 5：结果写入 MySQL
```bash
mysql -u root -p < mysql/create_tables.sql
spark-submit --jars /opt/jars/mysql-connector-java-8.0.33.jar spark/export_to_mysql.py
```
> ⚠️ 运行前请修改脚本中的数据库密码配置。

### Step 6：前端可视化
```bash
# 浏览器直接打开
frontend/dashboard.html
```

---

## 六、核心分析结果

<!-- 请在此补充：本项目实际产出的关键统计指标与业务结论 -->

| 指标 | 数值 |
|------|------|
| 待补充 | 待补充 |

---

## 七、环境依赖

- Hadoop 3.3.x / HDFS
- Hive 3.1.x
- Spark 3.3.x（PySpark）
- MySQL 8.0.x
- Python 3.8+
- ECharts 5.x

---

## 八、License

本项目使用 [The Unlicense](LICENSE) 协议开源。

---

*大数据技术栈综合实战项目*