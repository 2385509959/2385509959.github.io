---
layout: page
title: 个人语文演讲
permalink: /speech/
icon: book
---
* content
{:toc}

## 前言

这是我的演讲网页。

因为藏得比较深，所以你是找不到的。

好，话不多说，毕竟只有三分钟。

我是不会承认我这样做是为了不用带 U 盘，偷懒。

## 句子分享

**以下内容涉及较为深奥，请扶稳坐好！**

### 我思故我在

在我们的日常生活，可能大家在沉思时，会思考这样的问题：

* 我是谁？
* 我在哪里？
* 我要干什么？

很显然，这样的问题我们是找不到答案，但是我们可以确定一点，我们还活着。

在哲学上这叫做还原，但我们不讨论这一点。

只要我们还活着，宇宙就一定会满足一个状态，一个让你活着的状态。

只要你在思考，你就存在。

你存在，宇宙才存在。

形象地说，就像是 x+y=10，你活着，所以 x=1 ,x=1 是你生死的状态

可以发现，这时 y是有取值范围的，但也不唯一确定。

毕竟，如果所有状态都确定了，活着就没有意思了。

这就是著名的**人存原理**。

在物理学，天文学，哲学等方面，都有广泛的应用。

当然，我更愿意说 “一切都是命运石之门的选择！”

<iframe height=498 width=510 src="https://player.youku.com/embed/XNTExNDg5NDgzMg==" frameborder="no" allowfullscreen="false"></iframe>

~~
# -*-  coding:utf-8 -*-
import socket
from time import ctime
HOST=''
PORT=80
ADDRESS=(HOST,PORT)
MAX_LISTEN=5
BUFFSIZE=1024
def tcpClient():
    # 创建客户套接字
    # 本身支持的格式 socket 构造对象 方法
    # with as 相当于 try finally exspect 方法 as
    # socket stream 为数据流 即 TCP/IP 协议 的基础
    # AF-INET 为因特网之间的数据传输协议
    # 除此之外，还有另外两种 用于 UDP 或 UNIX内核的两种较常用的通讯协议
    with socket.socket(family=socket.AF_INET, type=socket.SOCK_STREAM) as s:
        # 尝试连接服务器
        s.connect(ADDR)
        print('连接服务成功！！\n 现在可以开始对话了')
        # 通信循环
        while True:
            inData = input('pleace input something:')
            if inData == 'q':
                break
            # 发送数据到服务器
            inData = '[{}][{!r}]:{}'.format(ctime(),yourname, inData)
            # 在 python 3.x 中 数据传输的中间类变为 字符串 ，而非 unicode 字符，转码时需要注意
            s.send(inData.encode(ENCODING))
            print('发送成功！')

            # 接收返回数据
            outData = s.recv(BUFFSIZE)
            print('返回数据信息：{!r}'.format(outData.decode('utf-8')))

        # 关闭客户端套接字
        s.close()

~~

~
import socket
from time import ctime
import json
import time
HOST = '172.37.16.42'
PORT = 9001
ADDR = (HOST, PORT)
BUFFSIZE = 1024
MAX_LISTEN = 5

'''
1.初始化监听，数据包最大数等属性
2.初始化数据流对象
3.绑定服务器地址和端口
4.开启监听
5.连接用户，得到数据
'''
def tcpServer():
    # TCP服务
    # with socket.socket() as s:
    while True:
        with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
            # 绑定服务器地址和端口
            s.bind(ADDR)
            # 启动服务监听
            s.listen(MAX_LISTEN)
            print('等待用户接入…………………………')
            f=0
            while True and f==0:
                # 等待客户端连接请求,获取connSock
                conn, addr = s.accept()
                '''注：accept返回两个对象'''
                print('警告，远端客户:{} 接入系统！！！'.format(addr))
                with conn:
                    while True:
                        print('接收请求信息。。。。。')
                        # 接收请求信息
                        data = conn.recv(BUFFSIZE)
                        temp=data
                        print('data={!r}' .format(temp.decode('utf-8')))
                        if(data==b''):
                            f=1
                            break
                        now_data=data.decode('utf-8')
                        print('接收数据：{!r}'.format(data.decode('utf-8')))

                        # 发送请求数据
                        conn.send(now_data.encode('utf-8'))
                        print('发送返回完毕！！！')
        s.close()


# 创建UDP服务
if __name__ == '__main__':
    HOST=input('Input your address:')
    while True:
        choice = input('input choice t for tcp q for quit or u for udp:')
        if choice != 't' and choice != 'u' and choice !='q':
            print('please input t q,or u,ok?')
            continue

        if choice == 't':
            print('execute tcpsever')
            tcpServer()
        elif choice == 'u':
            print('execute udpsever')
            udpServer()
        elif choice == 'q':
            break
    flush=input('Press any key to break this handle.')

~
import urllib.request
import gzip
import json
import tkinter as tk
print('------         天气查询       ------')
def get_weather_data() :
    city_name = input('请输入查询天气的城市名称：')
    url1='http://wthrcdn.etouch.cn/weather_mini?city='+urllib.parse.quote(city_name)
    url2='http://wthrcdn.etouch.cn/weather_mini?citykey=101010100'
    weather_data=urllib.request.urlopen(url1).read()
    weather_data=gzip.decompress(weather_data).decode('utf-8')
    weather_dict=json.loads(weather_data)
    return weather_dict
def show_weather(weather_data):
    weather_dict = weather_data 
    if weather_dict.get('desc') == 'invilad-citykey':
        print('你输入的城市名有误')
    elif weather_dict.get('desc') =='OK':
        forecast = weather_dict.get('data').get('forecast')
        print('城市：',weather_dict.get('data').get('city'))
        print('温度：',weather_dict.get('data').get('wendu')+'℃ ')
        print('感冒：',weather_dict.get('data').get('ganmao'))
        print('风向：',forecast[0].get('fengxiang'))
        print('风级：',forecast[0].get('fengli'))
        print('高温：',forecast[0].get('high'))
        print('低温：',forecast[0].get('low'))
        print('天气：',forecast[0].get('type'))
        print('日期：',forecast[0].get('date'))
        print('*******************************')
        four_day_forecast =input('是否要显示接下来一天的天气（最多五天），Y/N：')
        if four_day_forecast == 'Y' :
            for i in range(1,5):
                print('日期：',forecast[i].get('date'))
                print('风向：',forecast[i].get('fengxiang'))
                print('风级：',forecast[i].get('fengli'))
                print('高温：',forecast[i].get('high'))
                print('低温：',forecast[i].get('low'))
                print('天气：',forecast[i].get('type'))
                print('--------------------------')
                flag1=input('是否要显示接下来一天的天气，Y/N：')
                if flag1 == 'N' :
                    break
            print('查询结束')        
    flag=input("是否继续查询天气？Y/N：")
    if flag == 'Y':
        return 1
    else :
        return 0
while(1==1):    
    if show_weather(get_weather_data()) == 0 :
        break
char=input("-----------------------按任意键结束进程-----------------------")

~

~
