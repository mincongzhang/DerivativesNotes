# [John Hull教材笔记] 信贷违约互换 Credit Default Swaps

最近看了John C. Hull的《Options, Futures, and Other Derivatives》里Credit risk和Credit Derivatives章节, 本想一节一节学习并翻译, 但发现这本书的知识逻辑实在是不太行, 我不得不自己整理出一个稍清晰一些的知识体系. 同样,  细节以原文为主, 有问题欢迎指出.

这篇文章主要整理信贷违约互换(Credit Default Swaps, CDS)的背景知识和定价方法. 结构大概为:

1. 背景知识
2. CDS定价初探以及相关概念
3. 追回率/回收率(Recovery Rates)
4. 违约概率, 存活概率以及风险率(Default Probability, Survival Probability and Hazard Rate)
5. CDS定价案例
6. 连续时间CDS定价公式
7. 其他相关知识

## 1. 背景知识

首先来说人话, 信贷违约互换(Credit Default Swaps, CDS, 之后我们都用CDS缩写)是什么东西并且有什么用.

作为投资人, 你会购买一些债券, 比如公司债券, 以获取债券的利息作为投资回报. 但是公司有可能破产呀, 破产后直接本金亏完这就是很大的风险. 这时候你可以去找投行买一些这个公司的保险, 如果公司破产, 这份保险可以让你把这份债券的本金收回. 当然买保险你肯定要定期付保费, 一般是在这个公司没破产的情况下, 每个季度付保费. 那么这个保险合约也就是信贷违约互换(Credit Default Swaps, CDS). 

由此, CDS这种合约可以正常用来对冲风险, 也可以玩出花样, 作为投资人, 你可以:

1. 买一份某公司债券, 买相应的CDS作为保险, 完美对冲风险, 当然也就没有额外收益了, 在理想环境下这时候的收益就单纯的是无风险利率
2. 不买债券, 直接买CDS, 赌这个公司未来某时刻会破产, 如果真破产了那收益就很大了, 如果没破产也就亏个保费还凑合
3. 其他玩法

关于CDS最有名的也就是玩出2008年的次贷危机了吧. 最初是一位大佬赌房地产贷款这样的固定收益资产会崩盘(也就是赌很多人会还不起贷款), 让投行创造出对应的CDS, 然后投行基于这种CDS又创造出很多复杂衍生品, 最后确实很多人付不起贷款, CDS的保险作用确实生效了, 但基于此的其他复杂衍生品崩盘, 最后美国政府/纳税人买单. 有兴趣可以看看电影《大空头》里面讲的挺不错. 

接着来看看复杂版本的解释, 先来定义一些术语:

参考实体(Reference Entity): 就是对应的公司, 或者国家

信用事件(Credit Event): 就是违约或者破产, 也可能是债务重组

名义本金(Notional Principal): 对应的总债券金额面值

```
Notional principal amounts are the theoretical value that each party pays interest to the other at specified intervals. In bonds, the notional principal amount is equal to the face value of a bond
```

整个信贷违约互换(Credit Default Swaps, CDS)的运作就是, 买方定期付钱(一般是按季度付), 如果参考实体(对应的公司)破产或者违约, 买方如果买的是实物交割(physical settlement), 买方有权按债券的面值价格卖出这些债券, 如果买的是现金结算(cash settlement), 买方可以获得债券原面值和拍卖面值的差价. 

## 2. CDS定价初探以及相关概念

按上面的背景, 其实CDS这个产品有两部分:

1. 买方按时支付的保费(CDS spread, Premium Leg)
2. 破产后卖方的赔款(CDS payoff, Protection Leg)

__CDS定价其实就是, 算出买方每次需要交够多少保费, 期望上才能和最终破产后卖方的赔款一样.__

对于CDS的赔款还有一些细节. 首先公司破产后, 公司债券价值并不是直接清零, 所以我们有一个回收率(Recovery rate)的概念. 当一个公司破产, 这个公司剩余的资产还是可以被用来抵债. 假如一个公司的债券值$100,000, 最后剩下的资产变卖可回收$80,000, 那么这个公司债券的回收率就是80%. 此外我们还需要某个公司的存活概率和相应的破产概率. 

至此我们已经有了CDS定价所需的所有内容了. 

我们定义未知的保费为 $s$, 并且假设公司在某个时间点破产, 来看看CDS的两部分的公式:

买方按时支付的保费期望:

$$Premium Leg = s \times 存活到t时刻概率 = s \times P\(存活到t时刻\)$$

破产后卖方的赔款期望:

$$Protection Leg = \(1-回收率\) \times 存活到t时刻条件下的破产概率 = \(1-R\) \times P( t时刻破产概率 | 存活到t时刻 )$$

这两部分的期望应该是相等的, 所以我们有:

$$s \times P\(存活到t时刻\) = \(1-R\) \times P( t时刻破产概率 | 存活到t时刻 )$$

其中只有 $s$ 是未知的, 解出即可. CDS定价就这么完成了, 所以其实概念上非常简单对吧. 

当然我们也不是止步于此, 提到的这一系列概念还值得深挖. 

接下来我们会讨论和深挖这些必要的知识概念, 我们会介绍追回率/回收率, 违约概率, 存活概率以及风险率, 有了这些知识后我们通过一个简单的例子走一遍CDS定价的流程, 最后就可以整理出CDS定价的公式了. 

## 3. 追回率/回收率 Recovery Rates

刚才其实已经介绍了追回率/回收率(Recovery Rates). 现在正式再来一次. 

当一个公司破产, 这个公司剩余的资产还是可以被用来抵债. 假如一个公司的债券值$100,000, 最后剩下的资产变卖可回收$80,000, 那么这个公司债券的回收率就是80%. CDS合约要赔付的也只有 $20, 000. 

我们定义一个债券的回收率(Recovery rate)为这个公司破产违约后, 这个债券能追回的市场价值和债券本身面值所占的百分比, 如下面表格例子:

![image](https://user-images.githubusercontent.com/5571030/235479159-9278111d-8e32-4f53-8451-12d4d979f89e.png)

## 4. 违约概率, 存活概率以及风险率 Default Probability, Survival Probability and Hazard Rate

接下来我们看一些历史违约概率案例, 并引入风险率(hazard rate)的概念.  借由风险率我们可以得到连续时间里的存活概率和条件违约概率. 


### 历史违约概率 Historical default probabilities

来看看以下评级机构(穆迪)的案例表格, 表示的是逐年的累计违约概率 (cumulative default rates)

红圈部分表示的是:
1. __从开始__ 到第一年结束时有0.177%的概率会违约
2. __从开始__ 到第二年结束时有0.495%的概率会违约
3. 以此类推. 

那么单看第二年间违约的概率是 $0.495-0.177=0.318$ %

![image](https://user-images.githubusercontent.com/5571030/235375368-0c1d9d57-9770-4f7b-8e2c-429a2484350c.png)

再看看A评级的债券和B评级的债券, 我们可以观察到A评级债券每年违约概率竟然会逐渐上升, 而B评级债券每年违约概率竟然会逐渐下降. 

原因是, 对于一个评级较差的债券, 第一二年会比较关键, 活过这两年后, 活的时间越久它的经济状况就会越好, 越不容易违约. 

![image](https://user-images.githubusercontent.com/5571030/235375423-ca921c1f-e857-4f47-8894-be189823a017.png)

### 风险率 Hazard Rates

来看看下面评级Caa及以下的债券, 在第三年期间的违约概率是 $36.908-27.867=9.041$ %

我们把这种概率称为无条件违约概率(unconditional default probability). 

再看条件违约概率, 我们可以做以下计算:

累计存活到第二年底的概率: $100-27.867=72.133$ %

在前两年不违约的条件下, 第三年违约的条件违约概率: $9.041/72.133=12.53$ % 

![image](https://user-images.githubusercontent.com/5571030/235376631-c8482c82-6653-4660-ac6b-4e7875be7f4f.png)



我们刚才算的第三年条件违约概率: $9.041/72.133=12.53$ % 取的是一年的长度. 现在我们来取极限, 求得某时刻 $t$ 的存活概率和违约概率. 并用风险率(Hazard rate)来表示他们. 

我们先做一些风险率(Hazard rate)相关的定义:

1. 假设一段极短时间: $\Delta t$
2. 在 $t$ 时刻前不违约的条件下, 在 $t$ 时刻的风险率(Hazard rate): $\lambda(t)$
3. 在 $t$ 和 $t + \Delta t$ 这段时间, 在之前不违约的条件下, 这段时间的条件违约概率: $\lambda(t) \Delta t$

所以

$$某时间段的条件违约概率 = 风险率\(Hazard \ rate\) \times 时间段$$

也就是

$$\Delta t时间段的条件违约概率 = \lambda(t) \Delta t$$


然后是存活概率和条件违约概率:

1. 累计到 $t$ 时刻的存活概率: $V(t)$, 累计到 $t$ 时刻的条件违约概率: $1-V(t)$
2. 累计到 $t + \Delta t$ 时刻的存活概率: $V(t + \Delta t)$,  累计到 $t + \Delta t$ 时刻的条件违约概率: $1-V(t + \Delta t)$

这样我们就可以把以上两者结合, 得到在 $t$ 时刻前不违约的条件下, $t + \Delta t$ 违约的概率:

$$ \frac {[1-V(t + \Delta t)] - [1-V(t)]} {V(t)} = \lambda(t) \Delta t$$

整理可得:

$$ V(t + \Delta t) - V(t) =  - V(t) \lambda(t) \Delta t $$

取极限: 

$$ \frac{dV(t)} {dt} =  - V(t) \lambda(t) $$

```
下一步教材没说:
```

观察上式 $V(t)$ , 并且我们查导数表(Differentiation rules)可知:

$$ \frac{de^{f(x)}} {dx}  = f'(x)e^{f(x)}  $$

$x$ 换成 $t$, $f(t)$ 换成 $- \int_{0}^{t} \lambda(\tau) d \tau $, 我们可得: 

$$ \frac{de^{- \int_{0}^{t} \lambda(\tau) d \tau}} {dt}  = - \lambda(t)e^{- \int_{0}^{t} \lambda(\tau) d \tau}  $$

```
回到教材:
```

所以我们可以凑出累计到 $t$ 时刻的存活概率 $V(t)$:

$$ V(t) = e^{-  \int_{0}^{t} \lambda(\tau) d \tau } $$

其实也可以看出 $t$ 时刻的条件存活概率为:

$$ V(t) = e^{-  \lambda(t)  } $$

我们再定义 $Q(t)$ 为到时间 $t$ 的违约概率, 那么我们有:

$$Q(t) = 1 - V(t)$$

带入 $V(t)$:

$$Q(t) = 1 - e^{- \int_{0}^{t} \lambda(\tau) d \tau }$$

我们用 $\overline{\lambda}(t)$ 表示从时间 $0$ 到 $t$ 的平均风险率(average hazard rate), 我们可以修改上式为: 

$$Q(t) = 1 - e^{- \overline{\lambda}(t)t  }$$

这个平均风险率(average hazard rate)我们也可以称为违约强度(default intensity). 这个概念对我们主线知识没什么用. 但是在这个领域里比较重要, 借此一提. 


## 5. CDS定价案例

通过上面推导出来的存活概率和违约概率, 我们可以列出一系列表格, 其实就可以做CDS定价了. 虽然我们现在还没有推出公式, 但我们通过下面例子来看看怎么给CDS定价的. 

如果要给给某个参考实体(Reference Entity)的CDS溢价(CDS spread)定价, 我们可以用估算的违约概率来做. 我们来看一个5年期CDS案例. 假设这个参考实体(Reference Entity)比如某个公司, 每年的风险率都是2%, 并且5年都一样. 根据上面的公式, 它的存活率是 $e^{-0.02t}$ . 那么我们有:

1. 到第一年年底的存活率(Survival Probability): $e^{-0.02*1}=0.9802$ , __这一年间的__ 违约概率: $e^{-0.02 * 0} - e^{-0.02 * 1}=0.0198$
2. 到第二年年底的存活率: $e^{-0.02 * 2} = 0.9608$, __这一年间的__ 违约概率: $e^{-0.02 * 1} - e^{-0.02 * 2}=0.0194$
3. 以此类推

我们还可以画出以下表格:

![image](https://user-images.githubusercontent.com/5571030/236641125-032ea53d-49fb-4ea8-8fc2-aa86faddb986.png)

我们再做一些假设:
1. 假如违约总是发生在年中
2. 买家每年对CDS的付款都在年底
3. 无风险利率每年都是5%, 并且是复利形式, 这样折现率(Discount Factor)就是 $e^{-0.05t}$
4. 追回率(Recovery Rate)是40%
5. 债券总面值(notional principal)是$1
6. 每年CDS溢价(CDS spread), 也就是每年买家需要支付费率设为 $s$, 这也是我们最后要算的

#### CDS买家5年支付费用期望 = 每年CDS费用期望 + 每年年中违约半年费用期望

先算每年年底的CDS溢价(CDS spread)的期望费率, 也就是CDS买家每年年底需要支付的费用. 同时因为是到年底, 通过折现我们可以算得:

折现率第一年 $e^{-0.05*1} =0.9512$

折现率第二年 $e^{-0.05*2} =0.9048$

以此类推. 

现在我们就可以算得以后每年CDS溢价(CDS spread)折现到现在的期望费用(Expected Payment): 

![image](https://user-images.githubusercontent.com/5571030/236695316-b7a07a03-13d4-4ed9-8194-172b1b5d7b45.png)


因为我们假设违约是发生在年中, 这0.5年期间的累计CDS溢价费用我们要记为 $0.5s$ , 这样我们还要算一下这些半年费用的期望:

![image](https://user-images.githubusercontent.com/5571030/236703857-2ce59399-0470-46e1-be3c-1953349e07ae.png)

我们可以算得支付费用总期望:

$$4.0728s + 0.0422s = 4.1150s$$

#### CDS买家5年收益期望

接下来我们算违约后买方的期望收益(Payoff), 按前面假设违约总是发生在年中, 我们再算一下折现率:

折现率第0.5年 $e^{-0.05*0.5} =0.9753$

折现率第1.5年 $e^{-0.05*1.5} =0.9277$

以此类推

我们就可以写出以下表格, 算得每年的期望收益(Payoff):

![image](https://user-images.githubusercontent.com/5571030/236703845-8021c2e8-e521-45f5-934d-42c6dd75a13e.png)

我们可以算得收益总期望:

$$0.0506$$

#### 风险中性情况下, 5年收益期望 = 5年支付费用期望

最后我们知道在风险中性情况下, 没有可套利的空间, 所以 5年收益期望 = 5年支付费用期望, 我们有:

$$4.1150s = 0.0506$$

可得:

$$s = 0.0123$$

也就是说我们算出的CDS定价为123基点(bp, basis points).

回到例子, 我们算出来对$1面值的债券, 不算现金流折现, 每年买家该向卖家支付:
1. $0.9802s = 0.9802*0.0123 = 0.0121$
2. $0.9608s = 0.9608*0.0123 = 0.0118$
3. $0.9418s = 0.9418*0.0123 = 0.0116$
4. $0.9231s = 0.9231*0.0123 = 0.0114$
5. $0.9048s = 0.9048*0.0123 = 0.0111$

```
我们算出CDS定价为0.0123=123bp, 其实我们可以观察到, 0.0123 = 0.02 * (1-0.4) = 每年风险率 * (1-追回率)
我们之后会有一个话题: "从债券收益利差估算违约概率 Estimating Default Probabilities From Bond Yield Spreads"
里面我们的预估就是, 一段时间违约后无法回收的价值期望 = 债券和无风险利率的利差 = CDS溢价(CDS spread)
```

## 6. 连续时间CDS定价公式

学术化讨论的话, 我们最终都需要整理出一套连续时间下的定价公式. 

通过上面离散时间下的例子, 我们现在可以得出连续时间下的公式. 

再回顾一下我们之前推的公式:

我们用 $\overline{\lambda}(t)$ 表示从时间 $0$ 到 $t$ 的平均风险率(average hazard rate), 我们有存活率(Survival Rate):

$$ e^{- \overline{\lambda}(t)t  }$$

### CDS溢价期望 Expectation of CDS spread (Premium leg)

我们来算一下连续时间下买家需要支付的CDS溢价(CDS spread). 

假设债券到 $T$ 时刻违约, 并且每$1债券面值的CDS费率为 $s$ , 那么CDS溢价连续时间现金流的折现价值是:

$$s*SUM(&Delta;t存活概率 * &Delta;t现金流折现)$$

也就是:

$$s  \int_{0}^{T} e^{- \lambda(t)t  } e^{- rt  }   dt$$

$$ s \int_{0}^{T} e^{- (\lambda(t)  + r)t  }   dt$$

### 收益期望 Expectation of CDS payoff (Protection Leg)

假设债券到 $T$ 时刻违约, 那么买家可收到的CDS偿付的折现价值是: 

$$(1-追回率Recovery Rate) * SUM(&Delta;t 风险率 * &Delta;t 存活率 * &Delta;t现金流折现)  $$

也就是: 


$$ (1-R) \int_{0}^{T} \lambda(t) e^{- \lambda(t)t  } e^{- rt  }   dt$$

$$ (1-R) \int_{0}^{T} \lambda(t) e^{- (\lambda(t)  + r)t  }   dt$$

$$ (1-R) \overline{\lambda}(t) \int_{0}^{T} e^{- (\lambda(t)  + r)t  }   dt$$



### 溢价期望和收益期望相等  Expectation of CDS spread = Expectation of CDS payoff

在风险中性测度下, 买家支付的溢价期望和CDS偿付收益期望应该相等. 也就是上面两个公式应该相等:

$$ s \int_{0}^{T} e^{- (\lambda(t)  + r)t  }   dt = (1-R) \overline{\lambda}(t) \int_{0}^{T} e^{- (\lambda(t)  + r)t  }   dt$$

于是最后我们可以推得:

$$ s = (1-R) \int_{0}^{T} \lambda(t) dt $$

$$ s = (1-R) \overline{\lambda}(t) $$


参考:

境内外信用违约互换发展与现状研究(第18页): http://www.sse.com.cn/aboutus/research/report/c/4849605.pdf 

## 7. 其他相关知识


### 从债券收益利差估算违约概率(信用三角) Estimating Default Probabilities From Bond Yield Spreads(credit triangle)

另一种预估违约概率的方法是通过债券收益利差(Bond Yield Spreads). 

债券收益利差是债券收益率和无风险利率(risk free rate)的利率差. 这中间的差别, 也就是比无风险利率多出的超额收益, 可以看作对违约风险的补偿. 

我们来做一些假设:

1. 假设 $T$ 年期债券每年的利差(Bond Yield Spread): $s(T)$
2. 假设这段时间的平均风险率(Average Hazard Rate): $\overline{\lambda}(T)$
3. 假设回收率(Recovery Rate): $R$

那么我们可得: 这段时间违约后无法回收的价值期望: $\overline{\lambda}(T) (1-R)$

这个期望应该和利差相等: 

$$ \overline{\lambda}(T) (1-R) = s(T) $$

$$ \overline{\lambda}(T)  = \frac{s(T)}{(1-R)} $$

这种预估适用于很大一部分情况. 

这也是一个比较有名的概念 __信用三角(credit triangle)__:

信用三角就是上面那个简单公式. 如果我们有回收率(Recovery Rate), 并且我们可以从市场上观察到CDS利差(CDS Spread, 市场上的CDS Spread也叫Par Spread), 那么我们就可以估算出风险率(Hazard Rate)了. 

有了风险率(Hazard Rate)我们也可以算得风险中性下的隐含违约概率. 

```
The term "credit triangle" refers to the simple formula that relates the single-name CDS spreads to the risk neutral hazard rates and recovery rates (RR). Thus, having RR
fixed, it is easy to estimate hazard rates from CDS spreads observed in the market place. The hazard rate is the key attribute of the “reduced-form” framework. Knowing the hazard
rate one may estimate the implied risk neutral probability of default (PD) of the company that has issued a bond protected by the CDS contract.
```

参考: Katz, Yuri A., Navigating Beyond the Credit Triangle (January 22, 2015). Available at SSRN: https://ssrn.com/abstract=2554027 or http://dx.doi.org/10.2139/ssrn.2554027

__来看一个例题__

假设一个公司的一年期, 二年期, 三年期债券的债券收益和无风险利率的利率差(Bond Yield Spread)分别是: 150, 180和195基点(basis points). 假设回收率(Recovery Rate)是40%.

根据公式: 

$$ \overline{\lambda}(T)  = \frac{s(T)}{(1-R)} $$

我们有:

1. 第一年的平均风险率(Average Hazard Rate): $[0.0150/(1-0.4)] = 2.5$ %
2. 第一年和第二年的平均风险率(Average Hazard Rate): $[0.0180/(1-0.4)] = 3.0$ %
3. 第一年,第二年和第三年的平均风险率(Average Hazard Rate): $[0.0195/(1-0.4)] = 3.25$ %

我们也可以算出:

1. 第二年的平均风险率(Average Hazard Rate): $2 \times 0.03 - 1 \times 0.025 = 3.5$ %
2. 第三年的平均风险率(Average Hazard Rate): $3 \times 0.0325 - 2 \times 0.03 = 3.75$ %

### 信贷违约互换和债券收益 Credit Default Swaps and Bond Yields

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
