# 目录结构
├── Makefile        # 项目编译、运行、测试快捷命令
├── README.md
├── api             # rpc文件
│   └── user
│       └── v1
│           ├── user.pb.go
│           ├── user.proto
│           └── user_grpc.pb.go
├── bin
│   └── server      # 构建好的二进制文件
├── cmd
│   └── server      # 编译入口
│       ├── main.go
│       ├── wire.go
│       └── wire_gen.go
├── go.mod
├── go.sum
├── internal
│   ├── biz         # 业务组装层
│   │   └── user.go
│   ├── data        # 数据层
│   │   └── user.go
│   ├── pkg         # 公共库
│   │   └── grpc    # gRPC server封装
│   │       └── server.go
│   └── service     # API实现层
│       └── user.go
└── test            # 测试服务API
    └── user.go
    
    
视频要再看一遍，之后把代码补上。