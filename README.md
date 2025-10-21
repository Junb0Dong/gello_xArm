# 双臂遥操部署
## 硬件设置
**左臂：**
- 主臂（引导臂）:usb-FTDI_USB__-__Serial_Converter_FTAD3ZBL-if00-port0 USB1
- 从臂（xArm）: 192.168.1.213

**右臂:**
- 主臂（引导臂）:usb-FTDI_USB__-__Serial_Converter_FTA0VTIS-if00-port0 USB0
- 从臂（xArm）: 192.168.1.209

`get_offset`运行命令示例
```bash
python scripts/gello_get_offset.py     --start-joints 0 0.318 0 1.4 0 1.4 0     --joint-signs 1 1 1 1 1 1 1     --port /dev/serial/by-id/usb-FTDI_USB__-__Serial_Converter_FTA0VTIS-if00-port0
```
## xArm双臂开发
### 问题
- 不能读取dynamixel的值
    > 重启了一下，可以读到dynamixel的电机值
- 双臂遥操时，两条臂向各自相同的goal pose运动，即使每条单臂是可以遥操的
    > 作者只针对UR开发了双臂的遥操代码，有一些hard code需要更改，例如机械臂的初始角度值
- [ ] 需要打印一个支架放置gello以免每次都需要进行offset的校准

### 改动要点
1. `run_env.py`中改变双臂的初始关节角度值
2. `gello_agent.py`中改变初始的offset