## Three-way handshake
一个虚拟的链接的建立  是通过三次握手 来实现的 

*SYN: 握手信号* Synchronous
*ACK: 确认标志 

SYN/ACK 包: 确认包  仅仅是 SYN 和 ACK 标记为1 的 TCP 包

** 第一次握手:     **
1. 客户端  发一个 SYN=1 ACK=0 的TCP包          表示:  请求进行连接.

	只是请求/试探/询问是否可以连接服务器,服务器同意连的话 
	还是要客户端再确认一次(也就是第三次握手)才正式连接. 

** 第二次握手:    **
2.  服务器收到请求并允许进行连接的话  

	发一个 SYN=1  ACK=1  的 TCP 包给客户端  
	表示: 可以连接了 并 要求客户端返回一个确认数据包 确认进行连接 
	(有可能 客户端只是问问能不能链接)

** 第三次握手:   **
3. 客户端  发一个SYN=0，ACK=1的数据包给服务器，告诉服务器我确实要建立连接 而不是耍你… 正式连接成功
	 

	连接成功以后: TCP 的每个包 都会设置 ACK 位
	这就是连接跟踪 很重要的原因了  
	没有跟踪的话防火墙无法判断 收到的 ACK 包是不是属于一个已经建立的链接. 
	 

	在客户机和服务器之间建立正常的TCP网络连接时，
	首先 客户端发出一个包含SYN标志的数据包
	然后 服务器 返回 SYN+ACK的应答包  表示接收到了这个消息，
	最后 客户机再返回一个ACK确认包响应。
	这样在客户机和服务器之间才能建立起可靠的TCP连接，数据才可以在客户机和服务器之间传递。
	当服务器发送应答包后 没收到确认包 服务器就会进入等待直到超时
	等待期间 这些半链接的客户端都保存在一个有限的缓存列表中 
	如果有大量的 syn 包发给服务器 而且又不回应服务器的话 会造成 tcp 资源迅速耗尽  直到服务器系统崩溃 



	wireshark  TCP 握手 实测:
	显示过滤里 设置  tcp.stream eq 5  
	然后打开一个网站   wireshark 里就能 看到3个 数据了  这就是三次握手包

