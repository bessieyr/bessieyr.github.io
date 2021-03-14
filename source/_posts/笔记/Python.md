[python3 初次使用pyuserinput鼠标键盘消息包的踩坑记录]([python3 初次使用pyuserinput鼠标键盘消息包的踩坑记录_让他让的博客-CSDN博客](https://blog.csdn.net/u014314850/article/details/88352794))

[pip安装第三方包报错：There was a problem confirming the ssl certificate - YinMan - 博客园 (cnblogs.com)](https://www.cnblogs.com/yinhaiping/p/13375375.html)

- 关闭filter断点（机场）

pip install pyuserinput

pip install pyautogui

```python
import os,time,sys
import pyautogui #自动化
from pymouse import PyMouse #鼠标控制
from pynput.mouse import Listener, Button #鼠标监听

# 鼠标控制方式 #
m = PyMouse()
m.move(x, y)
m.click(x, y)
time.sleep(t)

# 监听 #
def on_click(x, y, button, is_press): #宣告function
    if button == Button.right:
        print("鼠标右键，停止监听")
        return False #返回False，停止事件
    print(f"鼠标{button}键在({x}, {y})处{'按下' if is_press else '松开'}")
listener = Listener(
    on_click=on_click
)
listener.start()

# 鼠标坐标显示 #
try:
    while True
        print("Press Ctrl-C to end")
        x,y = pyautogui.position() #返回鼠标的坐标
        posStr="Position:"+str(x).rjust(4)+','+str(y).rjust(4)
        print (posStr) #打印坐标
        time.sleep(0.2)
        os.system('cls') #清楚屏幕
except  KeyboardInterrupt:
    print ('end....')
    

```

