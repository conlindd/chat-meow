---
title: ChatGpt随身WiFi智能音箱之制作ChatGpt智能音箱
date: 2023-5-29 11:59:21
tags: [ChatGpt,Open Ai,随身wifi,音响]
categories: 
	- ai
	- ChatGpt
	- 随身WiFi
	- 音响
permalink: /articke/chatgpt-suishenwifi-yinxiang4.html
---

### +.前期准备看博客:

http://jiuhuai.top

### 0.前期准备

0.1插好设备线

0.2.开启USB HUB模式

```
echo host > /sys/kernel/debug/usb/ci_hdrc.0/role
```

0.3.检查PulseAudio是否正在运行并具有默认的音频输入和输出设备，请按照以下步骤操作：

 ```
   1. 打开终端窗口。
   2. 运行`pulseaudio --check`命令，以确保PulseAudio正在运行。如果PulseAudio未运行，则可以使用`pulseaudio --start`命令启动它。
   3. 运行`pacmd list-sinks`命令，以查看当前的音频输出设备。默认情况下，应该存在一个名为`alsa_output.pci-0000_00_1f.3.analog-stereo`的设备。
   4. 运行`pacmd list-sources`命令，以查看当前的音频输入设备。默认情况下，应该存在一个名为`alsa_input.pci-0000_00_1f.3.analog-stereo`的设备。
 ```

### 1.克隆项目

1.1在根目录创建文件夹

```
mkdir geren

cd geren
```

1.2克隆本项目到本地

git clone https://github.com/conlindd/chat-meow.git

### 2.配置ChatGpt Api  和百度语音识别APi

2.1在项目根目录的key.yml文件中配置百度语音识别Api

申请地址：https://developer.baidu.com/

![image-20230529104053413](https://s2.loli.net/2023/05/29/kQYD91zAxcvtmg4.png)

![image-20230529104133901](https://s2.loli.net/2023/05/29/rSTMu8WsOoCjIeF.png)

![image-20230529103851456](https://s2.loli.net/2023/05/29/DC7TJaRMusQyOoL.png)

2.2在项目根路径下的chat.py文件中配置ChatGpt Api

![image-20230529103442892](https://s2.loli.net/2023/05/29/4ReELsNWzrBAmPo.png)

### 3.部署

在克隆的项目根路径执行命令

```shell

docker run -d \
    -v /geren/chat-meow:/chat \
    -v /dev/snd:/dev/snd \
    --privileged \
    -e PULSE_SERVER=unix:/run/pulse/native \
    -e PULSE_COOKIE=/run/pulse/cookie \
    -e PULSE_SINK=alsa_output.usb-Device-1c4f_2072-00.analog-stereo \
    -e PULSE_SOURCE=alsa_input.usb-Device-1c4f_2072-00.analog-stereo \
    -e ALSA_CARD=1 \
    kjqaq/chatmeow
```

![image-20230529105029863](https://s2.loli.net/2023/05/29/RGUuLH4zhqPAk8Y.png)

![image-20230529105120366](https://s2.loli.net/2023/05/29/FAzD1G9njYpKM23.png)

### 4.和ChatGpt智能语音对话聊天

![image-20230529105217143](https://s2.loli.net/2023/05/29/PKFHELY29b6DiuG.png)

![image-20230529105232081](https://s2.loli.net/2023/05/29/EFqXB6SkYIf7o5O.png)

![image-20230529105257951](https://s2.loli.net/2023/05/29/osTFBq5d1A7LJ2Y.png)





项目原作者:[MeowKJ/chat-meow (github.com)](https://github.com/MeowKJ/chat-meow)