# Sip协议（rfc3261）-  学习笔记

[TOC]

## 一、SIP协议介绍

1. 会话：参与者之间的数据交换。

2. 通讯媒介：文本、多媒体、音频、视频

3. SIP允许创建Network hosts（代理服务器）。

   代理服务器功能：用户终端注册、发出会话邀请、发出其他请求。

4. SIP特点：轻型、多用途、独立运作于通讯协议之下、不依赖建立的会话类型。

5. SIP功能：创建、修改、终止会话。

## 二、SIP协议功能概况

1. SIP是一个**应用层的控制协议**

2. SIP可以建立、修改、终止多媒体会话（会议）。

3. SIP可以邀请参加已经存在的会话。

   媒体可以在一个已经存在的会话中方便的增加或者删除。

4. SIP透明地支持名字映射和重定向服务。

   可以用于支持个人移动业务。用户可以使用一个唯一的外部标志，而不用关心实际地点。

5. SIP在建立和维持、终止多媒体会话协议上，支持五个方面：

   1. 用户定位：检查终端用户的位置，用于通信
   2. 用户有效性：检查用户参与会话的意愿程度
   3. 用户能力：检查媒体和媒体参数
   4. 建立会话："ringing"，简历会话参数在呼叫方和被叫方
   5. 会话管理：发送、终止会话，修改会话参数，激活服务。

6. SIP不是一个垂直的通讯系统，类似一个部件。可以用作其他IETF协议的一部分，用来构造完整的多媒体架构。

7. SIP本身不提供服务，但是提供了一个基础，可以用来实现不同的服务。

8. SIP不提供会议控制服务，一般通过**建立其他的会议控制协议**来发起一个会议。SIP可以管理参与会议各方的会话，所以会议可以**跨异构的网络**。SIP不提供任何形式的**网络资源预留管理**。

9. SIP提供了一套安全服务：

   1. 防止拒绝服务
   2. 认证服务（用户到用户，代理到用户）
   3. 完整性保证
   4. 加密和隐私服务

10. SIP可以基于IPv4，也可以基于IPv6。

## 三、术语

1. 必须
2. 不允许
3. 要求
4. 可以 - 不可以
5. 应该 - 不应该
6. 建议 - 不建议
7. 可能
8. 可选

- **根据 BCP14,RFC 2119[2]的规范描述SIP 实现需要的不同层次**

## 四、实施概览

1. 

## 五、协议的结构



## 六、协议的定义

1. Address-of-Record（AOR）: 记录地址
2. Back-to-Back UserAgent（B2BUA）: 背对背的用户代理。他需要维持对话状态，并且参与已经建立的对话中的每一个请求。
3. Call:呼叫。
4. Call Leg:呼叫的别名。
5. Call Stateful:代理服务器保存对话状态，代理服务器就是请求有状态的。请求有状态那么一定事务有状态，但是事务有状态不一定是请求有状态。
6. Client:客户端。发出SIP请求和接收SIP应答。用户代理客户端（UAC）和代理服务器（UAS）都是客户端。
7. Conference:会议，一个包含多个参与方的多媒体会话。
8. Core:核心，定义了SIP实体的特定类别。
9. Dialog:对话，指一段时间的两个UA之间的端到端的SIP关系。
10. Downstream: 它是事务中的消息传递方向，特指从 UAC 到 UAS 的请求流的方向。
11. Final Response:终结响应。
12. Header:头域，用来描述SIP消息信息的部分，由一堆头域字段组成。
13. Header Field：头域字段。一个头域字段可以由多个头域字段行组成。一个头域字段由一个头域名和（零个或多个）头域值组成。多个头域值’,’分割。
14. Header Field Value：头域值。一个头域字段可以有0个或多个头域值。
15. Home Domain:宿主机，提供SIP服务的主机，一般指在登记服务中指明记录地址URI的主机。
16. Informational Response：提示应答。
17. Initiator, Calling Party, Caller：用INVITE初始一个会话的一方。
18. Invitation：INVITE请求。
19. Invitee, Invited User, Called Party, Callee:被叫方。收到INVITE请求的一方。
20. Location Service：定位服务。确定被叫方可能的位置使用。它包含一张AOR（记录地址）表，可能有0或多个记录，可通过多种渠道添加和删除，本规范用 REGISTER 来更新绑定表。
21. Loop:环路。请求第二次来到同一个代理服务器。
22. Loose Routing：松散路由。
23. Message：消息，SIP元素之间传递的协议数据。
24. Method：方法，请求处理的功能。
25. Outbound Proxy：对外代理服务器，一个代理服务器收到用户的请求。通常一个UA会手工配置一个对外代理服务器。
26. Parallel Search：并行搜索，代理服务器会向多个**用户可能存在的地方**发起请求，并等待应答，但是不会的等待上一个应答，而是直接一个接一个的发起下一个搜索请求。
27. Provisional Response：临时应答。服务器用来标记自己正在处理的应答。
28. Proxy, Proxy Server：代理、代理服务器。既是客户端，也是服务端，提供请求的转发服务。
29. Recursion：回路、递归。
30. Redirect Server: 重定向服务器。一个重定向服务器是一个产生 3xx 应答的UAS 服务器，用于指示客户端连接到别的 URI。
31. Registrar：登记服务器，一个接收 REGISTER 请求的服务器。它将请求信息放到定位服务器中，方便定位服务器查找位置信息。
32. Regular Transaction: 常规事务。凡不包含 INVITE,ACK(*Ack*nowledge character，确认字符）,或者 CANCEL 方法的事务就是常规事务。
33. Request: 请求。 一个由客户端发到服务端得 SIP 信息，用于执行特定得功能。
34. Response：应答。用来响应从客户端发往服务端的请求处理的情况。
35. Ringback: 回铃音，信号音，给呼叫方得一个信号表示被叫方正在振铃（Ringing）。
36. Route Set: 路由集。路由集是一个顺序的 SIP 或SIPS URI。这些 URI 描
    述了传递一个请求所必须经历的代理列表。路由集可以是自适应得，也可以是依赖配置得到。
37. Server：服务器，一个接收请求、处理请求并发送回应的地方。例：代理服务器、用户代理服务器、重定向服务器、登记服务器。
38. Sequential Search：顺序查找。
39. Session：会话。
40. SIP 事务：指客户端和服务端的事件。
41. Spiral：回溯。同一个请求第二次访问同一个路由器，但是请求的目的地址变成另一个用户。导致这样现象的原因是**呼叫转发**。
42. Stateful Proxy:有状态的代理服务器。维持客户端和服务端的事务状态机。
43. Stateless Proxy：无状态的代理服务器。不维持客户端和服务端的事务状态机，直接转发收到的请求和响应。
44. Target Refresh Request: 目标刷新请求，用来更改对话目标的请求。
45. Transaction User(TU):事务用户。
46. Upstream: 上行流。指用户代理服务器到用户代理客户端的消息流方向。
47. URL-encoded：编码字符。
48. User Agent Client(UAC):用户代理客户端。
49. UAC Core: UAC 核心。在 transaction（事务）和 transport （传输）层之上得 UAC 实现的功能集合。
50. User Agent Server(UAS): 用户代理服务器。
51. UAS Core：UAS 核心。在 transaction 和 transport 层之上的 UAS 实现的功能集合。
52. User Agent（UA）：用户代理。一个逻辑实体的概念，包含 UAC 和 UAS。例如，当发出一个初始化 INVITE 请求的时候，UA 作为UAC 初始化一个呼叫动作，当从被叫方接收到一个 BYE 请求的时候，UA 作为UAS 响应。

## 七、SIP消息

1. SIP协议是一个基于文本的协议，使用UTF-8字符集。
2. 一个SIP消息，既可以是一个请求，也可以是一个应答。
3. 消息都基于 RFC2822 格式。
4. 消息 = 起始行 + 包头 + 消息正文
5. 起始行 = 请求行/状态行



### 		7.1请求

1. Request-Line = Method SP Reuqest-URI SP SIP-Version
2. SP：空格，Space
3. CRFL只用作行结束标志，不允许CR或LF单独出现在其他地方。
4. Method的六个方法：
   - REGISTER：用于登记联系信息
   - INVITE、ACK、CANCEL：用于建立会话
   - BYE：用于结束会话
   - OPTIONS：用于查询服务器负载（是否支持某个选项）
5. Request-URI：是一个SIP或者SIPS-URI，或者是一个通用的URI。并且禁止包含空白字符或者控制字符，禁止用<>括上。
   - SIP-URI：  sip:bob.smith@nokia.com
   - SIPS-URI：sips:bob.smith@nokia.com
   - SIPS使用TLS作为安全传输协议，要求在传输SIP消息之前先建立TLS连接。
6.  SIP元素支持SIP和SIPS之外规定的Request-URIs。SIP元素可以用ENUM服务器（类似DNS服务器）进行他们之间的转换，比如说把TEL-URI转换成SIP-URI。
7. SIP-Version：请求和应答都应该包含当前使用的SIP版本（例：SIP/2.0），SIP版本串大小写不敏感，但实际使用必须发送大写字母。

### 7.2应答

1. 应答和请求的区别：START-LINE中是否包含STATUS-LINE。
2. status-line = SIP-VERSION SP STATUS-CODE SP Reason-Phrase CRLF
3. Status-Code是一个3位的数字，用来标志处理请求的结果。
4. Reason-Phrase是一个简短的Status-Code的说明。
5. Status-Code方便程序处理，Reason-Phrase是为了显示给用户阅读。
6. status-code的第一个数字代表应答类型，接下来两个数字不做区分。
7. SIP/2.0 允许6类应答类型：
   - 1xx：临时应答，请求已接收，正在处理这个请求。
   - 2xx：成功处理，请求已经成功接收，并正确处理该请求。
   - 3xx：重定向，本请求转发到其他服务器进行处理。
   - 4xx：客户端错误，请求包含错误格式，或者该服务器无法完成
   - 5xx：服务器错误，服务器无法处理该显然合法的请求。
   - 6xx：全局错误，请求无法被任何服务器处理。

### 7.3头域

1. header = "header-name" HCOLON header-value *(COMMA header-value)
2. 头域格式（field-name:field-value）
3. 消息头中，允许冒号的左右有任意个空格，但是建议：域名和冒号之间**无空格**，冒号和值之间使用**单个空格**
4. 头域可以扩展成**多行**，多行之间的SP或者TAB将被识别成单个空格
5. 不同域名之间的相关顺序没有什么意义，建议：**与路由相关的域**放在消息的最前面，可以提高处理速度。
6. 



## 十五、结束一个会话

1. 初始化的INVITE产生了非2XX的应答，即终结了本次请求创建的所有会话。
2. 2XX应答代表成功处理请求，即请求已成功接收并且正确处理。
3. BYE用于结束会话，当对话中任何一方收到一个BYE，则所有与该对话相关的会话都应该终止。
4. UA（用户代理）禁止在对话外发送BYE请求。
5. **呼叫方**可以在早期对话中发起BYE请求，即对话还未完全建立的时候。
6. **被呼叫方**只能在建立好的对话中发起BYE请求。
7. 被呼叫方的UA收到对应2XX应答的ACK是**对话完全建立的标志**。







## 篇外

### SIP传输协议的选择

1. SIP支持多种传输协议

2. 定义传输协议，有两种方法：显式、隐式

   

3. 显式：

   ​		在URI描述中显示说明：transport=tcp 或者  transport=sctp  或者  transport=udp。

   ​		一般对于transport=tls来说，应该使用SIPS-URI方案，transport=udp是非标准的。

   

4. 隐式：

   1. 如果URI中包含**数字IP地址**，那么对于 SIP-URI 使用 UDP , SIPS-URI    使用 TCP 。
   2. 如果URI中**没有包含**数字IP地址，只包含端口号，那么对于 SIP-URI 还是使用 UDP , SIPS-URI  还是使用 TCP 。
   3. 待补充...



### Cseq的作用

​		用于区分INVITE请求的版本。若是一个新的INVITE请求，则Cseq++，否则若是重传，还是旧的INVITE请求，则Cseq不变。

### Tag的作用

​		Call-id、From（tag）、To （tag）三个值相同代表是同一个会话。tag的作用就是用来判断该sip协议归属于哪个会话。



## sip消息内容示例

		SUBSCRIBE sip:001_qhcrm@192.168.100.86:5080 SIP/2.0
		Via: SIP/2.0/UDP 192.168.100.86:63858;branch=z9hG4bK-d87543-5a546228b5146c36-1--d87543-;rport
		Max-Forwards: 70
		Contact: <sip:001_qhcrm@192.168.100.86:63858>
		To: "001_qhcrm"<sip:001_qhcrm@192.168.100.86:5080>
		From: "001_qhcrm"<sip:001_qhcrm@192.168.100.86:5080>;tag=bf41f319
		Call-ID: MzEzODViZjZhZWQxZjFiN2RkZDBlYzk2YTg2NzBjNTM.
		CSeq: 1 SUBSCRIBE
		Expires: 300
		Allow: INVITE, ACK, CANCEL, OPTIONS, BYE, REFER, NOTIFY, MESSAGE, SUBSCRIBE, INFO
		User-Agent: eyeBeam release 1011d stamp 40820
		Event: message-summary
		Content-Length: 0
		
		/*
			branch作为事务的ID,用来保证事务的唯一性。
			via也包含了应答送回的地址，即:192.168.100.86:63858
			From代表发起请求方的标记，其中，刚开始的"001_qhcrm"代表的是逻辑名，sip:后面那一串代表的是发起请求		方的主机名，可以通过对From的检查，来选择规则对请求进行处理，例如：自动拒绝某人的呼叫。
			Allow代表代理服务器所支持的 消息请求类型列表。
		*/
	
		INVITE sip:13225958632@192.168.100.86:5080 SIP/2.0
		Via: SIP/2.0/UDP 192.168.100.86:63858;branch=z9hG4bK-d87543-ec4d8c071a25652a-1--d87543-;rport
		Max-Forwards: 70
		Contact: <sip:001_qhcrm@192.168.100.86:63858>
		To: "13225958632"<sip:13225958632@192.168.100.86:5080>
		From: "001_qhcrm"<sip:001_qhcrm@192.168.100.86:5080>;tag=6652b135
		Call-ID: OTdkNjBhNGQ1NWRjY2RkMThkY2JjNDE1Y2YyN2ZjOGY.
		CSeq: 1 INVITE
		Allow: INVITE, ACK, CANCEL, OPTIONS, BYE, REFER, NOTIFY, MESSAGE, SUBSCRIBE, INFO
		Content-Type: application/sdp
		User-Agent: eyeBeam release 1011d stamp 40820
		Content-Length: 443
	
		v=0
		o=- 3 2 IN IP4 192.168.100.86
		s=CounterPath eyeBeam 1.5
		c=IN IP4 192.168.100.86
		t=0 0
		m=audio 18814 RTP/AVP 0 8 18 101
		a=alt:1 3 : ovaLulGu qTNNi6t2 192.168.93.1 18814
		a=alt:2 2 : slIWCCb2 2A5hIsX1 192.168.211.1 18814
		a=alt:3 1 : mjtbNYbs 5gc58cRi 192.168.100.86 18814
		a=fmtp:18 annexb=no
		a=fmtp:101 0-15
		a=rtpmap:18 G729/8000
		a=rtpmap:101 telephone-event/8000
		a=sendrecv
		a=x-rtp-session-id:ADA7E815F3B04299BBD7F277E70D24A2
	
		CANCEL sip:13225958632@192.168.100.86:5080 SIP/2.0
		Via: SIP/2.0/UDP 192.168.100.86:63858;branch=z9hG4bK-d87543-ec4d8c071a25652a-1--d87543-;rport
	    To: "13225958632"<sip:13225958632@192.168.100.86:5080>
	    From: "001_qhcrm"<sip:001_qhcrm@192.168.100.86:5080>;tag=6652b135
	    Call-ID: OTdkNjBhNGQ1NWRjY2RkMThkY2JjNDE1Y2YyN2ZjOGY.
	    CSeq: 1 CANCEL
	    User-Agent: eyeBeam release 1011d stamp 40820
	    Content-Length: 0



