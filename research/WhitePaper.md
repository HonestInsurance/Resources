[<img src="https://github.com/HonestInsurance/Resources/blob/master/branding/HonestInsurance-hor-blue.png?raw=true" width="250">](https://www.honestinsurance.net)

---

**A subscription-based, self-governing, people-to-people insurance platform**

---

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

---

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

---

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

The interest component (CCU<sub>Interest</sub>) in relation to WC<sub>Time</sub> is considered to be a linear function in which Liquidity Providers demand a fixed daily return for providing the funds. As a result, CCU<sub>Interest</sub> is the product of the demanded daily return and the duration (WC<sub>Time</sub>):

〖CCU〗_Interest (x)=d*x     …    [ % ]

CCU<sub>Total</sub> can be calculated as the sum of CCU<sub>Risk</sub> and CCU<sub>Interest</sub>.

〖CCU〗_Total (x)=〖CCU〗_Risk (x)+ 〖CCU〗_Interest (x)     …    [ % ]

The ideal WC<sub>TargetTime</sub> can now be calculated by finding a minimum for CCU<sub>Total</sub>:

 〖WC〗_TargetTime=(〖CCU〗_Risk (x)+ 〖CCU〗_Interest (x))     …    [ day ]

Mathematically, we can conclude:

0= 〖CCU〗_Total'(x)
0= 〖CCU〗_Risk'(x)+ 〖CCU〗_Interest'(x)  
0= 〖a*b* x〗^(b-1)+ d

〖WC〗_TargetTime=√(b-1&(-d)/(a*b))    …    [ Day ]

Demand of Working Capital (WC<sub>Delta</sub>)

In comparing WC<sub>TargetTime</sub> with the current WC<sub>Time</sub>, the demand for additional WC required can be expressed as

〖WC〗_Delta= 〖(WC〗_TargetTime-〖WC〗_Time)*〖WC〗_Exp    …    [cu]

A positive value for WC<sub>Delta</sub> describes the demand for additional liquidity required to match WC<sub>Time</sub> with WC<sub>TargetTime</sub>. A negative value for WC<sub>Delta</sub> indicates that the insurance pool is over funded and no additional liquidity is required at this point in time.

---

# 4. Liquidity Providers and Insurance Pool Bonds (Bond)

Liquidity Providers **invest** in the insurance pool by 

* Purchasing Insurance Pool Bonds issued by the pool and 
* Transferring the Principal of the Bond into the insurance pool’s Funding Account. 

A Liquidity Provider can be any natural person of eligible age or a legal entity that is permitted to engage in commercial activity within the jurisdiction of the insurance pool’s locality.

## Working Capital Transit (WC<sub>Transit</sub>)

Due to a delay in a bond being issued and the corresponding principal being credited to the insurance pool’s bank account, the variable WC<sub>Transit</sub> is used to capture the sum of all the Bonds’ principal in transit.

Bond B issued:    〖WC〗_Transit  +=〖Bond〗_Principal    …    [cu]
Bond B credited:    〖WC〗_Transit  -=〖Bond〗_Principal    …    [cu]

When the Liquidity Provider fails to deposit the principal within the Bond Payment Period, the Bond contract is voided and the corresponding WCTransit is removed as well.

Bond B voided:    〖WC〗_Transit  -=〖Bond〗_Principal    …    [cu]

To encourage Liquidity Providers to deposit the principal and fulfil their contractual obligations, Liquidity Providers need to provide a security valued at 10% of the value of the Bond’s principal. If a Liquidity Provider fails to deposit the principal, the ownership of the security transfers to the insurance pool. Two options are proposed to provide this security:

1. Deposit 10% of the bond’s principal into the Funding Account.
2.  Reference an existing insurance pool bond
    * Whose principal amount has already been credited
    * That does not expire (reach maturity) within the Bond Payment Period
    * That is currently not being used as a reference for another bond.

As stated earlier, when the principal does not get credited within the Bond Payment Period, the ownership of the referenced insurance bond transfers to the insurance pool (i.e. the owner of the bond forfeits a percentage of the bond’s principal including its yield). If the principal is credited within the time limit, the hold on the bond is removed.

## Working Capital Bond (WC<sub>Bond</sub>)

Taking WC<sub>Transit</sub> into account, the actual demand for new capital (WC<sub>Bond</sub>) to be acquired by the insurance pool through issuing bonds can be calculated as follows:

〖WC〗_Bond= 〖WC〗_Delta-〖WC〗_Transit    …    [cu]

In purchasing Bonds, the following bond constraints and clauses apply to Liquidity Providers.

## Bond Principal

The combined principal of all Bonds on sale is limited and defined by WC<sub>Bond</sub>. If WC<sub>Bond</sub> is zero or negative, no bonds are available for purchase. Otherwise, Liquidity Providers can choose any desired principal amount as long as the principal is equal to or lesser than WCBond. In addition, Liquidity Providers can purchase a multitude of Bonds.

## Bond Maturity

The maturity of any Bond is a constant and defined by WC<sub>TargetTime</sub>. No bonds with a maturity unequal to WC<sub>TargetTime</sub> are offered.

## Bond Yield (Yield to Maturity)

The actual yield Liquidity Providers can expect from a bond (BondYield) is the result of supply and demand market forces. This model proposes a dynamic way of adjusting the Yield and Gradient for the bonds on offer.  An escalator will be used to illustrate the concept of adjusting the Yield and Gradient.
The properties of the escalator are: 

The number of steps on the escalator equals WC<sub>Bond</sub> (one step for every unit of cu currency – e.g. $ 10 results in 10 steps). Figure 1 displays an escalator with 8 steps ➔ WC<sub>Bond</sub> = 8.
At the beginning, the steps are distributed evenly from the top to the bottom step just like a normal escalator (see Figure 1). Yield refers to the yield of the top step on the escalator (the yield of the highest selling unit of WCBond on offer). Gradient describes the step-by-step decrease in yield starting from the top step’s yield.

The steps are moving together at the same speed just like a normal escalator. Figure 2 displays this scenario in which the Yield (yield of the top step) moves from 6% to 7.5%. In addition, all the remaining steps’ yield has increased by the same delta of 1.5%. 
All steps on the escalator accelerate vertically at the same rate by multiplying the Yield with a Yield Acceleration Constant (YAC) on a minute by minute basis. In Figure 2, the Yield is at 7.5%. Hence, the escalator accelerates at the rate of (1 + 7.5%) multiplied by YAC.
The height of the ground of any step represents the yield this step holds. (e.g. in Figure 2 the top step’s yield is 9%, while the bottom step’s yield is at 3% with the remaining steps distributed evenly).

Liquidity Providers purchase any number of steps on the escalator starting from the top downward. As a result, the combined bond’s yield (BondYield) is the average of the steps’ yield purchased. In Figure 3, a Liquidity Provider purchased three steps. Hence, the bond’s combined yield is the average of all the steps’ yield purchased ([7.5% + 6.75% + 6%] / 3 ➔ BondYield = 6.75%).

When an updated demand for liquidity is calculated by the insurance pool (new value for WC<sub>Delta</sub> and WC<sub>Bond</sub>), the escalator gets a reset with WC<sub>Bond</sub> steps being redistributed evenly from the last Yield value (before the reset) to a yield of zero. If WC<sub>Bond</sub> is zero or negative, no steps are available for purchase from the escalator. 

Such a reset is illustrated in Figure 4 with a new WC<sub>Bond</sub> of 12, a Yield of 5.25% (equals Yield before the reset), and the steps being redistributed equally.

## Re-initialization of WCBond, Yield and Gradient

At periodic intervals, a new demand for WC<sub>Delta</sub> is calculated by the insurance pool. This event in turn triggers a recalculation of WC<sub>Bond</sub>, Yield and Gradient which are referenced by the process of issuing new Bonds.

First, a new value for WC<sub>Bond</sub> is calculated by using the previous formula 

〖WC〗_Bond= 〖WC〗_Delta-〖WC〗_Transit    …    [ cu ]

Yield (Yield of the top step) remains at the same value. If no value has been defined in the past, a value of 1% is chosen as its initial value.
Finally, the Gradient can be recalculated by

Gradient=  Yield/〖WC〗_Bond     …    [ % ]

## Acceleration of Yield

The Yield of the insurance pool accelerates at a discrete interval of one minute. However, this increase is executed only if WC<sub>Bond</sub> exceeds a minimum threshold of 10% of WC<sub>Exp</sub>.

Yield= Yield*(1+YAC [% per minute])  |  〖WC〗_Bond>〖WC〗_Exp*10%

The reasoning for this 10% threshold is twofold. First, the resources consumed on a minute-by-minute basis to increase the Yield in comparison to the outstanding WCBond volume may not justify its operations.

Second, and more importantly, a small value for WC<sub>Bond</sub> may not make it worthwhile to any Liquidity Provider to purchase a bond with the remaining WC<sub>Bond</sub> as its principal. This would potentially cause the Yield to increase to a very high value. When a reinitialization occurs and a higher WC<sub>Bond</sub> demand is on offer, a significant portion of this WC<sub>Bond</sub> becomes available at an unjustifiably high Yield.

The implications in choosing an appropriate value for YAC are as follows:

Double Value Time represents the duration it would take the Yield to increase by a factor of two (i.e. to double in value). Hence, this duration determines the insurance pool’s ability to respond to a changing environment in which Liquidity Providers request a higher Yield.

Double Value Time=  (ln (2) )/(ln (1+YAC [% per hour]) )    …    [ hour ]

Turnover Rate refers to the time it would take to sell all the WC<sub>Bond</sub> under the condition that Liquidity Providers’ demanded Yield remains constant. This can be perceived as the speed at which WC<sub>Bond</sub> is being ‘sold’ to Liquidity Providers.

Turnover Rate=  1/(YAC [% per hour])    …    [ hour ]

The relationship between Double Value Time and Turnover Rate, depending on YAC, is shown in the diagram below. 
 
To obtain YAC on a per minute basis calculate 

YAC= √(60&YAC [% per hour]+1)-1   …    [ % per minute]

## Issuing of a new Insurance Pool Bond (Bond)

The terms of a newly issued Bond are as follows:

〖Bond〗_Principal= Liquidity Providers choosing  |  0<〖Bond〗_Principal≤〖WC〗_Bond    …    [ cu ]
〖Bond〗_Yield= Yield-  (Gradient * 〖Bond〗_Principal)/2    …    [ % ]
〖Bond〗_Maturity= 〖WC〗_TargetTime

Bond payment deadline=Bond Payment Period   …    [ hour ]

## Adjustment of WCBond and Yield

Upon the successful issue of a Bond, WCBond and Yield are adjusted:

〖WC〗_Bond  -=〖Bond〗_Principal
Yield -=Gradient*〖Bond〗_Principal

## Reimbursement of Liquidity Providers

At the time, a Bond matures, the Bond’s principal (BondPrincipal) plus yield (BondYield) are transferred back to the Liquidity Provider.

Bond payout amount= 〖[Bond〗_Principal*(1+〖Bond〗_Yield)]   …    [ cu ]

