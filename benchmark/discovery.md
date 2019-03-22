# 注册服务基准测试

> 作者 张磊

## 数据估算

* 注册服务数 S，估算100
* 服务同步频率 N，配置10秒
* 并发数估算 C=S，估算100
* 评估 并发时长<N

## 基准测试

> 以下基准测试采用分布式模拟并发，持续120秒

### 获取实例列表

| 节点数 | 并发数 | 平均 | 最小 | 最大 | 90th | 95th | 99th | 错误率 | 吞吐率 | 返回量(KB) |
| ---| ---| ---| ---| ---| ---| ---| ---| ---| ---| ---|
| 1 | 100 | 66 | 1 | 1125 | 126 | 129 | 134 | 0 | 326/sec | 26798.41 |
| 1 | 200 | 138 | 2 | 1165 | 148 | 152 | 167 | 0 | 326/sec | 26807.41 |
| 1 | 400 | 280 | 2 | 8125 | 470 | 686 | 1154 | 0 | 327/sec | 26892.44 |
| 1 | 600 | 426 | 1 | 15910 | 904 | 1191 | 2018 | 0 | 323/sec | 27125.76 |
| 1 | 800 | 579 | 2 | 16212 | 1220 | 1665 | 2623 | 0 | 319/sec | 26786.82 |
| 1 | 1000 | 720 | 2 | 27475 | 1595 | 2058 | 3430 | 0 | 320/sec | 26980.88 |

### 获取实例明细

| 节点数 | 并发数 | 平均 | 最小 | 最大 | 90th | 95th | 99th | 错误率 | 吞吐率 | 返回量(KB) |
| ---| ---| ---| ---| ---| ---| ---| ---| ---| ---| ---|
| 1 | 100 | 0 | 0 | 21 | 1 | 1 | 2 | 0 | 630/sec | 1413.88 |
| 1 | 200 | 1 | 0 | 67 | 2 | 2 | 3 | 0 | 849/sec | 1906.27 |
| 1 | 400 | 1 | 0 | 60 | 2 | 2 | 4 | 0 | 954/sec | 2140.79 |
| 1 | 600 | 1 | 0 | 223 | 2 | 2 | 4 | 0 | 1013/sec | 2273.20 |
| 1 | 800 | 1 | 0 | 203 | 2 | 2 | 5 | 0 | 1061/sec | 2380.18 |
| 1 | 1000 | 1 | 0 | 503 | 2 | 4 | 17 | 0 | 1076/sec | 2415.08 |
