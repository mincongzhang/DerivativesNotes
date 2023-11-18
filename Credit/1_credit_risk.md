# 信用风险 Credit Risk

## 信用评级和评级机构 Credit rattings

评级机构有:

1. 穆迪(Moody's)
2. S&P
3. Fitch

他们主要是给公司债券做信用评级. 

穆迪的评级从高到低有: Aaa, Aa, A, Baa, Ba, B, ... 其中Aaa是最高信用评级, 表示几乎不可能违约.

我们认为只有Baa或以上评级的债券才有投资价值(investment grade), 以下的都算垃圾价值(junk grade).

(这两个名词找不到对应中文翻译, 我只能意译了)

参考:

https://www.investopedia.com/ask/answers/what-does-investment-grade-mean/#citation-1


## 历史违约概率 Historical default probabilities

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

## 风险率 Hazard Rates

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

这个平均风险率(average hazard rate)我们也可以称为违约强度(default intensity).

## 追回率/回收率 Recovery Rates

当一个公司破产, 这个公司剩余的资产还是可以被用来抵债. 假如一个公司的债券值$100,000, 最后剩下的资产变卖可回收$80,000, 那么这个公司债券的回收率就是80%.

我们定义一个债券的回收率(Recovery rate)为这个公司破产违约后, 这个债券能追回的市场价值和债券本身面值所占的百分比, 如下面表格例子:

![image](https://user-images.githubusercontent.com/5571030/235479159-9278111d-8e32-4f53-8451-12d4d979f89e.png)

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

https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2554027

参考: Katz, Yuri A., Navigating Beyond the Credit Triangle (January 22, 2015). Available at SSRN: https://ssrn.com/abstract=2554027 or http://dx.doi.org/10.2139/ssrn.2554027

#### 来看一个例题

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
