## Martingale vs Markov

Markov: now is independent with previous

马尔可夫过程的条件概率仅仅与系统的当前状态相关，而与它的过去历史或未来状态，都是独立、不相关的

属于马尔可夫过程但不属于鞅过程的例子: 天气预报, 明天的天气只和今天相关, 今天的天气只和昨天有关. 但未来任意一天的天气的期望和今天的天气的期望是不相等的. 比如明天天气的期望和今天相关但是不相等.  

Martingale: future value expectation is the same as current value

已知过去某一时刻 s 以及之前所有时刻的观测值，若某一时刻 t 的观测值的条件期望等于过去某一时刻 s 的观测值，则称这一随机过程是鞅

属于鞅过程但不属于马尔可夫过程的例子: 抛硬币, 或者其他赌博, 因为每一次赌博都和过去或者现在的状态无关, 但是未来一次赌博获胜的期望和现在这次赌博获胜的期望一样. 

属于鞅过程且属于马尔可夫过程的例子: 买入股票和卖出无风险利率这样投资组合的价格

## Martingale

The martingale approach is a mathematical method that models the stochastic behavior of a financial instrument's value over time, and it assumes that the expected value of the instrument's value at any future point in time is equal to its current value.


## markov-and-martingale-processes

http://www.deltaquants.com/markov-and-martingale-processes

## how is martingale used in CDS pricing

In credit default swaps (CDS) pricing, the martingale approach is used to value the risky cash flows associated with the contract. The martingale approach is a mathematical method that models the stochastic behavior of a financial instrument's value over time, and it assumes that the expected value of the instrument's value at any future point in time is equal to its current value.

To apply the martingale approach to CDS pricing, the market is modeled using a probability measure, and a default event is modeled as a jump in the value of the underlying asset. The probability of a default event occurring is estimated using the historical default rates and other relevant market information.

The martingale approach assumes that __the price of a CDS__ should be equal to __the expected value of the discounted future cash flows associated with the contract__. This means that the expected present value of the CDS contract's future cash flows is equal to the current market price of the CDS.

In practice, the martingale approach is used in combination with other valuation techniques, such as Monte Carlo simulation and numerical methods, to accurately price CDS contracts. These techniques take into account the complex interplay between credit risk, market risk, and other factors that can affect the value of CDS contracts.

https://www.acted.co.uk/forums/index.php?threads/markov-vs-martingale-ch8.14423/#:~:text=Que%20%3A%20What%20is%20the%20difference%20between%20Markov%20Property%20and%20a%20Martingale%3F&text=Markov%20means%20where%20go%20next,to%20be%20the%20current%20value.

https://www.quantstart.com/articles/The-Markov-and-Martingale-Properties/

## martingale 怎么用于CDS定价, 或者怎么用于其他金融产品定价呢?

在CDS这种金融产品中, 我们一般可以分成两个"Leg"：
1. Protection Leg: 意思是违约后赔付的现金(对于买家来说是正的)
2. Premium Leg: 意思是在违约之前要定期(一般是按季度)交的保费, 我们想求得这个保费是多少, 也就是CDS定价

那么怎么用martingale定价呢? 我们可以知道在风险中性的环境下, 这两个"Leg"的任何未来时刻的期望都应该是一样的. 我们可以推出Protection Leg的公式, 那么对应的也就可以求得CDS保费了
