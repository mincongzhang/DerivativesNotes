# 信用衍生品 Credit Derivatives

## 信贷违约互换 Credit Default Swaps

参考实体(Reference Entity): 就是对应的公司, 或者国家

信用事件(Credit Event): 就是违约或者破产, 也可能是债务重组

名义本金(Notional Principal): 对应的总债券金额面值

(Notional principal amounts are the theoretical value that each party pays interest to the other at specified intervals. In bonds, the notional principal amount is equal to the face value of a bond)

整个信贷违约互换(Credit Default Swaps, CDS)的运作就是, 买方定期付钱(一般是按季度付), 如果参考实体(对应的公司)破产或者违约, 买方如果买的是实物交割(physical settlement), 买方有权按债券的面值价格卖出这些债券, 如果买的是现金结算(cash settlement), 买方可以获得债券原面值和拍卖面值的差价. 

案例:

假设买卖方敲定了一个5年的CDS, 开始时间是2015年3月20日. 假设一个公司实体的债券总金额面值$100 million. 买方同意每年付90基点(bp, basis points), 也就是债券金额面值的0.9%, 每个季度支付一部分(1/4). 

![image](https://user-images.githubusercontent.com/5571030/235788841-92e2141d-c263-48f6-8d22-2bca280c4d12.png)

如果没有信用事件(Credit Event)发生, 也就是说该公司没有破产, 所以对应的债券没有违约支付利息, 买方每个季度需要给卖方支付22.5基点(bp, basis points), 也就是每年90bp的1/4. 对应债券面值$100 million, 也就是每个季度支付 0.225% * 100,000,000 = $225,000. 第一次支付时间是2015年6月20日, 之后每个季度依此支付. 

假设信用事件(Credit Event)在2018年5月20日发生了, 也就是这个公司违约了, 债券发不出利息了:

1. 现金结算(cash settlement): 假设买家买的是现金结算, ISDA会进行拍卖, 假设每$100面值的债券拍卖可得$35, 也就是公司剩余资产拍卖用于偿还债务, 最后偿还的债务比例也就是追回率(Recovery Rate)=35%, 那么买家最后可得原债券面值和追回后的价值的差价$65 million收益(最后卖家亏$65 million). 
2. 实物交割(physical settlement): 假设买家买的是实物交割, 买家有权利以全额面值$100 million卖出这些债券. 所以假设这些债券违约, 买家还是可以以$100 million的价格卖给卖家拿回本金. 卖家则拿到这些债券拍卖后的收益$35 million, 最后卖家同样亏$65 million. 

```
上面债券违约后CDS的收益看起来有点怪, 比如"买家有权利以全额面值$100 million卖出这些债券"是怎么回事? 
假如买家起初全额$100 million买入了这些债券, 并且买了对应的CDS, 债券违约后, 手持的CDS就可以保证本金$100 million全部归还. 所以CDS这时候起到了一个保险的作用, 完全对冲掉债券的风险. 
反过来说, 如果起初没有买入债券, 而是直接买了CDS, 那就获得 100M - 35M = $65 million的收益了.
```

### CDS溢价 CDS spread
上面那种每个季度支付的费用, 类似保险费的东西, 是CDS的买方定期向卖方支付一笔溢价, 被称为CDS溢价(CDS spread).

参考: https://www.zhihu.com/question/38915859

## 信贷违约互换和债券收益 Credit Default Swaps and Bond Yields

CDS可以用来对冲公司债券. 假如投资者买了一个5年期年收益7%的公司债券, 同时买一个这些债券对应的CDS来避免债券违约的风险. 假如CDS利差(CDS spread)是200基点(bp, basis points), 也就是每年2%. 那么CDS和债券对冲的结果就是投资者获得了一个近乎5%年收益的无风险的债券(risk-free bond). 

这时会有两种情况:

1. 如果债券没有违约, 买家每年收益 7% - 2% = 5%
2. 如果债券违约, 在违约的事件之前买家每年收益7% - 2% = 5%, 违约之后因为CDS的保险可以全额获得债券的面值. 用这个面值的本金再去投资真正的无风险利率(或者再买一个同类型的债券和CDS). 忽略中间的时间差就是近乎5%无风险年收益

这个案例也说明:

公司债券的收益(bond yield)-无风险利率(risk free rate)=CDS利差(CDS spread)

假如不是这样的话, 投资者可以买入或者做空从而套利, 所以理论上是没有套利空间的. 

这也就是所谓的"CDS债券基础"(CDS–bond basis), 再来看一下它的定义:

![image](https://user-images.githubusercontent.com/5571030/236074508-7471b31b-2dbb-49f7-97c3-a081a7fc3539.png)

债券收益利差(bond yield spread)是用LIBOR互换率(LIBOR/swap rate)作为无风险利率(risk free rate)算得的. 

(Usually the bond yield spread is set equal to the asset swap spread)这一句还没看懂. 


### 最便宜可交割债券 Cheapest to delivery Bond

```
这段原文我觉得简直东拉西扯讲不明白, 我只能凑合翻译整理一下, 同时合并其他参考资料了
```


首先追回率(Recovery Rate)是债券违约后可追回的市场价值和原债券面值的比例. 假设追回率是 $R$ , 债券面值是 $L$ , 所以CDS在信用事件发生后将支付 $L(1-R)$ . 

假设买家当初定的是实物交割(physical settlement), 按我们之前的例子: 

买家有权利以全额面值$100 million卖出这些债券. 所以假设这些债券违约, 买家还是可以以$100 million的价格卖给卖家拿回本金. 

这时候, CDS买方拥有这些债券的最便宜交割权(a cheapest-to-deliver bond option). 下面是我自己的理解, 这些债券在IDSA的定义里可能会有不同的收益(yield), 不同的市场价, 不同的到期日. 但是只要是在IDSA的定义下的债券, 买方可以选择最便宜的债券做实物交割. 

怎么"选"呢? 一方面可能买家手头有比$100 million面值多的债券, 把里面最便宜的拿出来兑换, 剩余的亏损, 这样可以减少买家的亏损(当然这对卖家是不利的). 另一方面假如买家手头没有这些债券, 那么买家可以从市场上买入这些债券实物, 当然肯定不是按面值买入, 比如是按追回率35%的价格买入, 这时候买家也可以选市面上能买到的"最便宜"的债券来交割. 

同样的, 同一个公司债券对应的CDS有大量买方, 信用事件发生时, 需要大量实物交割, 买方并不一定拥有可交割的债券, 这时候他们都想在市场上买这些债券, 从而推高这些债券的价格, 导致这种违约的债券的价格泡沫式增长. 

这样看来现金交割(cash settlement)会更好吗? 现金交割的问题是怎么定义回收率(Recovery Rate). 根据下面参考材料, 由于没有一个直观的方式来决定市场成员公允的违约债券回收率, 通行的做法是通过信用事件拍卖. 当信用事件发生时, 所有以这个实体为参考的 CDS 交易商都可以参加拍卖并得出一个统一的, 市场认同的回收率. 这样就方便现金交割了. 

参考:

境内外信用违约互换发展与现状研究(第21页): http://www.sse.com.cn/aboutus/research/report/c/4849605.pdf 
