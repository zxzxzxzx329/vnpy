# 市场信号雷达模块（MarketRadar）

&nbsp;

该模块的主要功能，是允许用户基于自定义Python数学公式，实时计算衍生行情数据。



一看之下可能会觉得和SpreadTrading模块中的价差组合行情计算功能重复了，但实际上两者在功能定位上完全不同：

- **MarketRadar模块**

  - 定位**分析**，主要用于扫描和寻找市场信号机会
  - 支持灵活的Python数学公式：加减乘除、内置函数（max/min等）
  - 基于公式内各个合约的最新成交价，计算自定义公式的最新数值

- **SpreadTrading模块**

  - 定位**交易**，主要用于执行多条腿的价差组合买卖
  - 只能通过价差腿的系数正负，来实现加减的公式计算
  - 基于各条腿的1档盘口，计算价差组合的盘口价格



在VN Station启动对话框中，加载MarketRadar模块，启动VN Trader后先连接登录交易接口，再打开【市场雷达】组件可以看到类似下图的界面：



![](https://static.vnpy.com/upload/temp/ab87a58a-7c81-45a9-ac54-462e9dd72a2f.png)





在窗口左下角的编辑区中，可以快速创建要扫描的雷达规则（RadarRule）：





![](https://static.vnpy.com/upload/temp/f592704d-0194-4143-8a23-101701eee7ce.jpg)



其中各字段的对应含义如下：

- 名称

  - 雷达规则的名称，注意不能重复

- 公式

  - 规则的计算公式，支持任意合法的Python数学公式
  - 注意其中的变量，只能是A、B、C、D、E（不需要都用）

- A、B、C、D、E

  - 计算公式中要用到的变量对应的合约本地代码（vt_symbol）
  - 收到其中任何一个合约的TICK行情推送时，会实时触发规则计算
  - 不用的变量留空即可

- 小数

  - 公式的最终计算结果保留多少位小数



点击【添加】按钮即可完成新规则的添加，MarketRadar会自动订阅相关合约行情并开始自动扫描计算。



除了跨期价差这种减法求差的规则外，MarketRadar也能支持**金银比**这种比例类的计算规则：






![](https://static.vnpy.com/upload/temp/899637b1-ec9f-420c-8c87-fb0cf44c572e.png)


对于需要调整的规则，也可以同样在左下角输入相应信息（名称请填写要修改的规则名称），点击【修改】按钮即可完成修改。对于不再需要的规则，可以点击监控表中最右侧的【删除】按钮来进行移除。



需要添加较多的雷达规则时，可以通过CSV文件来一次性批量导入，点击窗口右下角的【导入CSV】按钮，在弹出的对话框中找到要导入的CSV文件后打开即可快速完成导入（右下角日志组件中有对应信息输出）：





![](https://static.vnpy.com/upload/temp/9d272b13-b288-4b1e-9c31-2cb4a069b16b.jpg)



CSV文件的格式如下图所示，和编辑区的各字段完全一致：




![](https://static.vnpy.com/upload/temp/d8ed6497-27ed-47c2-98b4-96d56c5177cd.jpg)




结合Excel的表格快速编辑功能，批量添加规则还是挺方便的：




![](https://static.vnpy.com/upload/temp/9ee7dd89-49ce-4ad9-9b5f-cdcae79176e3.jpg)




目前2.1.7版本的MarketRadar只支持雷达规则计算结果的数字显示，后续我们会进一步加入图表显示（参考文华的组合）、条件提醒（警报和发微信）、策略信号订阅等功能。

&nbsp;