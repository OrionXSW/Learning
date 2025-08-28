# 通信基础

## 串行和并行

串行: 数据逐位按顺序依次传输	特点:传输速率低,抗干扰能力强,通信距离长,成本低,占用IO口少

并行:数据各位通过多条线同时传输 特点: 传输速率高,抗干扰能力弱,通行距离短,成本高,占用IO口多

## 单工/半双工/全双工

传输方向

是否可同时发送

## 同步/异步

是否有同步时钟,时钟线?

## 波特率和比特率

比特率: 每秒发送的**比特**数, 单位: bit/s

波特率: 每秒发送的**码元**数 单位: Baud

比特率 = 波特率 * log2 M  	M表示每个码元承载的信息量

# UART

UART --


# 波特率计算

USART_BRR 	baud rate register

过采样 16 或 8 F4专属 OVER8 取 0 则为16倍采样, 取1为8倍采样

16倍更准确,8倍更快

![1756280256736](image/USART/1756280256736.png)

要求USARTDIV这个值,一般都把OVER8设置成0,即16倍采样

要是把over8设置为0,则有个快速公式:(处理后(移位))的)USARTDIV = (fck + baud / 2) / baud  (有四舍五入的情况)

要是不用四舍五入则USARTDIV(移位后) = fck / baud;

四舍五入最终版:USARTDIV = (fck * 2 + baud) / baud * 2	(16倍采样版本)

```
// 波特率  USART->BRR  要先得到DIV Fplck = 84Mhz (APB2) 
//   double temp;
//   uint16_t mantissa;
//   uint16_t fraction;
//   
//   temp = (float)(84 * 1000000 / (baud * 16));    // over8 = 0 16倍采样 
//   mantissa = temp;     // 获取整数部分
//   fraction = (temp - mantissa) * 16 + 0.5;   // 单位换算,把小数部分转化为能塞入BRR寄存器里面的值 加个0.5四舍五入
//   mantissa <<= 4;      // 左移到[16:4]的位置为小数部分腾开位置
//   mantissa = mantissa + fraction;  
//   // 直接上公式的话(无四舍五入的情况 mantissa = fck / baud)
//   USART1->BRR = mantissa;  // 波特率设置:115200
```
