# union  
	有疑问欢迎加群：828958110   
## 什么是union
	union是分布式的游戏服务器框架，自带认证服，逻辑服的部分实现，其中逻辑服采用Actor模型。   
## 简单，简单，再简单
	简单到1s起服
	简单到美术可以运维
	简单到逻辑就像填空题
	简单到不需要配置go路径
	简单到union虽然是分布式架构，但你连ip都不需要配置
## 编译前准备
	这版的开发环境为windows
	编译union前需要按照3个软件
	1 go
	2 python2.7
	3 redis，union自带了，目录在tools/bin Redis-x64-3.2.100.msi,安装后注意设置Path路径
## 1s编译
	运行build.bat会要求选择pb的版本，选择后即可编译出可执行文件，输入1可以直接运行可执行文件
## 1s运行
	编译出exe后，运行run.bat，按照提示操作，如果没有启动redis，会自动运行redis-server
	运行后，会要求选择服务器，请至少启动一个认证服和逻辑服，服务器会自动组网
## 1s测试
	运行test.bat 会要求按照python的pb库，选择和服务器一样的版本就行
	按照好后按照指令输入即可看到服务器返回值
## protobuf版本问题
	union支持protobuf2.5和protobuf3.6，
	开发时选择一个好版本后，直接修改build.bat，以免后续出错
	为什么要同时支持pb2.5和pb3.6呢，比如我们用unity开发了一个游戏，采用lua+protobuf2.5，现在又要移植为H5
	由于go在pb2.5和pb3.6产生的代码上的差异，union为了统一选择了pb2.5的语法
## 依赖管理
	union直接把依赖下载到本地进行管理，dep目录里面有所有go依赖
## 一切基于PB
	从数据模型开始union就基于PB，会用PB生成逻辑代码。
## 数据库
	游戏需要sql吗？
	在我做的商业游戏中，确实有用到sql的地方，但只有日志分析和gm后台使用，所以union采用redis作为主存
	redis存的数据是有pb格式和msgpack格式
	其中pb格式用于存储大且不需要被redis lua解析的数据，比如战斗回放
	默认情况redis内存存储的是msgpack格式的数据，可以被redis lua解析与操作
## 分布式下的一致性
	union保证数据一致性的方法是用redis lua作为存储过程，因为redis是单线程的   
## 微服务
	union可以非常方便的实现微服务   
	不用配置etcd，不用写任何网络相关代码，union已经集成了服务发现，断线重连等   
	同时union会自动发现负载最低的服务器   
	没有grpc，union的微服务使用纯的tcp模式，同时会像grpc一样自动生成代码，不过生成的代码集成度更高，调用就像普通函数一样方便   
## 整体目录
	union
		conf 配置
			doc 策划档配置
		deps 依赖项目
		log 日志，运行时产生
		src 源码路径
			frame 框架代码
			gmodel 全局model
			gcontrol 全局control
			proto pb产生的go代码
			idl 中间语言
				pb2 pb2代码
				pb3 pb3代码
				csv 引导代码，会根据csv内容自动生产go代码，比如错误码等
			server 服务器代码
				auth 认证服
				logic 逻辑服
				test 测试服
		tools 工具路径
			auto 自动产生代码的路径
			bin 可执行文件路径
			gencode 动态产生代码的代码
			redis redis目录
			test 测试目录
			build.py 生成服务器可执行文件
			redis.py 启动测试redis-server
		main.go 入口
		
## IDL
	IDL为union的中间语言，有pb和csv两种，union会根据idl生成一些代码
### PB规范
	由于union需要pb生成一部分代码，所以对pb有所规范
	所有的客服端交互消息在client.proto里面
	客服端发送的消息以C2S结尾，服务器回复的消息以S2C结尾
	服务器回复的消息必须包含error字段
### CSV规范

## 消息处理
	union的消息处理支持两种

## 安装python依赖，运行测试代码
	下载protobuf-matstr  https://github.com/google/protobuf
	复制python目录和src目录到tools/bin目录
	修改python目录下setup.py 在# Find the Protocol Compiler.这句下面添加protoc路径os.environ['PROTOC'] = "../protoc.exe"
	
	
## 配置文件
	服务器配置采用yaml格式

## 为什么没有代码
	仅接受商业定制，支持全球同服，千万级DAU


















