**TCP提供了一种字节流服务，而收发双方都不保持记录的边界，应用程序应该如何提供他们自己的记录标识呢？**

应用程序使用自己约定的规则来表示消息的边界，比如有一些使用回车+换行（"\r\n"），比如 Redis 的通信协议（RESP protocol）



**序列号**

A B 两个主机之间建立了一个 TCP 连接，A 主机发给 B 主机两个 TCP 报文，大小分别是 500 和 300，第一个报文的序列号是 200，那么 B 主机接收两个报文后，返回的确认号是（）

- A、200
- B、700
- C、800
- D、1000

答案：D，500+300+200



**TCP/IP 协议中，MSS 和 MTU 分别工作在哪一层**

参考：MSS->传输层，MTU：链路层



**在 MTU=1500 字节的以太网中，TCP 报文的最大载荷为多少字节**

参考：1500（MTU） - 20（IP 头大小） - 20（TCP 头大小）= 1460



**端口号**

小于（）的 TCP/UDP 端口号已保留与现有服务一一对应，此数字以上的端口号可自由分配？

- A、80
- B、1024
- C、8080
- D、65525

参考：B，保留端口号



**下列 TCP 端口号中不属于熟知端口号的是（）**

- A、21
- B、23
- C、80
- D、3210

参考：D，小于 1024 的端口号是熟知端口号

**关于网络端口号，以下哪个说法是正确的（）**

- A、通过 netstat 命令，可以查看进程监听端口的情况
- B、https 协议默认端口号是 8081
- C、ssh 默认端口号是 80
- D、一般认为，0-80 之间的端口号为周知端口号(Well Known Ports)

A

**TCP 协议三次握手建立一个连接，第二次握手的时候服务器所处的状态是（）**

- A、SYN_RECV
- B、ESTABLISHED
- C、SYN-SENT
- D、LAST_ACK

参考：A，收到了 SYN，发送 SYN+ACK 以后的状态



**下面关于三次握手与connect()函数的关系说法错误的是（）**

- A、客户端发送 SYN 给服务器
- B、服务器只发送 SYN 给客户端
- C、客户端收到服务器回应后发送 ACK 给服务器
- D、connect() 函数在三次握手的第二次返回

参考：B，服务端发送 SYN+ACK



**HTTP传输完成，断开进行四次挥手，第二次挥手的时候客户端所处的状态是：**

- A、CLOSE_WAIT
- B、LAST_ACK
- C、FIN_WAIT2
- D、TIME_WAIT

参考：C

**正常的 TCP 三次握手和四次挥手过程（客户端建连、断连）中，以下状态分别处于服务端和客户端描述正确的是**

- A、服务端：SYN-SEND，TIME-WAIT 客户端：SYN-RCVD，CLOSE-WAIT
- B、服务端：SYN-SEND，CLOSE-WAIT 客户端：SYN-RCVD，TIME-WAIT
- C、服务端：SYN-RCVD，CLOSE-WAIT 客户端：SYN-SEND，TIME-WAIT
- D、服务端：SYN-RCVD，TIME-WAIT 客户端：SYN-SEND，CLOSE-WAIT

参考：C，SYN-RCVD 出现在被动打开方服务端，排除A、B，TIME-WAIT 出现在主动断开方客户端，排除 D



**下列TCP连接建立过程描述正确的是：**

- A、服务端收到客户端的 SYN 包后等待 2*MSL 时间后就会进入 SYN_SENT 状态
- B、服务端收到客户端的 ACK 包后会进入 SYN_RCVD 状态
- C、当客户端处于 ESTABLISHED 状态时，服务端可能仍然处于 SYN_RCVD 状态
- D、服务端未收到客户端确认包，等待 2*MSL 时间后会直接关闭连接

参考：C，建连与 2*ML 没有关系，排除 A、D，服务端在收到 SYN 包且发出去 SYN+ACK 以后 进入 SYN_RCVD 状态，排除 B。如果客户端给服务端的 ACK 丢失，客户端进入 ESTABLISHED 状态时，服务端仍然处于 SYN_RCVD 状态。



**TCP连接关闭，可能有经历哪几种状态：**

- A、LISTEN
- B、TIME-WAIT
- C、LAST-ACK
- D、SYN-RECEIVED

参考：B，主动断开方进入 TIME-WAIT，其它几个都不是



**TCP 状态变迁中，存在 TIME_WAIT 状态，请问以下正确的描述是？**

- A、TIME_WAIT 状态可以帮助 TCP 的全双工连接可靠释放
- B、TIME_WAIT 状态是 TCP 是三次握手过程中的状态
- C、TIME_WAIT 状态是为了保证重新生成的 socket 不受之前延迟报文的影响
- D、TIME_WAIT 状态是为了让旧数据包消失在网络中

参考：B 明显错误，TIME_WAIT 不是挥手阶段的状态。A、C、D都正确



**假设 MSL 是 60s，请问系统能够初始化一个新连接然后主动关闭的最大速率是多少？（忽略1~1024区间的端口）**

- 参考：系统可用端口号的范围：65536 - 1024 = 64512，主动关闭方会保持 TIME_WAIT 时间 2*MSL = 120s，那最大的速率是：64512 / 120 = 537.6