# GPIO

general purpose input output (通用输出输出端口)

# 复用模式

复用是指将GPIO的控制权交给片上外设,这不意味着不需要对GPIO口进行任何配置

就算你不进行任何设置,GPIO口会默认为复用推挽模式

复用后,必有输出配置(推挽/开漏),就算不配置也有

四大金刚: GPIOx_MODER GPIOx_OTYPER GPIOx_PUPD  GPIOx_OSPEED

模式选择:输入 | 输出 | 复用

输出模式选择: 推挽 | 开漏

上下拉选择: 浮空 | 上拉 | 下拉

输出速度: 2MHz | 25 MHz | 50MHz | ....

复用寄存器: GPIOx_AFRH/ GPIOx_AFRL 

在程序上是用数组来表示这两个寄存器,比如GPIOx_AFR[0]表示GPIOx_AFRL 低寄存器
