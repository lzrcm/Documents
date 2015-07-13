## PC Software Protocol ##
### 0.版本说明 ###
<table><tbody>
<tr>
	<td><B>版本号</B></td>
    <td><B>修改内容</B></td>
    <td><B>修改日期</B></td>
	<td><B>作者</B></td>
	<td><B>审批</B></td>
</tr>
<tr>
	<td>1.0.0</td>
	<td>构建版本</td>
	<td>2015年05月20日</td>
	<td>Leo</td>
	<td></td>
</tr>
<tr>
	<td>1.0.1</td>
	<td>增加测试通道</td>
	<td>2015/7/13 16:37:23</td>
	<td>Leo</td>
	<td></td>
</tr>
</tbody></table>

### 1.引言 ###
#### 1.1编写目的 ####
此文档的目的是为了让开发者之间有一个共同的理解，为软件开发和今后的维护有据可循。
### 2.总体设计 ###
#### 2.1详细通讯协议 ####
- **基本格式**
<table><tbody>
<tr>
	<td><B>帧头</B></td>
    <td><B>帧长度</B></td>
    <td><B>命令及数据</B></td>
	<td><B>校验和</B></td>
</tr>
<tr>
	<td><I>0xFA</I> and <I>0xF5</I></td>
	<td>当前帧有多少字节</td>
	<td>详见命令及数据表格</td>
	<td>之前所有字节的和（不含校验和本身），取2字节（Big-endian）</td>
</tr>
</tbody></table>
- **命令及数据**
<table><tbody>
<tr>
	<td><B>功能</B></td>
    <td><B>描述</B></td>
    <td><B>对象</B></td>
	<td><B>命令</B></td>
	<td><B>数据</B></td>
</tr>
<tr>
	<th rowspan="24">仪器信息</th>
	<th rowspan="2">获取仪器型号</td>
	<td>电脑</td>
	<td>0x01</td>
	<td>----</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x01</td>
	<td>≤14 Bytes ASCII or none</td>
</tr>
<tr>
	<th rowspan="2">获取仪器序列号</td>
	<td>电脑</td>
	<td>0x02</td>
	<td>----</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x02</td>
	<td>≤14 Bytes ASCII or none</td>
</tr>
<tr>
	<th rowspan="2">获取仪器版本号</td>
	<td>电脑</td>
	<td>0x03</td>
	<td>----</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x03</td>
	<td>≤14 Bytes ASCII or none</td>
</tr>
<tr>
	<th rowspan="2">获取传输模式</td>
	<td>电脑</td>
	<td>0x04</td>
	<td>----</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x04</td>
	<td>1 Byte or none</td>
</tr>
<tr>
	<th rowspan="2">读写当前时间</td>
	<td>电脑</td>
	<td>0x05</td>
	<td>6 Bytes or none</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x05</td>
	<td>6 Bytes or none</td>
</tr>
<tr>
	<th rowspan="2">读写校准地址</td>
	<td>电脑</td>
	<td>0x06</td>
	<td>6 Bytes or none</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x06</td>
	<td>6 Bytes or none</td>
</tr>
<tr>
	<th rowspan="2">上次校准时间</td>
	<td>电脑</td>
	<td>0x07</td>
	<td>----</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x07</td>
	<td>6 Bytes or none</td>
</tr>
<tr>
	<th rowspan="2">引导程序版本号</td>
	<td>电脑</td>
	<td>0x08</td>
	<td>----</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x08</td>
	<td>≤14 Bytes ASCII or none</td>
</tr>
<tr>
	<th rowspan="2">当前的芯片型号</td>
	<td>电脑</td>
	<td>0x09</td>
	<td>----</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x09</td>
	<td>≤14 Bytes ASCII or none</td>
</tr>
<tr>
	<th rowspan="2">PCB版本号</td>
	<td>电脑</td>
	<td>0x0A</td>
	<td>----</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x0A</td>
	<td>≤14 Bytes ASCII or none</td>
</tr>
<tr>
	<th rowspan="2">Boot校验密码（可选）</td>
	<td>电脑</td>
	<td>0x0B</td>
	<td>----</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x0B</td>
	<td>≤14 Bytes ASCII or none</td>
</tr>
<tr>
	<th rowspan="2">测试通道 I</td>
	<td>电脑</td>
	<td>0x40</td>
	<td>----</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x40</td>
	<td>≤14 Bytes ASCII or none</td>
</tr>
<tr>
	<th rowspan="6">无线版系统更新</th>
	<th rowspan="2">获取仪器升级准备状态</td>
	<td>电脑</td>
	<td>0x55</td>
	<td>----</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x55</td>
	<td>1 Byte error code or none</td>
</tr>
<tr>
	<th rowspan="2">发送升级文件长度</td>
	<td>电脑</td>
	<td>0x56</td>
	<td>4 Bytes file length</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x56</td>
	<td>1 Byte error code or none</td>
</tr>
<tr>
	<th rowspan="2">发送升级文件</td>
	<td>电脑</td>
	<td>0x57</td>
	<td>12 Bytes data</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x57</td>
	<td>1 Byte error code or none</td>
</tr>
<tr>
	<th rowspan="8">无线版数据传输</th>
	<th rowspan="2">获取实时数据</td>
	<td>电脑</td>
	<td>0x58</td>
	<td>SN</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x58</td>
	<td>SN + wave(1 Byte) + spo2 + bpm + bar</td>
</tr>
<tr>
	<th rowspan="2">获取历史数据的时间长度</td>
	<td>电脑</td>
	<td>0x59</td>
	<td>----</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x59</td>
	<td>Total + info.(11 Bytes)</td>
</tr>
<tr>
	<th rowspan="2">获取历史数据</td>
	<td>电脑</td>
	<td>0x5A</td>
	<td>SN + item</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x5A</td>
	<td>SN + history data(12 Bytes)</td>
</tr>
<tr>
	<th rowspan="2">停止数据传输</td>
	<td>电脑</td>
	<td>0x5B</td>
	<td>----</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x5B</td>
	<td>----</td>
</tr>
<tr>
	<th rowspan="6">有线版系统更新</th>
	<th rowspan="2">获取仪器升级准备状态</td>
	<td>电脑</td>
	<td>0x55</td>
	<td>----</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x55</td>
	<td>1 Byte error code or none</td>
</tr>
<tr>
	<th rowspan="2">发送升级文件长度</td>
	<td>电脑</td>
	<td>0x56</td>
	<td>4 Bytes file length</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x56</td>
	<td>1 Byte error code or none</td>
</tr>
<tr>
	<th rowspan="2">发送升级文件</td>
	<td>电脑</td>
	<td>0x57</td>
	<td>64 Bytes data</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x57</td>
	<td>1 Byte error code or none</td>
</tr>
<tr>
	<th rowspan="8">有线版数据传输</th>
	<th rowspan="2">获取实时数据</td>
	<td>电脑</td>
	<td>0x58</td>
	<td>SN</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x58</td>
	<td>SN + wave(1 Byte) + spo2 + bpm + bar</td>
</tr>
<tr>
	<th rowspan="2">获取历史数据的时间长度</td>
	<td>电脑</td>
	<td>0x59</td>
	<td>----</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x59</td>
	<td>Total + info.(11 Bytes)</td>
</tr>
<tr>
	<th rowspan="2">获取历史数据</td>
	<td>电脑</td>
	<td>0x5A</td>
	<td>SN + item</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x5A</td>
	<td>SN + history data(64 Bytes)</td>
</tr>
<tr>
	<th rowspan="2">停止数据传输</td>
	<td>电脑</td>
	<td>0x5B</td>
	<td>----</td>
</tr>
<tr>
	<td>单片机</td>
	<td>0x5B</td>
	<td>----</td>
</tr>
</tbody></table>

- **备注**

(1) **SN**代表传输实时数据或历史数据时，每一帧的序号。序号的取值范围是0到FF，下一帧的序号与上一帧的序号差1或FF。

(2)	**Total**代表传输目录列表时，目录列表的总条数。

(3)	**item**代表传输历史数据时，指定从哪一条数据开始传输，item指的是具体的条目（从0算起）

(4)	目录列表的格式如下：序号（1 Byte） + 年（1 Byte） + 月（1 Byte） + 日（1 Byte） + 时（1 Byte） + 分（1 Byte） + 秒（1 Byte）+ 长度（4 Bytes）

(5)	原有格式拆分成12或64 Bytes。**历史记录原有格式如下：**
<table><tbody>
<tr>
	<td><B>准备发送标志</B></td>
    <td><B>文件头信息</B></td>
    <td><B>文件1</B></td>
	<td><B>……</B></td>
	<td><B>文件n</B></td>
	<td><B>传送结束标志</B></td>
</tr>
<tr>
	<td>10 Bytes of 0x00</td>
	<td>见表：文件头信息格式</td>
	<th colspan="3">见表：文件1至n格式</th>
	<td>10 Bytes of 0xFC</td>
</tr>
</tbody></table>

**文件头信息格式：**
<table><tbody>
<tr>
	<td><B>文件总长度</B></td>
    <td><B>采样率</B></td>
    <td><B>结束标志</B></td>
</tr>
<tr>
	<td>8 Bytes in big-endian</td>
	<td>0x00:2秒<br>
		0x01:4秒<br>
		0x02:</td>
	<td>10 Bytes of 0xFF</td>
</tr>
</tbody></table>

**文件1至n格式**
<table><tbody>
<tr>
	<td><B>文件目录信息</B></td>
    <td><B>数据信息</B></td>
    <td><B>结束标志</B></td>
</tr>
<tr>
	<td>见表：文件目录信息</td>
	<td>见表：数据信息</td>
	<td>10 Bytes of 0xFF</td>
</tr>
</tbody></table>

**文件目录信息**
<table><tbody>
<tr>
	<td><B>文件序号</B></td>
    <td><B>文件长度</B></td>
    <td><B>记录头</B></td>
</tr>
<tr>
	<td>1 Byte</td>
	<td>4 Bytes</td>
	<td>6 Bytes(YMDHMS)</td>
</tr>
</tbody></table>

**数据信息**
<table><tbody>
<tr>
	<td><B>报警上下限</B></td>
    <td><B>血氧值</B></td>
    <td><B>脉率值</B></td>
	<td><B>加速度传感器</B></td>
	<td><B>预留</B></td>
</tr>
<tr>
	<td>见表：报警上下限</td>
	<td>见表：血氧值</td>
	<td>见表：脉率值</td>
	<td>2 Bytes</td>
	<td>2 Bytes</td>
</tr>
</tbody></table>

**报警上下限**
<table><tbody>
<tr>
	<td><B>帧头</B></td>
    <td><B>血氧上限</B></td>
    <td><B>血氧下限</B></td>
	<td><B>脉率上限</B></td>
	<td><B>脉率下限</B></td>
</tr>
<tr>
	<td>0xfd,……0xfd</td>
	<td>1 Byte</td>
	<td>1 Byte</td>
	<td>1 Byte</td>
	<td>1 Byte</td>
</tr>
</tbody></table>

**血氧值**
<table><tbody>
<tr>
	<td><B>BIT7</B></td>
    <td><B>BIT6</B></td>
    <td><B>BIT5</B></td>
	<td><B>BIT4</B></td>
	<td><B>BIT3</B></td>
	<td><B>BIT2</B></td>
	<td><B>BIT1</B></td>
	<td><B>BIT0</B></td>
</tr>
<tr>
	<td>P8</td>
	<td>S6</td>
	<td>S5</td>
	<td>S4</td>
	<td>S3</td>
	<td>S2</td>
	<td>S1</td>
	<td>S0</td>
</tr>
</tbody></table>
> P8代表脉率第8位，
> S0至S6代表血氧的0到6位

**脉率值**
<table><tbody>
<tr>
	<td><B>BIT7</B></td>
    <td><B>BIT6</B></td>
    <td><B>BIT5</B></td>
	<td><B>BIT4</B></td>
	<td><B>BIT3</B></td>
	<td><B>BIT2</B></td>
	<td><B>BIT1</B></td>
	<td><B>BIT0</B></td>
</tr>
<tr>
	<td>P7</td>
	<td>P6</td>
	<td>P5</td>
	<td>P4</td>
	<td>P3</td>
	<td>P2</td>
	<td>P1</td>
	<td>P0</td>
</tr>
</tbody></table>
> P0至P7代表脉率的0到7位

(6)	默认传输模式为无线传输，此时不需要数据。当数据为0时为有线传输，其他数值保留。

(7)	读取时间时，不需要数据。修改时间时，数据为年（1 Byte） + 月（1 Byte） + 日（1 Byte） + 时（1 Byte） + 分（1 Byte） + 秒（1 Byte）

(8)	读取或修改时间数据均为年（1 Byte） + 月（1 Byte） + 日（1 Byte） + 时（1 Byte） + 分（1 Byte） + 秒（1 Byte）。如果不能进行时间操作，则为空的数据

(9) 测试通道 I，电脑发送命令，则单片机开始传输数据；再发一次命令，则单片机停止传输数据。
