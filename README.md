sequenceDiagram
    autonumber
    actor User as 实验员
    participant RDS as "RDS (调度系统)"
    participant Board as "板子 (平板屏端)"
    participant PLC as "PLC (车厢门控)"

    Note over User, PLC: 📍 阶段一：小车到达与身份验证
    RDS->>Board: 发送【到达站点】信号
    Note over Board: 唤醒并开启人脸识别
    User->>Board: 实验员正对屏幕进行人脸识别
    Note over Board: 特征比对 (匹配成功)
    Board->>PLC: 发送【开门】指令
    Note over PLC: 执行物理开门动作

    Note over User, PLC: 📦 阶段二：取物与物理状态反馈
    User->>PLC: 拿取物品后，手动将门关上
    PLC->>Board: 发送【门关到位】信号
    Note over Board: 锁定系统，暂停人脸识别

    Note over User, PLC: 🚀 阶段三：选择目的地与发车
    Note over Board: 屏幕弹出/激活【选择下一站】界面
    User->>Board: 在屏幕上点击选择下一站点
    Board->>RDS: 发送【前往目标站点】指令
    Note over RDS: 接收指令，控制AGV小车驶离当前站
