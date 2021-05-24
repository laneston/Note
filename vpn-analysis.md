# VPN概述

vpn：（Virtual Private Network）是指依靠Internet服务提供商ISP（Internet Service Provider）和网络服务提供商NSP（Network Service Provider）在公共网络中建立的虚拟专用通信网络。

- 租赁（建设时间长、价格昂贵、难于管理）
- 传统专网（依赖专用介质，速率慢，部署复杂）
- 虚拟专用网（灵活性、安全性、经济性、扩展性）


## vpn基本特征

专用（private）：VPN与底层承载网络之间保持资源独立，即VPN资源不被网络中非该VPN的用户所使用，且VPN能够提供足够的安全保证，确保VPN内部信息不受外部侵扰。 

虚拟（virtual）：逻辑上的专网。


## vpn的优势

安全、廉价、支持移动业务、可扩展性


## vpn的原理

利用隧道技术，把VPN报文封装在隧道中，利用VPN骨干网建立专用数据传输通道，实现报文的透明传输。隧道技术使用一种协议封装另外一种协议报文，而封装协议本身也可以被其他封装协议所封装或承载（疯狂套娃）。


## vpn的分类

按照组网型分类： 

1. 网关与网关： 数据流在公网的vpn节点之间的转发，数据包的转发实在网络层实现的，公网的每个vpn节点需要为每个vpn建立专用路由转发表，包含网络层可达性信息。为实现局域网之间互通而产生例如：ATM，Frame Relay，GRE，MPLS VPN，IPSec VPN。

2. 主机与网关： Access VPN使出差流动员工家庭办公人员和远程小办公室可以通过廉价的拨号介质接入internet，然后利用VPN和企业的内网建立私有网络连接，从而访问企业内部服务器例如：IPSec，PPTP，L2TP，L2TP over IPSec, SSLVPN。

3. 主机与主机之间按照实现层次分类：

L3VPN：三层技术：GRE VPN、ipsec VPN（网络层）——ATM、帧中继优势：能够封装各类三层流量、很好的QoS保障 

L2VPN：二层技术：点到点、二层转发协议、二层隧道协议（数据链路层）GRE——完整的VPN功能；缺乏安全性

MPLS VPN——any-to-any；需要SP接入点，缺乏安全性

ipsec VPN——省钱安全；带宽不能保障


第二节：ipsec简介1.ipsec： ipsec（internet协议安全）是一个工业标准网络安全协议，为ip网络通信提供透明的安全服务，保护TCP/IP通信免遭窃听和篡改，可以有效抵御网络攻击，同时保持易用性。透明：中间的隧道采用加密等技术对于互相通信的双方是不感知的免遭窃听和篡改：加密和保证数据的完整性抵御网络攻击：防重放 ipsec通过在ipsec对等体间建立双向安全联盟，形成一个安全互通的ipsec隧道，来实现internet上数据的安全传输2.ipsec组成部分： ipsec包括AH：验证头、ESP：封装安全载荷、IKE：因特网秘钥交换，用于保护主机与主机之间，主机与网关之间，网关与网关之间的一个或多个数据流。提供安全服务（AH、ESP）用于秘钥交换（IKE）3，ipsec特性：对等体认证，无连接的完整性、数据来源验证（哈希）防重放，机密性（加密）4.ipsec基本组件：ipsec对等体，ipsec隧道，数据封装模式（隧道模式，传输模式），安全协议（AH，ESP），安全联盟IPSec用于在协商发起方和响应方这两个端点之间提供安全的IP通信，通信的两个端点被称为IPSec对等体。其中，端点可以是网关路由器，也可以是主机。5.安全联盟：（SPI安全参数索引，目的ip地址，安全协议号）SA：是出于安全目的而建立的一个单向逻辑连接，要建立IPSec隧道的通信双方对隧道参数的约定，包括隧道两端的IP地址、隧道采用的验证方式、验证算法、验证密钥、加密算法、加密密钥、共享密钥以及生存周期等一系列参数。两种方式：（手动和ike协议协商）6.传输模式：加密点与通信点完全一致，没有新的包头 隧道模式：加密点与通信点不一致，增加新的包头






7.AH：协议号：50 只认证，提供数据来源认证，数据完整性校验和报文防重放功能。工作原理：在每一个数据包的标准ip包头后面添加一个AH包头。AH 对数据包和认证密钥进行Hash计算，接收到对方收到带有计算结果的数据包后，执行同样的Hash计算并与原计算结果比较，有任何更改则无效。ESP协议号：51 可以加密 还提供加密功能 工作原理：在一个标准的ip包头后面添加一个ESP报文头部，并在数据包后面加一个ESP尾部（ESP Tail和ESP Auth data)。与AH不同的是，ESP Auth data用于对数据提供来源认证和完整性校验，并且ESP将数据中的有效载荷进行加密后再封装到数据包中，以保证数据的机密性，但ESP没有对头部内容进行保护。8.ESP包输入处理：检查处理这个包的SA是否存在（SPI，安全协议，目的ip）检查序列号是否有效对数据包进行完整性和来源进行验证对数据包解密对数据包进行初步的有效性检验最终处理结果第三节：ike 介绍1.ike负责自动建立和维护ike SA和ipsec SA对双方进行认证交换公共密钥，产生密钥资源，管理密钥协商协议参数（封装，加密，验证）2.模式：主模式：6种报文野蛮模式：3种报文快速模式：3种报文


主模式与野蛮模式的对比：



野蛮模式适应场景：


快速模式：


快速模式交换过程图：



IKEv2所有消息都以请求-响应的方式成对出现，响应方都要对发起方发送的消息进行确认，如果在规定的时间内没有收到确认报文，发起方需要对报文进行重传处理，提高了安全性。3.版本ikev1：先建立IKE SA（双向），在建立ipsec SA （主模式，野蛮模式）——复合协议三个组件：SKEME：定义如何通过公共密钥技术（DH算法）实现密钥交换。Oakley：提供了IPSec对各种技术的支持ISAKMP：定义了消息交换的体系结构，包括两个IPSec对等体间分组形式和状态转变（定义封装格式和协商包交换的方式）ikev2：直接生成ipsec秘钥，生成ipsec SA 4.IKE安全机制身份认证、身份保护、DH（秘钥交换算法）、完善的前向安全性PFS5.身份认证的方法： 预共享秘钥（pre-shared-key）、数字证书RSA、数字信封第四节：PKI基本架构概述1.PKI（Public Key Infrastructure，公钥基础设施）是通过使用公钥技术和数字证书来提供系统信息安全服务，并负责验证数字证书持有者身份的一种体系。PKI保证了通信数据的机密性、完整性、不可否认性和认证性2.为什么用PKI？IPSec身份认证（预共享密钥方式） 配置简单。只需在总舵和分舵的网关上配置相同的密钥即可。 维护复杂。但随着分舵数量越来越多，总舵和每个分舵之间形成的对等体都要配置预共享密钥。 安全风险高。如果所有对等体都使用同一个密钥，存在安全风险。IPSec身份认证（PKI中的证书认证方式） 维护简单。随着分舵数量越来越多，只需要向CA申请证书即可。 安全风险低。不同的分舵使用不同的证书，对应的密钥也不同。3.PKI的功能：签发证书证书、密钥对的自动更新签发证书黑名单密钥备份与恢复功能加密、签名密钥的分隔密钥历史的管理证书鉴别，交叉认证4.PKI的组成证书颁发机构（CA）证书注册机构（RA）证书库密钥备份及恢复系统证书废除处理系统应用系统接口数字证书5.PKI系统一般工作流程 实体生成密钥对，并将公钥、实体信息发送给RA进行证书申请。 RA审核实体身份，将实体身份信息和公开密钥以数字签名的方式发送给CA。 CA验证数字签名，同意实体的申请，颁发证书。 RA接收CA返回的证书，发送到LDAP服务器以提供目录浏览服务，并通知实体证书发行成功。 实体获取并安装证书，利用该证书可以与其它实体使用加密、数字签名进行安全通信。 实体希望撤销自己的证书时（或者密钥泄漏、服务过期等），向CA提交申请。CA批准实体撤销证书，并更新CRL，发布到LDAP服务器。6.PKI框架两个重要角色：终端实体（EE，End Entity）：证书的最终使用者，例如总部和分支的网关。证书颁发机构（CA，Certificate Authority）：是一个权威的、可信任的第三方机构，负责证书颁发、查询以及更新等工作。7.CA证书组成版本：即使用X.509的版本，目前普遍使用的是v3版本（0x2）。序列号：该序列号在CA服务范围内唯一。签名算法：CA签名使用的算法。颁发者：CA的名称。有效期：包含有效的起、止日期，不在有效期范围的证书为无效证书。主题：证书所有者的名称。公钥信息：对外公开的公钥。扩展信息：通常包含了使用者备用名称、使用者密钥标识符等可选字段。签名：CA的签名信息，又叫CA的指纹信息。8.获取证书方法在线，离线