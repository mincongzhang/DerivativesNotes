

```
C++
simd vector
https://stackoverflow.blog/2020/07/08/improving-performance-with-simd-intrinsics-in-three-use-cases/
```

```
C++
AAD programming
https://informaconnect.com/a-brief-introduction-to-automatic-adjoint-differentiation-aad/#:~:text=AAD%20(where%20the%20first%20A,the%20scenes%2C%20over%20calculation%20code.
```

```
template, and template specialisation
static polymorphism with template
C++ 20 template: https://en.cppreference.com/w/cpp/language/constraints

https://www.geeksforgeeks.org/templates-cpp/
```

```
inline and when to use it
https://stackoverflow.com/questions/1932311/when-to-use-the-inline-function-and-when-not-to-use-it
```

```
C++ type traits
https://www.internalpointers.com/post/quick-primer-type-traits-modern-cpp
```

```
Math:
1/x diff => -1 x^(-2)

https://qcweb.qc.edu.hk/math/Resource/AL/Derivative%20Table.pdf
```

```
CVA inputs: 
e.g. interest rate swap CVA:
default prob, volatility

CVA calc:
https://www.gbm.hsbc.com/insights/markets/calculations-and-drivers-of-the-credit-valuation-adjustment
```
https://www.gbm.hsbc.com/insights/markets/calculations-and-drivers-of-the-credit-valuation-adjustment

```
CDS hazard rate and survival rate, and conditional unconditional再看一遍
```

```
CDS options pricing
on CDS spread: market spread + default spread = synthetic default spread as underlying
```

```
Martingale: 
stock price is no martingale because it has yeilds, if it has no yields it still have risk free rate discounting
so stock + borrow money (-risk free rate) combination is a martingale

discounted stock price is a martingale, mentioned here:
http://galton.uchicago.edu/~lalley/Courses/390/Lecture3.pdf
```

```

Using a Poisson Process to Model Default
We now assume the arrival of default follows a Poisson process9 with parameter λ so that P(τ ≤ t) = 1 − e−λt

http://www.columbia.edu/~mh2078/FoundationsFE/credit_models.pdf
```
http://www.columbia.edu/~mh2078/FoundationsFE/credit_models.pdf

```
Modelling Single-name and Multi-name Credit Derivatives
Book by Dominic O'Kane
 
first half
```

```
Credit Derivatives Pricing models
http://moulek.free.fr/Schonbucher.pdf
```


```
risk sensitivities: such as Credit DV01, RPV01 and IR

CS 01 (credit spread 01):
Defined as the change in the value of 100 notional amount of a CDS if the __CDS spread__ falls by one basis point.
CS01 captures the change in present value for a one basis point (1 bps) parallel upward shift in the underlying credit spread curve.
https://fincyclopedia.net/derivatives/c/cs01-risk

DV01 (dollar duration):
credit delta of a CDS is roughly equal to the DV01.
The change in the value of credit default swap (CDS) in reaction to a one basis point increase in the __underlying spread__
https://fincyclopedia.net/derivatives/c/credit-delta

RPV01 (risky present value, or risky-annuity):
其实就是Protection Leg PV = (1-R) SUM(hazard rate/lambda * surv prob * discount)
因为hazard rate未知, surv prob * discount已知, 所以RPV01就是预先计算好的surv prob * discount的结合

PV:
CDS.pv() = CDS premium * RPV01 - ProtectionLegPV

Par Spread:
how instruments quoted in the market

Par Spread VS quotes spread:
pars spreads are used to bootstrap a single hazard curve. Whereas quoted spreads have a flat hazard curve each (used to convert to an upfront amount)

bootstrap:
construct a discount curve:
start with the shortest maturity prd, solve for the discount factor at its maturity date, interpolation, move to the next longest maturity do it again
https://cran.r-project.org/web/packages/credule/vignettes/credule.html
```

https://readthedocs.org/projects/quantcred/downloads/pdf/latest/

![image](https://github.com/mincongzhang/Quant100Public/assets/5571030/870719ff-6da3-4dfb-971c-5f54123a6871)


![image](https://github.com/mincongzhang/Quant100Public/assets/5571030/0a2e39ec-62ec-435b-b5e0-57e4f0426d49)


```
analytics exp:
spherical harmonics and convolution
wavelet base wave and children wave, smooth the curve, quant trading
b-spline - interpolate the curve
kalman filter

fouries to spherical harmonics in hilbert space
https://en.wikipedia.org/wiki/Hilbert_space

bilaterial filter -> gaussian with steps -> convolution
```

------------------------------------------------------

```
lambda function recursion
```

```
visitor pattern
```

```
explicit template specialization

template in .h and .cpp
https://stackoverflow.com/questions/115703/storing-c-template-function-definitions-in-a-cpp-file
```

```
derivitive:
ln'(x)
[ln(ln(x))]'
integral of ln(x)? [xln(x)]' = ln(x) + 1 =>  [xln(x) - x]' = ln(x)
(e^x - 1 /x)what's the value when lim x->0  => 洛必达 e^x/1 when x=0, result = 1
used in piecewise constant harzard rate
Newton's method: x(n+1) = x(n)-f(xn)/f'(xn)
```

```
root finding:
https://zh.wikipedia.org/wiki/%E7%89%9B%E9%A1%BF%E6%B3%95
```
