![image](https://github.com/mincongzhang/Quant100Public/assets/5571030/7157e122-9585-46b4-b805-d5444fa8926c)


### CVA component 1: Probability of Default (PD)

1. Not a single value, usually a term structure
2. Can be calculated from CDS: CDS market price of different contract tenors -> put back to CDS pricing model -> implied a term structure of default probabilities

### CVA component 2: Loss Given Default (LGD)

the loss to creditors is not necessarily the full exposure as some portion might be recovered from the defaulting counterparty

1. LGD = (1-Recovery rate)

### CVA component 3: Expected Positive Exposure (EPE)

The exposure to a derivatives counterparty can vary significantly over the life of a transaction, with the nature of the derivative product being an important factor in understanding how much exposure is potentially at risk should the counterparty default. Therefore, it is those exposures that hold a positive mark-to-market (MTM) that are relevant (that is, where the derivative counterparty has an obligation to the corporate at the time of default). 

https://www.gbm.hsbc.com/insights/markets/calculations-and-drivers-of-the-credit-valuation-adjustment
