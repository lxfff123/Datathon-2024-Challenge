# AGV Camera Server

## 项目简介
AGV视觉智能监控服务器，基于YOLO11行人检测 + Flask + Gevent + MQTT实现。
用于接收AGV小车摄像头视频流，实时检测行人，自动下发报警指令，实现AGV视觉安全防护。

## 核心功能
- 接收摄像头视频流（ImageZMQ）
- 实时AI行人检测（YOLO11，支持GPU加速）
- ROI区域智能检测，过滤无效目标
- 检测到行人后自动通过MQTT发送报警指令
- 双路自动录像（全段录像 + 仅行人录像）
- 按小时自动切分、自动归档
- Web页面实时查看监控画面
- MQTT设备状态同步

## 端口配置
- Web 监控界面：5016
- 视频流接收：5555
- MQTT 通信：1884

## 录像保存路径
E:\records\[设备ID]\[日期]\
E:\records\[设备ID]\[日期]\person\

## 启动命令
python server_recordzzb.py

## MQTT 协议
订阅：amb/+/status
推送报警：amb/{设备ID}/cmd
报警内容：ALERT