# minertunnel
MinerTunnel(矿工隧道)，最稳定的MinerProxy/矿池代理程序,支持ETH,BTC,ETC,可以轻松搭建以太坊ETH和比特币BTC代理中转矿池程序，ETH和BTC抽水不掉线, 支持TCP直接转发，也支持SSL加密和SSL解密，具有稳定性高，传输速度快，并发强等优点


使用方法
------


MinerTunnel.exe [-m proxy mode] [-p port] [-r remote address:port] [-t digital currency type] [-f feeRate] [-w wallet address] [-d remote address:port]

温馨提示:上面的参数中，其中参数-m,-p,-r是必须的，缺一不可.参数-t,-f,-w是可选的，不需要时可以不用输入

* -m，工作模式
  * 0，表示tcp2tcp模式，对tcp协议数据包直接转发到目标地址
  * 1，表示tcp2ssl模式，对tcp协议数据包经过ssl加密后转发到目标ssl服务器地址
  * 2，表示ssl2tcp模式，对ssl协议数据包经过解密后转发到目标地址
* -p，监听端口号，用来接收对方发来的数据包
* -r，目标矿池地址，地址格式为address:port，必须带上端口，其中，address可以是ip也可以是域名，port是端口号
* -t，数字货币类型，只支持ETH和BTC，是可选参数
  * 0，表示ETH矿池代理，这是默认值，不输入该参数时它的值0
  * 1，表示BTC矿池代理，如果需要搭建btc矿池代理，请必须要设置该参数值
* -t，抽水比例，以千分之一为单位，比如，该值是5，表示千分之5的抽水比例，该参数必须在使用-w参数设置了钱包地址才会生效，是可选项参数，如果不需要抽水，可以忽略此参数
* -w，钱包地址，是eth以太坊的钱包地址或者btc矿池所注册的子用户名。该参数必须在使用-t参数设置了抽水比例才会生效，是可选参数，如果不需要抽水，请忽略此参数。设置了抽水后，还可以使用参数"-d"设置抽水矿池地址
* -d，抽水矿池地址，地址格式为address:port，必须带上端口，其中，address可以是ip也可以是域名，port是端口号。是可选参数，如果不设置此参数，在开了抽水功能前提下会默认使用"-r"参数设置的地址作为抽水的矿池地址

命令行实例
------
MinerTunnel.exe -m 0 -p 61000 -r 47.243.161.95:3100

MinerTunnel.exe -m 1 -p 61000 -r 47.243.161.95:3100

MinerTunnel.exe -m 2 -p 3100 -r asia1.ethermine.org:4444

MinerTunnel.exe -m 2 -p 3100 -t 0 -r asia1.ethermine.org:4444

MinerTunnel.exe -m 2 -p 3100 -r stratum-eth.antpool.com:8008

MinerTunnel.exe -m 2 -p 3100 -r stratum-eth.antpool.com:8008 -t 1 -w usernametest -f 30 -d nyv.s.eksy.org:443

MinerTunnel.exe -m 2 -p 3100 -r asia1.ethermine.org:4444 -f 10 -w 0xaF041b55a28a4F07F106606797229374E664800b

MinerTunnel.exe -m 2 -p 3100 -r asia1.ethermine.org:4444 -f 10 -w 0xaF041b55a28a4F07F106606797229374E664800b -d asia1.ethermine.org:4444

MinerTunnel.exe -m 1 -p 62000 -t 1 -r 47.243.161.95:4100

MinerTunnel.exe -m 2 -p 4100 -t 1 -r ss.antpool.com:443



使用实例
------

假如服务器IP地址是47.243.161.95

下面是以太坊ETH矿池代理搭建详细步骤：
------

第一步：需要在本地电脑加密，本地电脑可以用用两种方式加密，一种是使用本程序加密，一种是在类似轻松矿工的软件中直接加密。下面以轻松矿工举例。

第一种加密方式：
使用本程序矿工隧道加密时，可在本地电脑使用命令：

MinerTunnel.exe -m 1 -p 61000 -r 47.243.161.95:3100 
 
该命令行表示监听本地的61000端口，并且会把该端口的挖矿数据经过ssl加密后转发到服务器47.243.161.95的3100端口，然后需要在轻松矿工中设置如下矿池地址：

127.0.0.1:61000

表示轻松矿工会把挖矿数据发到本地的61000端口

第二种加密方式：
使用轻松矿工加密时，直接在轻松矿工中设置如下矿池地址：

stratum+ssl://47.243.161.95:3100

表示轻松矿工把挖矿数据加密后发到服务器47.243.161.95的3100端口

第二步：需要在服务器解密，然后转发到矿池

使用本程序矿工隧道解密时，可以在服务器中使用命令：

MinerTunnel.exe -m 2 -p 3100 -r asia1.ethermine.org:4444

上述的asia1.ethermine.org可以改成其它矿池地址，比如:

MinerTunnel.exe -m 2 -p 3100 -r stratum-eth.antpool.com:8008

如果你需要抽水，请添加抽水参数，如下

MinerTunnel.exe -m 2 -p 3100 -r asia1.ethermine.org:4444 -f 10 -w 0xaF041b55a28a4F07F106606797229374E664800b

表示抽水比例是千分之10，抽水到钱包地址:0xaF041b55a28a4F07F106606797229374E664800b



下面是比特币BTC矿池代理搭建详细步骤：
------

第一步：在本地电脑使用矿工隧道进行加密

使用本程序矿工隧道加密时，可在本地电脑使用命令：

MinerTunnel.exe -m 1 -p 62000 -t 1 -r 47.243.161.95:4100 

该命令行比前面eth的多加了一个“-t 1”，命令行表示监听本地的62000端口，并且会把该端口接收到的挖矿数据经过ssl加密后转发到服务器47.243.161.95的4100端口

然后需要在btc矿机的控制面板中挖矿地址设置为：

stratum+tcp://192.168.0.3:62000

其中，192.168.0.3表示本地电脑在本地局域网内的ip地址，另外，矿工名设置方式不变

第二步：需要在服务器解密，然后转发到矿池

使用本程序矿工隧道解密时，可以在服务器中使用命令：

MinerTunnel.exe -m 2 -p 4100 -t 1 -r ss.antpool.com:443

表示把从端口4100收到的数据经过解密后转发到蚂蚁矿池antpool中

如果你需要抽水，请添加抽水参数，如下

MinerTunnel.exe -m 2 -p 4100 -t 1 -r ss.antpool.com:443 1 -w usernametest -f 30

该命令表示，会抽水到你在ss.antpool.com矿池注册的子账户usernametest中，抽水比例是千分之30

如果有问题，可以咨询telegram   https://t.me/MinerTunnel






