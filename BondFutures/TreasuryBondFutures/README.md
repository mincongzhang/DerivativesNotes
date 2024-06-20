### Terms

#### Accrued interest

Accrued interest: refers to the accumulated coupon interest on a bond that the buyer pays to the seller

```
The buyer pays the seller accrued interest because it compensates the seller for the interest that has accrued on the bond since the last coupon payment date.
 When a bond is traded between interest payment dates, the buyer is responsible for paying the seller the interest that has accumulated up to that point.
This ensures a fair exchange and reflects the bond’s value accurately. 
```

```
If a bond is bought or sold at a time other than those two dates each year, the purchaser will have to tack onto the sales amount any interest accrued since the previous interest payment.
The new owner will receive a full 1/2 year interest payment at the next payment date. Therefore, the previous owner must be paid the interest that accrued prior to the sale.
```

![image](https://github.com/mincongzhang/BHNotes/assets/5571030/a68c34a2-3916-4eea-b4f3-a4195eb2b39c)


https://www.investopedia.com/terms/a/accruedinterest.asp

#### Conversion factor

The conversion factor is used to equalize coupon and accrued interest differences of all delivery bonds. 

## Day Count and Quotation Conventions
### Day counts

- Actual/actual(in period): used for Treasury bonds in the US.
- 30/360: used for corporate and municipal bonds
- actual/360: used for money market instruments in the US. (The money market is defined as dealing in debt of less than one year.)

### Price Quotations of US Treasury Bonds

- clean price: quoted price, is not the same as the cash price (__so what is it?__)
- dirty price: cash price paid by the purchaser

$$Cash \ Price = Quoted \ Price(Clean \ Price) + Accrued \ interest \  since \ last \ coupon \ date$$


## Treasury Bond Futures

### Conversion Factors
The Treasury bond futures contract allows the party with the short position(seller) to choose to deliver any bond that has a maturity between 15 and 25 years. 

When a particular bond is delivered, a parameter known as its __conversion factor__ defines __the price received for the bond__ by the party with the short position(seller).

The applicable quoted price for the bond delivered is the product of the conversion factor and the most recent settlement price for the futures contract. 

$$Bond \ Cash \ Price = (Most \ Recent \ Future \ Settlement \ Price \times Conversion \ Factor) + Accrued \ Interest$$

```
Settlement Price是Futures的Price. 但是对应的Bond因为有不同的coupon和不同的Day Count, 所以其中需要Conversion Factor来给他们归一化到Future Price
```

### Example 1
A Bond, assumed to have exactly 20 years to maturity: 

- 10% coupon (semiannual, i.e. 5% per 6 months)
- 20 years to maturity (i.e. 40*6 months)
- discount rate is 6% per annum with semiannual compounding (3% per 6 months)
- Face value is $100

$$Discounted \ Total \ Coupons = \sum_{n=1}^{40} \frac{5}{1.03^i}$$

$$Discounted \ Face \ Value = \frac{100}{1.03^{40}}$$

$$Discounted \ Total \ Bond \ Value = Discounted \ Total \ Coupons + Discounted \ Face \ Value = \sum_{n=1}^{40} \frac{5}{1.03^i} + \frac{100}{1.03^{40}} = 146.23$$

$$Accrued \ Interest = 0$$

From what we have known:

$$Bond \ Cash \ Price = (Most \ Recent \ Future \ Settlement \ Price \times Conversion \ Factor) + Accrued \ Interest$$

$$Conversion \ Factor = \frac {Bond \ Clean \ Price - Accrued \ Interest} {Most \ Recent \ Future \ Settlement \ Price} $$

$$Conversion \ Factor = \frac{Discounted \ Total \ Bond \ Value - 0}{FaceValue} = 1.4623$$

### Example 2

A Bond, assumed to have 18 years and 3 months to maturity: 

- 8% coupon (semiannual, i.e. 4% per 6 months)
- 18 years and 3 months to maturity (i.e. 36*6 months + 3 months)
- discount rate is 6% per annum with semiannual compounding (3% per 6 months)
- Face value is $100

Discounting in time 3 months from today:

$$Coupon \ 3 \ months \ later \ from \ today = 4$$ 

$$Discounted \ Total \ Coupons = \sum_{n=1}^{36} \frac{4}{1.03^i}$$

$$Discounted \ Face \ Value = \frac{100}{1.03^{36}}$$

$$Discounted \ Total \ Bond \ Value = Coupon + Discounted \ Total \ Coupons + Discounted \ Face \ Value =  4 + \sum_{n=1}^{36} \frac{4}{1.03^i} + \frac{100}{1.03^{36}} = 125.83$$


![image](https://github.com/mincongzhang/BHNotes/assets/5571030/ee5ecaf6-a32e-4424-8fd2-101631061f47)

Because we have discount rate is 6% per annum with semiannual compounding (3% per 6 months):

$$1 \ year \ yield = 1.03^2$$

$$6 \ months \ yield = 1.03$$

$$3 \ months \ yield = \sqrt{1.03}$$

$$3 \ months \ interest = \sqrt{1.03} - 1 = 1.4889\\%$$

$$Total \ Bond \ Value \ discounted \ to \ today = 125.83/(1+1.4889\\%) = 123.99$$


$$3 \ months \ accrued \ interest = 4/2 = 2$$

From what we have known:

$$Bond \ Cash \ Price = (Most \ Recent \ Future \ Settlement \ Price \times Conversion \ Factor) + Accrued \ Interest$$

$$Conversion \ Factor = \frac {Bond \ Clean \ Price - Accrued \ Interest} {Most \ Recent \ Future \ Settlement \ Price} $$

$$Conversion \ Factor = \frac{Total \ Bond \ Value \ discounted \ to \ today - Accrued \ Interest}{FaceValue} = \frac{ 123.99 - 2 }{ 100 } = 1.2199 $$


## Cheapest-to-Deliver Bond

The seller can choose which of the available bonds is "cheapest" to deliver. 

The seller can receive bond cash price:

$$Seller \ Received \ Bond \ Cash \ Price = (Most \ Recent \ Future \ Settlement \ Price \times Conversion \ Factor) + Accrued \ Interest$$

And the cost of purchasing a bond is:

$$Market \ Bond \ Cash \ Price = \ Quoted \ bond \ price (Clean \ price) + Accrued \ interest$$

the cheapest-to-deliver bond is the least in:

$$\ Quoted \ bond \ price (Clean \ price) -  (Most \ Recent \ Future \ Settlement \ Price \times Conversion \ Factor) $$

### Example

Assume the most recent future settlement price is 93-08, or 93.25.


![image](https://github.com/mincongzhang/BHNotes/assets/5571030/81d04d81-a0b6-461e-84a9-525dfd6bb28a)

![image](https://github.com/mincongzhang/BHNotes/assets/5571030/e97737ac-6d07-49c6-8235-660322ffb90f)

## Determining the Futures Price

Assume:
- the cheapest-to-deliver bond and the delivery date are known
- the Treasury bond futures contract is a futures contract on a traded security (the bond) that provides
the holder with known income

Futures price:

$$F_0 = (S_0-I) e^{rT}$$

$F_0$: future price

$S_0$: spot price

$I$: PV of the coupons during the life of the futures contract

$T$: time to maturity

### Example
In a Treasury bond futures contract, what we know:

- The cheapest-to-deliver bond: 12% coupon bond(semiannual), conversion factor 1.6
- delivery will take place in 270 days
- the last coupon date was 60 days ago
- the next coupon date is in 122 days
- the coupon date thereafter is in 305 days
- The term structure is flat
- rate: 10% per annum, continuous compounding
- bond price quoted: $115


![image](https://github.com/mincongzhang/BHNotes/assets/5571030/934228e3-d31f-43e6-ad2f-25f961d75484)


__Calculate cash price__ $S_0$: 

$$Cash \ Price = Quoted \ Price(Clean \ Price) + Accrued \ interest \  since \ last \ coupon \ date$$

Accrued interest:
$$\frac{60}{60+122} \times 12\\% \times 0.5 = 1.978$$

![image](https://github.com/mincongzhang/BHNotes/assets/5571030/e2ae74c4-57ae-4272-8408-6cce9708a221)


Quoted bond price (clean price): 115

__Bond Cash price__ $S_0$: 115 + 1.978 = 116.978

__Calculate coupon PV__ $I$:

A coupon of $6 will be received after 122 days (122/365=0.3342 years). 

__Coupon PV__ $I$:

$$6e^{-0.1 \times 0.3342} = 5.803$$

![image](https://github.com/mincongzhang/BHNotes/assets/5571030/7275ee31-fa48-4215-a2af-52e21d902e3d)


__Calculate cash futures price__ $F_0$:

$$F_0 = (S_0-I) e^{rT}$$

The futures contract lasts for 270 days: $T =270/365=0.7397$

The cash futures price, if the contract were written on the 12% bond:

$$F_0 = (S_0-I) e^{rT} = (116.978 - 5.803) e^{0.1 \times 0.7397} = 119.711$$

![image](https://github.com/mincongzhang/BHNotes/assets/5571030/925ba444-ec16-4bd7-8675-b255fb634350)


__Subtracting the accrued interest__:

At delivery, there are 148 days of accrued interest.

The quoted futures price needs to subtract the accrued interest. 

$$119.711 - 6 \times \frac{148}{148+35} = 114.859$$

![image](https://github.com/mincongzhang/BHNotes/assets/5571030/563e7f2c-0c65-402e-a049-6b9948cb94ec)


__Use Conversion Factor__:

From the definition of the conversion factor, 1.6000 standard bonds are considered equivalent to each 12% bond. The quoted futures price should therefore be:

$$\frac{114.859}{1.6} = 71.79$$
