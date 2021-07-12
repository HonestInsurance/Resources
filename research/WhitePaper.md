[<img src="https://github.com/HonestInsurance/Resources/blob/master/branding/HonestInsurance-hor-blue.png?raw=true" width="250">](https://www.honestinsurance.net)

-----------------------

**A subscription-based, self-governing, people-to-people insurance platform**

-----------------------

# 1. Problems worth solving

### Profiting from consumer loss

Insurance has become a very profitable industry generating $ 4.3 trillion (USD) in premiums in 2010 (1). However, if any profit has been reinvested, it’s clearly not resulting in equivalently strong outcomes for consumers.

### A lack of transparency

Only about 50% to 60% of the premiums are used for claim settlements (2). Consumers are often never informed about how the rest of their premiums are used. The reasoning behind premium calculations isn’t disclosed.

### Encouraging the purchase of unsuitable products

Aggressive advertising often aims to sell insurance products regardless of their suitability for a customer. As a result, more risk averse customers end up purchasing policies they may not require or multiple policies covering the same or a similar risk.

### Complicated, discouraging claims processes

Paying out insurance claims is the major cost to an insurance provider, a profit-maximization approach encourages insurance companies to delay the process or make it cumbersome. Often the fear of an irreversibly increased premium is enough to discourage even making a claim, which can leave consumers wondering why they have insurance in the first place.

### Claims adjusters incentivized to deny claims

A classic conflict of interest situation is found with claims adjusters who find themselves between the consumer who needs them and the company who pays them. The pressures of life ultimately lean toward staying gainfully employed, as we prefer not to bite the hand that feeds us, which leaves the consumers to get bitten.

### Insurance fraud & customers revolt 

According to the Insurance Information Institute, the financial impact caused by fraud now accounts for between 5 to 20 percent of the total claims’ costs. To make matters worse, this number is expected to increase (2). Research in the field of behavioral economics suggests that Consumers use unfair practices performed by the insurance industry as an argument to justify their own unethical behavior (5).

This paper proposes an alternative model of insurance that addresses the issues by leveraging opportunities Blockchain (6) (7) (8) has to offer.

### Further instructions
A list of abbreviations and acronyms used in this paper is presented at the end. Formulas outlined in this paper use the structure as shown below. The information presented within cornered brackets [ ] shows the unit (e.g. days, hours, minutes, points, %, Currency, etc.)  


Some formulas use the expression of ‘+=’ or ‘-=’.


# 2. An alternative insurance model – Insurance Pools

A conceptual overview of the proposed insurance pool model is presented in the diagram below. 

**Liquidity Providers** provide funds by purchasing insurance pool bonds and depositing the bond’s principal into the insurance pool’s **Funding Account**. The Funding Account’s balance is used to fund the various insurance pool expenditures such as:

* **Pool Operators** – Responsible for maintaining and running the insurance pool
* **Trust (Owners)** – Legal owners of the insurance pool
* **Claim Adjusters** – Handle and resolve claims logged by the Consumers
* **Suppliers** – Rectify the damage that was caused by an event
* **Cash Settlements** – In certain claim situations the Consumer is credited an agreed amount to rectify the claim-related damage themselves.

**Consumers** pay at an interval of their choosing (daily, weekly, fortnightly, monthly, etc.) their insurance premiums into the **Premium Account**. As the name suggests this account serves the purpose of holding the consumers’ premiums until these are consumed by the insurance pool. If a consumer cancels a policy, the policy’s unconsumed premiums are refunded from this account as well. All the funds held in this account are still ‘owned’ by the consumers.

Daily, the Insurance Pool charges the consumers today’s combined premium by transferring the corresponding amount from the **Premium Account** to the **Bond Account**. The Bond Account’s funds in turn are used to reimburse the **Liquidity Providers** for providing funds (purchasing bonds) at the bond’s maturity (principal plus yield).

Consumers can join and leave the insurance pool at their choosing. In addition, Consumers can have multiple insurance policies active in the same pool – each policy being independent from the others.

A more granular discussion of the components required by the proposed insurance pool model is presented next.

# 3. Working Capital (WC)

WC refers to the monetary assets of the insurance pool. These assets are available in accounts (e.g. a bank account), are denominated in currency units [ cu ] (e.g. EUR 150 cu ⪮ EUR 1.50 ⪮ 150 EURO cents) and are used to meet the insurance pool’s financial obligations.

## Working Capital Balance (WC<sub>Bal</sub>)

WC<sub>Bal</sub> refers to the account balance of Funding Account at any given point in time and can only be positive.

## Working Capital Expenditures (WC<sub>Exp</sub>)

The proposed model utilizes historic expenses to make a prediction about the insurance pool’s ‘near’ future expenses. These historical daily expenses of running the insurance pool can be calculated with ‘n’ being the number of days in the past that are considered.

〖WC〗_Exp=(∑_0^n▒〖(Insurance Pool Expenditures)〗)/n      ...     [cu/day]

In selecting an appropriate value for ‘n’ two aspects must be considered:

1. The influence of one or more significant events in the time period being considered
2. The influence of the distant past on the present.

Hence, if ‘n’ is chosen too narrowly, a substantial (or in other words costly) single claim has a disproportionate influence on WC<sub>Exp</sub>. On the other hand, a very broadly chosen ‘n’ places too much emphasis on the past in predicting the future (this is particularly an issue when the pool experiences strong growth or contraction phases).

WC<sub>Exp</sub> accounts only for actual costs that are settled from the funding account. As a result, Locked Working Capital (WC<sub>Locked</sub>) is not considered in this calculation.

## Working Capital Locked (WC<sub>Locked</sub>)

Due to sometimes significant time gaps between claim incidents and their settlements, WC<sub>Locked</sub> is used in this model to account for these future liabilities (accrued liabilities are created). The purpose of these accruals is to capture expected future expenditures in a timely fashion, allowing the model to respond more quickly to a changing environment.

〖WC〗_Locked=∑_0^m▒〖(〖Estimated claim liability〗_m)〗    …  [cu]

‘m’ represents the total number of claims for which an accrual has been established. Note: Establishing an accrual for a claim should be considered an exception to the rule and not the default operating procedure, the exception being if:

1. A single claim may result in significant financial liability for the insurance pool.
2. An event (e.g. natural disaster) causes many individual claims that may result in a significant liability for the insurance pool. Note: In this case, accruals are still created on a claim-by-claim basis (i.e. many individual accruals for a single event).

If an accrual has been established for a claim, this liability will be removed from WC<sub>Locked</sub> at claim settlement.

## Working Capital Time (WC<sub>Time</sub>)

A key metric on which the health of the insurance pool can be assessed is the duration in days WC<sub>Bal</sub> is able to cover anticipated claim payments without having any additional contributions made to it. This metric is called Working Capital Time (WC<sub>Time</sub>) and can be calculated as follows:

〖WC〗_Time=(〖WC〗_Bal-〖WC〗_Locked)/〖WC〗_Exp       …    [ Day ]

Since WC<sub>Locked</sub> is included in this formula, WC<sub>Time</sub> can also be a negative value. This would mean that WC<sub>Bal</sub> is insufficient to cover the anticipated claims represented by WC<sub>Locked</sub> causing the insurance pool to be in debt. However, the insurance pool remains solvent as long as WC<sub>Bal</sub> is able to fund ongoing WC<sub>Exp</sub>.

## Working Capital Target Time (WC<sub>TargetTime</sub>)

WC<sub>TargetTime</sub> represents the most important constant to be defined in this model for any given insurance pool. The proposed model’s single objective is to maintain its solvency by making WC<sub>Time</sub> match WC<sub>TargetTime</sub> (neither more nor less).

A thorough discussion on defining the Target Time for any given insurance pool would go beyond the scope of this paper. However, independent of any particular pool category, defining the Target Time requires understanding and optimizing the relationship between Capital Costs per Unit (CCU) and Trust.

1. Capital Costs per Unit (CCU) of Working Capital deployed in the bank account as WC<sub>Bal</sub> is the rate of return Liquidity Providers demand as compensation for providing liquidity and represent the costs of financing the insurance pool.
2. Trust in the insurance pool by all its stakeholders. Trust can be defined as the extent to which the insurance pool stakeholders believe in the enduring solvency of the pool.
3. Balancing CCU with Trust may be difficult as these two are interdependent with each other. A selected few qualitative factors that may impact the trust in the enduring solvency of the pool are:
   * Financial strength of the insurance pool
   * Strength of the insurance pool community among its members. Do the insurance Consumers remain loyal to the pool if insurance premiums increase due to the misfortune of some of their fellow Consumers?
   * Perceived impact of a maximum credible accident on the insurance pool
   * Transparency of the operations performed by the insurance pool stakeholders
   * Perceived honesty of the insurance pool stakeholders
   * Legislative uncertainties and impediments imposed on the insurance operations

From a quantitative point of view, the optimum WC<sub>TargetTime</sub> can be defined as the time at which the Capital Costs per Unit (CCU) are at a minimum so that the insurance pool can source its liquidity at a discount. CCU are the sum of two components:

1. Interest (CCU<sub>Interest</sub>) – This represents the expected return for a near risk-free investment (the expected return for providing the capital). A benchmark for this interest rate may be government bonds or the interest on bank cash deposits (i.e. interest on near risk-free investments).
2. Risk premium (CCU<sub>Risk</sub>) represents the return Liquidity Providers demand for accepting risks that are associated with their investment. The trust in the enduring solvency of the insurance pool with the qualitative factors outlined earlier (plus those that are missing) may have a significant impact on the risk premiums demanded by the Liquidity Providers.

The diagram below displays the anticipated Risk premium (CCU<sub>Risk</sub>), the Interest(CCU<sub>Interest</sub>) and the Total markup (CCU<sub>Total</sub>) as the sum of CCU<sub>Risk</sub> and CCU<sub>Interest</sub> in relation to WC<sub>Time</sub>.

The assumption for the CCU<sub>Risk</sub> component is that an increasing WC<sub>Time</sub> also causes WC<sub>Bal</sub> to grow. As a result, it can be assumed that the Liquidity Providers’ confidence in the solvency of the pool grows as greater financial strength enables the pool to withstand disruptive events more easily. Due to this perceived lower risk, Liquidity Providers may accept a lower CCU<sub>Risk</sub> in return.

The qualitative nature of the CCU<sub>Risk</sub> graph displayed above shows that Liquidity Providers are more sensitive to a change in WC<sub>Time</sub> when WC<sub>Time</sub> is low, as a change by one unit (day) causes a greater percentage change in WC<sub>Bal</sub> compared to a higher WC<sub>Time</sub> (see scenarios below).

```
Scenario 1: WCTime increases from 1 to 2 days ➔ WCBal grows by 100%.
Scenario 2: WCTime increases from 50 to 51 days ➔ WCBal grows by 2%.
```

Finally, a very high WC<sub>Time</sub> (and WC<sub>Bal</sub>) may provide Liquidity Providers with such confidence that they do not demand any risk compensation at all (CCU<sub>Risk</sub> = 0).

The Risk premium (CCU<sub>Risk</sub>) in the context of WC<sub>Time</sub> can be calculated as follows:

〖CCU〗_Risk (x)=〖a*x〗^b+c     …    [ % ]

The interest component (CCUInterest) in relation to WCTime is considered to be a linear function in which Liquidity Providers demand a fixed daily return for providing the funds. As a result, CCUInterest is the product of the demanded daily return and the duration (WCTime):

〖CCU〗_Interest (x)=d*x     …    [ % ]

CCUTotal can be calculated as the sum of CCURisk and CCUInterest.

〖CCU〗_Total (x)=〖CCU〗_Risk (x)+ 〖CCU〗_Interest (x)     …    [ % ]

The ideal WCTargetTime can now be calculated by finding a minimum for CCUTotal:

 〖WC〗_TargetTime=(〖CCU〗_Risk (x)+ 〖CCU〗_Interest (x))     …    [ day ]

Mathematically, we can conclude:

0= 〖CCU〗_Total'(x)
0= 〖CCU〗_Risk'(x)+ 〖CCU〗_Interest'(x)  
0= 〖a*b* x〗^(b-1)+ d
〖WC〗_TargetTime=√(b-1&(-d)/(a*b))    …    [ Day ]

Demand of Working Capital (WCDelta)

In comparing WCTargetTime with the current WCTime, the demand for additional WC required can be expressed as

〖WC〗_Delta= 〖(WC〗_TargetTime-〖WC〗_Time)*〖WC〗_Exp    …    [cu]

A positive value for WCDelta describes the demand for additional liquidity required to match WCTime with WCTargetTime. A negative value for WCDelta indicates that the insurance pool is over funded and no additional liquidity is required at this point in time.
