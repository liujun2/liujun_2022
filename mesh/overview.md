# 1  消费者的需求：
### 不复杂
### 易安装
### 易使用
https://rf.eefocus.com/article/id-333052

# 2 蓝牙mesh
## 组网
任何一个出厂的mesh设备是一个未配网设备（Unprovisioned Device），需要使用配网者（Provisioner）对未配网设备进行配网，使其成为mesh网络中的一个节点。要使未配网设备成为一个节点，需要配网者为其分配一个NetKey（表示该设备属于哪一个子网），一个IV Index（表示该设备是有效的），一个Unicast Address（作为该节点的唯一标识）。配网的流程其实就是配网者如何安全有效不冲突地将这些数据下发给未配网设备。

![Screen Shot 2022-10-25 at 16 24 01](https://user-images.githubusercontent.com/6103136/197722547-de2c9633-0abd-4f5c-a405-23281fd87418.png)

![Screen Shot 2022-10-25 at 16 08 38](https://user-images.githubusercontent.com/6103136/197719123-64072ed9-85df-45c4-8ece-cec62b96a943.png)


## 配网有两种方式，
### 一种是通过ADV广播的方式进行配网（PB-ADV）
### 一种是通过GATT连接的方式进行配网（PB-GATT）
