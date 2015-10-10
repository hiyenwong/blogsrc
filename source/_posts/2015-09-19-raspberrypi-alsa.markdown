---
layout: post
title: "raspberrypi 声卡设置"
date: 2015-09-19 14:27
comments: true
categories: [raspberrypi, debian, raspbian]
---

# 关于raspberry pi 2的声音的输出
Raspberry Pi的声音输出可以有两个方式选择:
- HDMI:因为HDMI的信号传输可以达到2.25GB/s，而raspberry pi在画面1028p传输过程中加上音频信号都会小于0.5GB/s,选择是不错的选择。
- 3.5mm音频接口，就普通很多手机的耳机接口。

# Raspberry Pi 2的声音设置
- Raspberry Pi2的CPU是BCM2835,我们首先要安装声音工具包`sudo apt-get install alsa-utils`,不过通常都会有已经安装了.
- 内核加载声卡: `sudo modprobe snd-bcm2835`
- 你可以先测试以下是否有声音，当然你首先要接耳机或是音响，另外接的时候注意功率输出。`speaker-test`
- 如果没有声音，你可以先看看是否音量太底了，你可以用`alsamixer`进行调节.
- 一般raspberrypi 默认是使用HDMI输出音频，你如果要切换为3.5mm的音频口，可能需要设置以下了，`sudo amixer cset numid=3 1`(这里最后一个1则表明耳机，0为自动，2为HDMI) 

最后你可以单独使用文件测试以下：
`sudo aplay /usr/share/sounds/alsa/Front_Center.wav`

-EOF-
