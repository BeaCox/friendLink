# issues-json-generator

自动提取本仓库 issues 中第一段 `JSON` 代码块并保存到仓库中，解决了直接调用 GitHub API 频率有限制以及速度过慢的问题。（你可以通过其它 N 种方式访问仓库文件）

例如动态友链：https://github.com/xaoxuu/friends

随意发挥你的创意吧～



## 使用方法

1. fork 本仓库，把 `config.yml` 配置改为自己的：

```yaml
issues:
  repo: BeaCox/friendLink # 仓库持有者/仓库名
  # 第一步筛选，state
  state: # 留空则从所有issue中抓取，open则从所有open的issue中抓取，closed从所有closed的issue中抓取
  # 第二步筛选，label
  label: active  # 只能配置1个或留空，留空则所有满足`state`的issue都会被抓取。配置1个时，issue只有在具有该标签时才被抓取
  groups: # 填写用来分组的label名称。留空则所有被抓取的issue输出至data.json，否则按照输出与组名同名的json文件
  sort: updated-desc # 排序，按最近更新，取消此项则按创建时间排序
```
配置实例说明如下
| state         | label         | groups                      | 输出文件                | 抓取issue                                 |
| ------------- | ------------- | --------------------------- | ----------------------- | ----------------------------------------- |
| state:        | label: active | groups:                     | data.json               | 所有label包含active的issue                |
| state:        | label: active | groups: ["ordinary", "top"] | ordinary.json, top.json | label包含active且包含ordinary或top的issue |
| state:        | label:        | groups:                     | data.json               | 所有issue                                 |
| state:        | label:        | groups: ["ordinary", "top"] | ordinary.json, top.json | label包含ordinary或top的issue             |
| state: open   | label: active | groups:                     | data.json               | 所有label包含active的、open的issue        |
| state: closed | label: active | groups:                     | data.json               | 所有label包含active的、closed的issue      |

2. 打开 action 运行权限。

## 测试是否配置成功

1. 新建 issue 并按照模板要求填写提交。
2. 等待 Action 运行完毕，检查 `output` 分支是否有 `/v2/data.json` 文件或`/v2/<组名>.json`，内容是否正确，如果正确则表示已经配置成功。

