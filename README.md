# 外部设备控制鼠标键盘小程序
## 应用简介
### 原理
   通过检测物体的横截面变化，将截面变化通过微动开关转化为电信号的方式来实现检测，并通过串口进行数据交换，利用python实现将外部截面变化转换为电脑鼠标变化，实现鼠标的点击和移动。
### 设备构成
1. ESP32开发板（个人感觉性价比较高），进行模拟信号的采集和模数转换
2. 微动开关（就鼠标中键的那种开关），可以检测较小的力，并将其转换为开关信号
3. 电阻与导线若干
4. 数据线（也可以不用，因为ESP32上搭载着蓝牙和WiFi模块）
5. 相关固定结构（这个本人不是很擅长，就还没咋设计）
### 注意事项
警告：由于本软件在运行时会强行控制鼠标，尽管我已经尽可能的进行了测试与调整，但仍不排除出现BUG的可能，在使用该程序前请尽可能关闭其他有着重要工作的软件，以免造成损失，并且如果出现bug的情况，电脑强制关机或者断电不免是一个更好的选择。
### 使用说明
   本软件使用时必须搭配相关的硬件，并且串口得选对，不然无法正常工作
   软件界面如下图所示：
   ![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/b1f57cc4-3f27-40aa-8592-da48cf41108e)
   
#### 各按键功能说明
   ##### 1. "串口相关"说明：
   串口：指设备连接到电脑端之后，系统会在注册表中创建一个设备文件，我们与设备的通信全是基于这个文件来进行的，一般使用默认的设置就行，无需修改数值
      
   ![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/0e3c13d8-d92c-428a-ad8d-b1e601224c06) 
   ##### 2. "键盘相关"说明：
      
   ![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/5f01cbbb-3d1a-4418-9979-c4bf9594a68e)
      
   只有当勾选开启键盘监听时，才会被允许进行相关的热键操作，否则将无法控制鼠标和键盘
      
   ##### 3. "鼠标相关"说明：
      
   ![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/bc0d1d8f-a3d8-4674-bd23-fced9037715c)
   
   只有当允许控制鼠标选择框被勾选时，才被允许进行鼠标的控制，否则将无法进行鼠标的控制
      
   ##### 4. "选择鼠标控制键"下拉框说明：

   ![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/60da18b4-f188-411a-b13f-4a7deb4b4e6c)

   该选框选择的是鼠标的控制按钮，比如选择左键，那么整个软件控制的对象就是鼠标左键，右键就是鼠标右键，中键就是鼠标中键

   ##### 5. "选择鼠标点击模式"下拉框说明：

   ![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/bac4af9f-efef-4164-8ef0-721728257808)

   该选择框控制的是鼠标在被控制移动时是保持鼠标长按还是鼠标在移动时不断点击

   ##### 6. "全自动控制模式"与半自动控制模式说明：

   ![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/d9479bab-cb2a-4049-b636-0d1098bee6ae)

   该选项控制了两种模式：分别是全自动控制模式与半自动控制模式
   
   ###### 6.1 全自动控制模式：

   ![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/7a9e3541-c30f-4b73-9e47-097e32c0e125)
   
   全自动控制模式有以下模式：
   
   ![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/489e5ac5-cc2a-43a5-90e6-951e9b5165e5)

   辅助获取坐标按钮：是将坐标点的选择可视化（在想要移动的起始位置处单击左键，就会记录那个位置的坐标并作为开始移动的开始位置，在想要终止的位置处单击左键，就能记录移动结束的终止坐标）（注：可以切换进程进行位置选择呦）
   
   直线模式：即控制鼠标在选定的两个坐标之间，根据外部设备的信号进行循环

   ![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/c53c202b-bc42-4e95-827f-8eab52d7b5af)
   
   矩形模式：即鼠标移动的轨迹是一个矩形，并根据外部设备的信号进行循环
   
   ![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/1e1ddbc6-2908-488b-abbf-88631a54ffca)

   圆形模式：即鼠标移动的轨迹是一个圆形，并根据外部设备的信号进行循环
   
   ![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/00b82818-6a0a-406e-9e46-d2d96cf4edac)

   记忆模式：可以根据自己之前设置的快捷键进行鼠标移动轨迹的记录，当按下相关快捷键时开始控制时，根据外部设备的信号进行循环（控制终端会有相关提示，按提示操作即可）
   
   ![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/ec06b998-75ae-4b2e-a392-c34339e5385e)

   ###### 6.2 半自动控制模式
   该模式由"选择鼠标点击模式"下拉选择框进行控制：在该模式下，无法控制鼠标的移动轨迹，但能控制鼠标的点击，有单击模式和长按模式，单击模式指的是设备检测到移动了多少个
   微动开关（即有多少个微动开关发生了变化），当个数累加到一定数量时，便会触发一次鼠标点击；而长按模式指的是，设备在指定时间内没有检测到微动开关开合时，软件就会松开鼠标，否则将一直按着鼠标不放
   
   单击模式下的控制方式：
   
   ![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/7aaf6aee-cca6-47be-a205-be1dad29f014)

   长按模式下的控制方式：

   ![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/46d956f7-8fad-4afa-ac6f-2b4a0a539d46)

   ##### 7. 设备校正按钮
   如果是第一次使用：那就必须进行设备的校正，本软件会一直提示

   如果是之前使用过并校准过，但本次传感器的个数发生了变化，本软件也会提醒进行校准
   
   校准流程：当软件与设备建立通信时，首先设备会进行数据自检，即检查连接的传感器个数是否与之前记录的传感器个数相等，如果相当，则正常检测，如果不等，那就会向软件发送重新校准请求，当软件接收到数据时，就会提醒
   进行设备校准，校准过程中，会在终端进行提示，按提示进行校准便可。

### 快捷键相关设置
在主界面旁选择热键设置，即可进行相关热键的设置，当设置完毕时，按下"保存修改"按钮即可（我也忘了是不是同步更新，如果不是的话，重启软件就行，热键的存储位置在data.dat文件中，用记事本即可打开）

![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/1f8766b4-ca77-44a6-8f11-0a3ef6e06575)


## 硬件连接与接线
在设计之初，为了尽可能减少接线，使用了串联分压电路的方式进行数据的采集，这就导致了一个问题，即微动开关的个数并不能无限堆叠，在3.3V电压输入的情况下，建议微动开关个数不超过10个，以下是电路图，以三个为例：

![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/6e2f8df9-2e44-4b83-821d-a430dc0266b3)

仿真结果如下所示：分别闭合开关时的电压电流情况（推荐 http://scratch.trtos.com/circuitjs.html 这个在线电路绘制网页）

![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/bd7cc106-1ab8-450e-9cf7-045c9a08dc1f)

单个微动开关的连接示意图（需要电焊），其他的进行串联即可

![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/f217f983-47b2-4c4b-b69c-709f289735e3)

分压电阻的焊接示意图：

![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/c8a93903-e871-4fb6-b238-77ef7998f8f0)

## 存在的缺陷与不足
在电路和软件的设计上，已经可以进行检测，但现在有个比较大的问题，就是微动开关好像不是很好固定，使用过皮筋进行固定，但会歪，效果不是很好，希望有大佬可以提供一个较好的解决方案，使得通用性尽可能高，即
可以很方便的进行组装和拆卸，并且还可以进行调整。

现在设想的方案是通过皮筋进行固定，如下图所示：
![image](https://github.com/gsd-gsd1/Peripheral-Analog-Mouse-and-Keyboard/assets/140622400/853a33eb-008e-4dbd-8269-3e9faa797e99)

在软件方面，肯定存在各种各样的BUG（毕竟我只用了不到一个星期写出来的代码，个人水平有限，让大家见笑了），还望大家多多见谅，硬件方面的程序用的是Arduino编写的，
这个对新手比较友好，STM32的话，说实话不是初学者一下就能看懂的，并且ESP32比较便宜，主频240MHz，还自带蓝牙和WIFI，仅需20多块钱，个人感觉性价比很高，而且体积还不大，兼容Arduino，python和C（我可不是打广告的，只是这个板子确实不错）。

## 未来的更新计划
找到了一种更好的传感器材料，可以把拉伸转换为电阻变化并且该材料本身具有弹性，非常适合用来该项目，但相关代码还未编写，相关材料还未进行具体的测试实验，但未来的方向就是那样，用一块可粘贴的切具有弹性的柔性传感器薄膜进行检测，可以说是相当方便。
#
