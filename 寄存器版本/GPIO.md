GPIO配置(寄存器版)

挂载时钟使能 | 端口模式 |输入/输出数据寄存器 | 输出模式 | 输出速度

# 通用输出配置

例1: 把 PC6 设置为 输出模式 默认高电平

RCC->AHB1ENR  |= (1 <<  2)	;		// 	使能AHB1总线上的GPIOC外设时钟

GPIOC->MODER &=  ~( 3 << 12);		// 	先清空相应的Bit位

GPIOC->MODER |= (1 << 12);		//	设置成通用输出模式

GPIOC->OTYPER  &=  ~( 1 << 6);		//	设置为推挽输出模式

GPIOC->OSPEEDR &= ~( 3 << 12)	// 	先清空相应的Bit位

GPIOC->OSPEEDR  |=  1 << 12		// 	输出速度中等

GPIOC-> PUPDR  &=  ~(3 << 12)	//	不上拉也不下拉

GPIOC->ODR 	&=  ~(1 << 6);		//	设置输出电平

GPIOC->ODR    |=	(1<<6);

# 通用输入配置

例2: 将PC3 设置成 输入模式 上拉

RCC->AHB1ENR  |= (1 <<  2)	;		// 	使能AHB1总线上的GPIOC外设时钟

GPIOC->MODER &=  ~( 3 << 6);		// 	清空相应的Bit位,默认00为输入模式

GPIOC->PUPDR &=  ~(3 << 6);

GPIOC->PUPDR |= (1 << 6);

如此即配置好通用输入模式

要想读取该端口的电平: 与上对应位即可

uint8_t  val =  (GPIOC->IDR  & (1 << 3));
