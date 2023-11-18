## CDS定价 CDS Valuation

### 回顾累计到时间t的违约概率和存活概率

先回顾一下我们之前推的公式:

我们用 $\overline{\lambda}(t)$ 表示从时间 $0$ 到 $t$ 的平均风险率(average hazard rate), $Q(t)$ 表示累计到时间 $t$ 的违约概率, 我们有: 

$$Q(t) = 1 - e^{- \overline{\lambda}(t)t  }$$

我们还有存活率(Survival Rate)为:

$$ e^{- \overline{\lambda}(t)t  }$$

### 案例

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
还记得我们之前章节credit risk部分: "从债券收益利差估算违约概率 Estimating Default Probabilities From Bond Yield Spreads"
里面我们的预估就是, 一段时间违约后无法回收的价值期望 = 债券和无风险利率的利差 = CDS溢价(CDS spread)
```


## 连续时间

上面的例子是离散时间下的, 我们现在可以根据例子得出连续时间下的公式. 

再回顾一下我们之前推的公式:

我们用 $\overline{\lambda}(t)$ 表示从时间 $0$ 到 $t$ 的平均风险率(average hazard rate), $Q(t)$ 表示累计到时间 $t$ 的违约概率, 我们有: 

$$Q(t) = 1 - e^{- \overline{\lambda}(t)t  }$$

存活率(Survival Rate)为:

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

http://www.sse.com.cn/aboutus/research/report/c/4849605.pdf 第18页
