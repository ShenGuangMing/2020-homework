# 1.书上作业

## 1.1第五章：

---

#### _2题：七段数码管有哪两种类型？断码如何确定？_

**答：**

共阴极和共阳极两种

0x3f 、0x06 、0x5b 、0x4f 、0x66 、0x6d 、0x7d 、0x07 、0x7f 、0x6f
、0x77 、0x7c 、0x39 、0x5e 、0x79 、0x71

无显示：0x00

只显示一点：0x80

共阳：只需和共阴互补即可，比如：
共阳0为：0xc0
共阴0为：0x3f
> 注：相加后两位等于ff即，c0 + 3f = ff

---

#### _6题：试说明矩阵式键盘的键扫描及识别过程。_
**参考1：**：

按键设置在行、列线交点上，行、列线分别连接到按键开关的两端。行线通过上拉电阻接到+5V上，无按键按下时，行线处于高电平状态，而当有按键按下时，行线电平状态将由与此行线相连的列线的电平决定。列线的电平如果为低，则行线电平为低;列线的电平如果为高，则行线的电平亦为高。将行、列线信号配合起来并做适当的处理，才能确定闭合键的位置。

**参考2：**

首先使与行线相连的端口线输出全零,然后读入列线的状态,如果全是"1"表明无按键按下,若非全“1"则表明有键按下。




## 2.1第六章：

---

#### _1题：80C51单片机有几个中断源？各中断标志是如何产生的？又是如何复位的？CPU响应各中断时，其中中断入口地址是多少？_

**答：**

5个中断源,分别为外中断INTO和INT1、T0和T1溢出中断、串口中断。

电平方式触发的外中断标志与引脚信号一致;边沿方式触发的外中断响应中断后由硬件自动复位。

TO和T1,CPU响应中断时,由硬件自动复位。RI和TI,由硬件置位。必须由软件复位。另外,所有能产生中断的标志位均可由软件置位或复位。

各中断入地址:INTO-0003H,TO一000BH,INT1-0013H,T1-001BH,RI和TI一0023H


---

#### _3题：外部中断源有电平触发和边沿触发两种方式，他们的中断过程有何不同？怎样设定？_

**答：**

采用中断电平触发方式时,中断请求标志ITO=0,CPU在每个机器周期的S5P2期间采样，一旦在P3.2(INTO)引脚上检测到低电平,则有中断申请,使IEO置位(置1),向CPU申请中断。

在电平触发方式中,在中断响应后中断标志位IEO的清0由硬件自动完成,但由于CPU对P3.2(INTO)引脚没有控制作用,使中断请求信号的低电平可能继续存在,在以后的机器周期采样时又会把已清0的IEO标志位重新置1,所以,在中断响应后必须采用其它方法撤消该引脚上的低电平,来撤除外部中断请求信号,否则有可能再次中断造成出错。

采用边沿触发方式时,ITO=1,CPU在每个机器的S5P2期间采样,当检测到前一周期为高电平,后一周期为低电平时,使标志IEO置1,向CPU申请中断,此标志位一直保持到CPU响应中断后,才由硬件自动清除。在边沿触发方式中,为保证CPU在两个机器周期内检测到由高到低的负跳变,高电平与低电平的持续时间不得少于一个机器周期的时间。

