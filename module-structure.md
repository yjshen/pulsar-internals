# Pulsar 模块功能简述

- buildtools

  Pulsar 基于 TestNG 编写测试用例，并采用 Maven surefire plugin 执行测试。
  buildtools 模块实现了 TestListener 和 AnnotationTransformer 用以定义整个 Pulsar 项目的测试执行行为：打印测试开始、结束，打印超时测试的threadDump，指定测试超时时间等。

- managed-ledger

  ManagedLedger 是构建于 BK ledger 上的，用以表示一个 topic 的存储层抽象。它表示了一个单写者的追加流，同时其上有多个 cursor 消费到这个流不同位置。

- tiered-storage

  tiered storage 是 Pulsar 中负责将 topic backlog 从 BK 中移出，存入廉价存储的模块，支持 S3、Google Cloud Storage 和 HDFS。

- pulsar-common

  通用的数据、工具类。

- pulsar-broker-common

  Broker 中认证与授权相关的功能。

- pulsar-broker

  Broker 是 Pulsar 的无状态服务组件，其主要功能是执行另外两个组件：

  - An HTTP server 向外暴露 REST API，提供 admin api 和 producer、consumer 需要的 topic lookup。
  - A dispatcher —— 一个异步的 TCP server，采用 pulsar 自定义的[二进制协议](https://pulsar.apache.org/docs/en/develop-binary-protocol/)，负责所有的数据传输。


- pulsar-client， pulsar-client-admin， pulsar-client-tools

  Pulsar Java client，admin client 及对应的命令行工具

- pulsar-websocket

  基于 Websocket 与 Pulsar 交互的方式，完成与 client 库相似的功能。WebSocket 能力参见 [Pulsar client matrix](https://github.com/apache/pulsar/wiki/Client-Features-Matrix)。Websocket服务可以在 broker 中开启，或者作为一个单独的组件。

- pulsar-proxy

  Client 可以与 broker 直连，或者通过 proxy 做网关，在使用 proxy 情况下，所有客户端连接都会流经 proxy。

- pulsar-discovery-service

  维护可用 broker 列表，并以循环方式将请求重定向到一个 broker 上。

- pulsar-zookeeper

  通过 AspectJ 的方式将 ZooKeeper 的一些参数暴露给 prometheus。

- pulsar-zookeeper-utils

  ZooKeeper 中存储数据的 in-memory cache。

- pulsar-testclient

  命令行工具 pulsar-perf 的实现，用来做 broker 性能测试。

- dashboard

  Dashboard 是用来监控 Pulsar instance 运行状况的 web 应用，已经不再更新，请采用 [pulsar manager](https://github.com/apache/pulsar-manager) 替代。

- pulsar-transaction

  Pulsar 的事务实现。

- pulsar-sql, pulsar-flink, pulsar-spark

  Pulsar 的分析引擎 connector。允许 Presto、Flink、Spark 读写 Pulsar。

- pulsar-functions

  Pulsar 的 Serverless 计算的实现。

- pulsar-io

  基于 Pulsar function 的，Pulsar 与外部系统进行交互的模块。

- distribution

  Pulsar 发布包构建。

- docker

  Pulsar 相关的 docker image 构建。

- tests

  Pulsar 兼容性测试及集成测试。

- pulsar-metadata (WIP)

  在 Pulsar 中支持可插拔 Metadata store。[PIP-45](https://github.com/apache/pulsar/wiki/PIP-45%3A-Pluggable-metadata-interface) 将元数据接口抽象出来，允许用户将元数据存储在 ZK 以外的位置。
