[<img src="https://github.com/HonestInsurance/Resources/blob/master/branding/HonestInsurance-hor-blue.png?raw=true" width="250">](https://www.honestinsurance.net)

---

# Honest Insurance

**A subscription-based, self-governing, people-to-people insurance platform**

---

# 1. Problems worth solving

### Profiting from consumer loss

Insurance has become a very profitable industry generating $ 4.3 trillion (USD) in premiums in 2010 (1). However, if any profit has been reinvested, it's clearly not resulting in equivalently strong outcomes for consumers.

### A lack of transparency

Only about 50% to 60% of the premiums are used for claim settlements (2). Consumers are often never informed about how the rest of their premiums are used. The reasoning behind premium calculations isn't disclosed.

### Encouraging the purchase of unsuitable products

Aggressive advertising often aims to sell insurance products regardless of their suitability for a customer. As a result, more risk averse customers end up purchasing policies they may not require or multiple policies covering the same or a similar risk.

### Complicated, discouraging claims processes

Paying out insurance claims is the major cost to an insurance provider, a profit-maximization approach encourages insurance companies to delay the process or make it cumbersome. Often the fear of an irreversibly increased premium is enough to discourage even making a claim, which can leave consumers wondering why they have insurance in the first place.

### Claims adjusters incentivized to deny claims

A classic conflict of interest situation is found with claims adjusters who find themselves between the consumer who needs them and the company who pays them. The pressures of life ultimately lean toward staying gainfully employed, as we prefer not to bite the hand that feeds us, which leaves the consumers to get bitten.

### Insurance fraud & customers revolt

According to the Insurance Information Institute, the financial impact caused by fraud now accounts for between 5 to 20 percent of the total claims' costs. To make matters worse, this number is expected to increase (2). Research in the field of behavioral economics suggests that Consumers use unfair practices performed by the insurance industry as an argument to justify their own unethical behavior (5).

This paper proposes an alternative model of insurance that addresses the issues by leveraging opportunities Blockchain (6) (7) (8) has to offer.

### Further instructions

A list of abbreviations and acronyms used in this paper is presented at the end. Formulas outlined in this paper use the structure as shown below. The information presented within cornered brackets [ ] shows the unit (e.g. days, hours, minutes, points, %, Currency, etc.)

<img src="https://github.com/HonestInsurance/Resources/blob/master/research/formulas/ch1-img1.png?raw=true" width="500">

Some formulas use the expression of '+=' or '-='.

<img src="https://github.com/HonestInsurance/Resources/blob/master/research/formulas/ch1-img2.png?raw=true" width="700">
<img src="https://github.com/HonestInsurance/Resources/blob/master/research/formulas/ch1-img3.png?raw=true" width="700">

## 2. An alternative insurance model – Insurance Pools

A conceptual overview of the proposed insurance pool model is presented in the diagram below.

<img src="https://github.com/HonestInsurance/Resources/blob/master/diagrams/InsuranceModel.png?raw=true" width="600">

**Liquidity Providers** provide funds by purchasing insurance pool bonds and depositing the bond's principal into the insurance pool's **Funding Account**. The Funding Account's balance is used to fund the various insurance pool expenditures such as:

- **Pool Operators** – Responsible for maintaining and running the insurance pool
- **Trust (Owners)** – Legal owners of the insurance pool
- **Claim Adjusters** – Handle and resolve claims logged by the Consumers
- **Suppliers** – Rectify the damage that was caused by an event
- **Cash Settlements** – In certain claim situations the Consumer is credited an agreed amount to rectify the claim-related damage themselves.

**Consumers** pay at an interval of their choosing (daily, weekly, fortnightly, monthly, etc.) their insurance premiums into the **Premium Account**. As the name suggests this account serves the purpose of holding the consumers' premiums until these are consumed by the insurance pool. If a consumer cancels a policy, the policy's unconsumed premiums are refunded from this account as well. All the funds held in this account are still 'owned' by the consumers.

Daily, the Insurance Pool charges the consumers today's combined premium by transferring the corresponding amount from the **Premium Account** to the **Bond Account**. The Bond Account's funds in turn are used to reimburse the **Liquidity Providers'** for providing funds (purchasing bonds) at the bond's maturity (principal plus yield).

Consumers can join and leave the insurance pool at their choosing. In addition, Consumers can have multiple insurance policies active in the same pool – each policy being independent from the others.

A more granular discussion of the components required by the proposed insurance pool model is presented next.

## 3. Working Capital (WC)

WC refers to the monetary assets of the insurance pool. These assets are available in accounts (e.g. a bank account), are denominated in currency units [cu] (e.g. EUR 150 cu ⪮ EUR 1.50 ⪮ 150 EURO cents) and are used to meet the insurance pool's financial obligations.

### Working Capital Balance (WC<sub>Bal</sub>)

WC<sub>Bal</sub> refers to the account balance of Funding Account at any given point in time and can only be positive.

### Working Capital Expenditures (WC<sub>Exp</sub>)

The proposed model utilizes historic expenses to make a prediction about the insurance pool's 'near' future expenses. These historical **daily expenses** of running the insurance pool can be calculated with 'n' being the number of days in the past that are considered.

<img src="https://github.com/HonestInsurance/Resources/blob/master/research/formulas/ch2-img1.png?raw=true" width="500">

In selecting an appropriate value for 'n' two aspects must be considered:

1. The influence of one or more significant events in the time period being considered
2. The influence of the distant past on the present.

Hence, if 'n' is chosen too narrowly, a substantial (or in other words costly) single claim has a disproportionate influence on WC<sub>Exp</sub>. On the other hand, a very broadly chosen 'n' places too much emphasis on the past in predicting the future (this is particularly an issue when the pool experiences strong growth or contraction phases).

WC<sub>Exp</sub> accounts only for actual costs that are settled from the funding account. As a result, Locked Working Capital (WC<sub>Locked</sub>) is not considered in this calculation.

### Working Capital Locked (WC<sub>Locked</sub>)

Due to sometimes significant time gaps between claim incidents and their settlements, WC<sub>Locked</sub> is used in this model to account for these future liabilities (accrued liabilities are created). The purpose of these accruals is to capture expected future expenditures in a timely fashion, allowing the model to respond more quickly to a changing environment.

<img src="https://github.com/HonestInsurance/Resources/blob/master/research/formulas/ch2-img2.png?raw=true" width="500">

'm' represents the total number of claims for which an accrual has been established. Note: Establishing an accrual for a claim should be considered an exception to the rule and not the default operating procedure, the exception being if:

1. A single claim may result in significant financial liability for the insurance pool.
2. An event (e.g. natural disaster) causes many individual claims that may result in a significant liability for the insurance pool. Note: In this case, accruals are still created on a claim-by-claim basis (i.e. many individual accruals for a single event).

If an accrual has been established for a claim, this liability will be removed from WC<sub>Locked</sub> at claim settlement.

### Working Capital Time (WC<sub>Time</sub>)

A key metric on which the health of the insurance pool can be assessed is the duration in days WC<sub>Bal</sub> is able to cover **anticipated** claim payments without having any additional contributions made to it. This metric is called Working Capital Time (WC<sub>Time</sub>) and can be calculated as follows:

<img src="https://github.com/HonestInsurance/Resources/blob/master/research/formulas/ch2-img3.png?raw=true" width="500">

Since WC<sub>Locked</sub> is included in this formula, WC<sub>Time</sub> can also be a negative value. This would mean that WC<sub>Bal</sub> is insufficient to cover the anticipated claims represented by WC<sub>Locked</sub> causing the insurance pool to be in debt. However, the insurance pool remains solvent as long as WC<sub>Bal</sub> is able to fund ongoing WC<sub>Exp</sub>.

### Working Capital Target Time (WC<sub>TargetTime</sub>)

WC<sub>TargetTime</sub> represents the most important constant to be defined in this model for any given insurance pool. The proposed model's single objective is to maintain its solvency by making WC<sub>Time</sub> match WC<sub>TargetTime</sub> (neither more nor less).

A thorough discussion on defining the Target Time for any given insurance pool would go beyond the scope of this paper. However, independent of any particular pool category, defining the Target Time requires understanding and optimizing the relationship between **Capital Costs per Unit (CCU)** and **Trust.**

1. **Capital Costs per Unit (CCU) of Working Capital** deployed in the bank account as WC<sub>Bal</sub> is the rate of return Liquidity Providers demand as compensation for providing liquidity and represent the costs of financing the insurance pool.
2. **Trust** in the insurance pool by all its stakeholders. Trust can be defined as the extent to which the insurance pool stakeholders believe in the **enduring solvency** of the pool.
3. Balancing **CCU** with **Trust** may be difficult as these two are interdependent with each other. A selected few **qualitative** factors that may impact the **trust in the enduring solvency** of the pool are:

- Financial strength of the insurance pool
- Strength of the insurance pool community among its members. Do the insurance Consumers remain loyal to the pool if insurance premiums increase due to the misfortune of some of their fellow Consumers?
- Perceived impact of a maximum credible accident on the insurance pool
- Transparency of the operations performed by the insurance pool stakeholders
- Perceived honesty of the insurance pool stakeholders
- Legislative uncertainties and impediments imposed on the insurance operations

From a **quantitative** point of view, the optimum WC<sub>TargetTime</sub> can be defined as the time at which the Capital Costs per Unit (CCU) are at a minimum so that the insurance pool can source its liquidity at a discount. CCU are the sum of two components:

1. **Interest (CCU****Interest****)** – This represents the expected return for a near risk-free investment (the expected return for providing the capital). A benchmark for this interest rate may be government bonds or the interest on bank cash deposits (i.e. interest on near risk-free investments).
2. **Risk premium (CCU****Risk****)** represents the return Liquidity Providers demand for accepting risks that are associated with their investment. The **trust in the enduring solvency of the insurance pool** with the qualitative factors outlined earlier (plus those that are missing) may have a significant impact on the risk premiums demanded by the Liquidity Providers.

The diagram below displays the anticipated Risk premium (CCU<sub>Risk</sub>), the Interest(CCU<sub>Interest</sub>) and the Total markup (CCUTotal) as the sum of CCU<sub>Risk</sub> and CCU<sub>Interest</sub> in relation to WC<sub>Time</sub>.

<img src="https://github.com/HonestInsurance/Resources/blob/master/research/diagrams/CaptialCostPerUnit-of-WorkingCaptial.png" width="800">

The assumption for the CCU<sub>Risk</sub> component is that an increasing WC<sub>Time</sub> also causes WC<sub>Bal</sub> to grow. As a result, it can be assumed that the Liquidity Providers' confidence in the solvency of the pool grows as greater financial strength enables the pool to withstand disruptive events more easily. Due to this perceived lower risk, Liquidity Providers may accept a lower CCU<sub>Risk</sub> in return.

The qualitative nature of the CCU<sub>Risk</sub> graph displayed above shows that Liquidity Providers are more sensitive to a change in WC<sub>Time</sub> when WC<sub>Time</sub> is low, as a change by one unit (day) causes a greater percentage change in WC<sub>Bal</sub> compared to a higher WC<sub>Time</sub> (see scenarios below).

###### Scenario 1: WC<sub>Time</sub> increases from 1 to 2 days ➔ WC<sub>Bal</sub> grows by 100%.

###### Scenario 2: WC<sub>Time</sub> increases from 50 to 51 days ➔ WC<sub>Bal</sub> grows by 2%.

Finally, a very high WC<sub>Time</sub> (and WC<sub>Bal</sub>) may provide Liquidity Providers with such confidence that they do not demand any risk compensation at all (CCU<sub>Risk</sub> = 0).

The Risk premium (CCU<sub>Risk</sub>) in the context of WC<sub>Time</sub> can be calculated as follows:

<img src="https://github.com/HonestInsurance/Resources/blob/master/research/formulas/ch2-img4.png?raw=true" width="500">


The interest component (CCU<sub>Interest</sub>) in relation to WC<sub>Time</sub> is considered to be a linear function in which Liquidity Providers demand a fixed daily return for providing the funds. As a result, CCU<sub>Interest</sub> is the product of the demanded daily return and the duration (WC<sub>Time</sub>):

<img src="https://github.com/HonestInsurance/Resources/blob/master/research/formulas/ch2-img5.png?raw=true" width="500">

CCUTotal can be calculated as the sum of CCU<sub>Risk</sub> and CCU<sub>Interest</sub>.

<img src="https://github.com/HonestInsurance/Resources/blob/master/research/formulas/ch2-img6.png?raw=true" width="500">

The ideal WC<sub>TargetTime</sub> can now be calculated by finding a minimum for CCUTotal:

<img src="https://github.com/HonestInsurance/Resources/blob/master/research/formulas/ch2-img7.png?raw=true" width="500">

Mathematically, we can conclude:

######


######


######


######


### Demand of Working Capital (WC<sub>Delta</sub>)

In comparing WC<sub>TargetTime</sub> with the current WC<sub>Time</sub>, the demand for additional WC required can be expressed as

######


A positive value for WC<sub>Delta</sub> describes the demand for additional liquidity required to match WC<sub>Time</sub> with WC<sub>TargetTime</sub>. A negative value for WC<sub>Delta</sub> indicates that the insurance pool is over funded and no additional liquidity is required at this point in time.

##


## 4. Liquidity Providers and Insurance Pool Bonds (Bond)

Liquidity Providers **invest** in the insurance pool by

- Purchasing Insurance Pool Bonds issued by the pool and
- Transferring the Principal of the Bond into the insurance pool's Funding Account.

A Liquidity Provider can be any natural person of eligible age or a legal entity that is permitted to engage in commercial activity within the jurisdiction of the insurance pool's locality.

### Working Capital Transit (WCTransit)

Due to a delay in a bond being issued and the corresponding principal being credited to the insurance pool's bank account, the variable WCTransit is used to capture the sum of all the Bonds' principal in transit.

######


######


When the Liquidity Provider fails to deposit the principal within the **Bond Payment Period** , the Bond contract is voided and the corresponding WCTransit is removed as well.

######


To encourage Liquidity Providers to deposit the principal and fulfil their contractual obligations, Liquidity Providers need to provide a security valued at 10% of the value of the Bond's principal. If a Liquidity Provider fails to deposit the principal, the ownership of the security transfers to the insurance pool. Two options are proposed to provide this security:

1. Deposit 10% of the bond's principal into the **Funding Account.**
2. Reference an existing insurance pool bond
  1. Whose principal amount has already been credited
  2. That does not expire (reach maturity) within the Bond Payment Period
  3. That is currently not being used as a reference for another bond.

As stated earlier, when the principal does not get credited within the Bond Payment Period, the ownership of the referenced insurance bond transfers to the insurance pool (i.e. the owner of the bond forfeits a percentage of the bond's principal including its yield). If the principal is credited within the time limit, the hold on the bond is removed.

### Working Capital Bond (WC<sub>Bond</sub>)

Taking WCTransit into account, the actual demand for new capital (WC<sub>Bond</sub>) to be acquired by the insurance pool through issuing bonds can be calculated as follows:

######


In purchasing Bonds, the following bond constraints and clauses apply to Liquidity Providers.

### Bond Principal

The combined principal of all Bonds on sale is limited and defined by WC<sub>Bond</sub>. If WC<sub>Bond</sub> is zero or negative, no bonds are available for purchase. Otherwise, Liquidity Providers can choose any desired principal amount as long as the principal is equal to or lesser than WC<sub>Bond</sub>. In addition, Liquidity Providers can purchase a multitude of Bonds. ![](RackMultipart20211030-4-10ku6rx_html_c6ef2c0d1d5d2f53.png)

### Bond Maturity

The maturity of any Bond is a constant and defined by WC<sub>TargetTime</sub>. No bonds with a maturity unequal to WC<sub>TargetTime</sub> are offered.

### Bond Yield (Yield to Maturity)

The actual yield Liquidity Providers can expect from a bond (BondYield) is the result of supply and demand market forces. This model proposes a dynamic way of adjusting the **Yield and Gradient** for the bonds on offer. An escalator will be used to illustrate the concept of adjusting the **Yield and Gradient.**![](RackMultipart20211030-4-10ku6rx_html_16b71ef8cd5bd.png)

The properties of the escalator are:

- The number of steps on the escalator equals WC<sub>Bond</sub> (one step for every unit of cu currency – e.g. $ 10 results in 10 steps). Figure 1 displays an escalator with 8 steps ➔ WC<sub>Bond</sub> = 8.
- At the beginning, the steps are distributed evenly from the top to the bottom step just like a normal escalator (see Figure 1). **Yield** refers to the yield of the top step on the escalator (the yield of the highest selling unit of WC<sub>Bond</sub> on offer). **Gradient** describes the step-by-step decrease in yield starting from the top step's yield.
- The steps are moving together at the same speed just like a normal escalator. Figure 2 displays this scenario in which the **Yield** (yield of the top step) moves from 6% to 7.5%. In addition, all the remaining steps' yield has increased by the same delta of 1.5%. ![](RackMultipart20211030-4-10ku6rx_html_99b954453ff48116.png)
- All steps on the escalator accelerate vertically at the same rate by multiplying the **Yield** with a **Yield Acceleration Constant (YAC)** on a minute by minute basis. In Figure 2, the **Yield** is at 7.5%. Hence, the escalator accelerates at the rate of (1 + 7.5%) multiplied by YAC.
- The height **of the ground** of any step represents the yield this step holds. (e.g. in Figure 2 the top step's yield is 9%, while the bottom step's yield is at 3% with the remaining steps distributed evenly).
- Liquidity Providers purchase any number of steps on the escalator starting from the top downward. As a result, the combined bond's yield (BondYield) is the average of the steps' yield purchased. In Figure 3, a Liquidity Provider purchased three steps. Hence, the bond's combined yield is the average of all the steps' yield purchased ([7.5% + 6.75% + 6%] / 3 ➔ BondYield = 6.75%). ![](RackMultipart20211030-4-10ku6rx_html_ea54aba7442e3ecf.png)
- When an updated demand for liquidity is calculated by the insurance pool (new value for WC<sub>Delta</sub> and WC<sub>Bond</sub>), the escalator gets a reset with WC<sub>Bond</sub> steps being redistributed evenly from the last **Yield** value (before the reset) to a yield of zero. If WC<sub>Bond</sub> is zero or negative, no steps are available for purchase from the escalator.
 Such a reset is illustrated in Figure 4 with a new WC<sub>Bond</sub> of 12, a **Yield** of 5.25% (equals **Yield** before the reset), and the steps being redistributed equally.

### Re-initialization of WC<sub>Bond</sub>, Yield and Gradient

At periodic intervals, a new demand for WC<sub>Delta</sub> is calculated by the insurance pool. This event in turn triggers a recalculation of **WC**** Bond ****, Yield** and **Gradient** which are referenced by the process of issuing new Bonds.

- First, a new value for WC<sub>Bond</sub> is calculated by using the previous formula

######


- Yield (Yield of the top step) remains at the same value. If no value has been defined in the past, a value of 1% is chosen as its initial value.
- Finally, the Gradient can be recalculated by

######


### Acceleration of Yield

The **Yield** of the insurance pool **accelerates at a discrete interval of one minute**. However, this increase is executed only if WC<sub>Bond</sub> exceeds a minimum threshold of 10% of WC<sub>Exp</sub>.

######


The reasoning for this 10% threshold is twofold. First, the resources consumed on a minute-by-minute basis to increase the Yield in comparison to the outstanding WC<sub>Bond</sub> volume may not justify its operations. Second, and more importantly, a small value for WC<sub>Bond</sub> may not make it worthwhile to any Liquidity Provider to purchase a bond with the remaining WC<sub>Bond</sub> as its principal. This would potentially cause the Yield to increase to a very high value. When a reinitialization occurs and a higher WC<sub>Bond</sub> demand is on offer, a significant portion of this WC<sub>Bond</sub> becomes available at an unjustifiably high Yield.

The implications in choosing an appropriate value for YAC are as follows:

1. **Double Value Time** represents the duration it would take the Yield to increase by a factor of two (i.e. to double in value). Hence, this duration determines the insurance pool's ability to respond to a changing environment in which Liquidity Providers request a higher Yield.

######


1. **Turnover Rate** refers to the time it would take to sell all the WC<sub>Bond</sub> under the condition that Liquidity Providers' demanded Yield remains constant. This can be perceived as the speed at which WC<sub>Bond</sub> is being 'sold' to Liquidity Providers.

######


The relationship between Double Value Time and Turnover Rate, depending on YAC, is shown in the diagram below.

![](RackMultipart20211030-4-10ku6rx_html_c54cd1130b129d38.png)

To obtain YAC on a per minute basis calculate

######


### Issuing of a new Insurance Pool Bond (Bond)

The terms of a newly issued Bond are as follows:

######


######


######


######


### Adjustment of WC<sub>Bond</sub> and Yield

Upon the successful issue of a Bond, WC<sub>Bond</sub> and Yield are adjusted:

######


######


### Reimbursement of Liquidity Providers

At the time, a Bond matures, the Bond's principal (BondPrincipal) plus yield (BondYield) are transferred back to the Liquidity Provider.

######


## 5. Insurance Consumers

Consumers can participate and get insurance coverage by subscribing to the insurance pool service. The term 'subscription' has been chosen deliberately since the proposed model provides a service that allows Consumers to trade their **policy risk coverage** (PolicyRisk) in exchange for a subscription fee **on a day-by-day basis**. Note: As mentioned earlier, consumers can choose the payment frequency as they are 'pre-funding' their insurance policy's holding account (Premium Account). From this account, all the consumers are charged the combined premium on a daily basis.

### Insurance Pool Risk Assessment function

As the policy risk coverage (PolicyRisk) is different from policy to policy, an objective and quantifiable process (or formula) to compare various insurance policies with each other is required. Such a process may differ again from insurance pool to insurance pool and hence needs to be defined in the context of the insurance pool's environment.

######


##### The required function needs to meet the following criteria:

- Considers 'n' predefined parameters that are provided as input variables in the calculation
- Does not depend on any source of data other than the 'n' input variables provided
- Returns a positive integer that is greater than zero
- Provides enough granularity so that the median value for PolicyRisk returned is around 1000 points
- Provides consistent results in returning PolicyRisk values for policies that capture their relative risk to each other. Risk in this context relates to a policy's **likelihood** of claim events occurring and the policy's claim events' combined **financial impact** on the insurance pool.

##### Some considerations in choosing input parameters are:

- Can the Consumer provide this parameter easily?
- What is the likelihood of a Consumer misinterpreting the parameter (i.e. providing the wrong information)?
- Is the parameter truly necessary or is its impact on the risk rating negligible?
- Would a Consumer feel more comfortable by providing additional information?

The ability and ease in defining such a function provides an indication for the suitability of forming a desired insurance pool. A cumbersome and difficult formula with many input parameters may be a strong indication of an insurance pool with too broad boundaries (i.e. one pool for everything). On the other hand, a very simple formula may provide an opportunity to broaden the pool's boundaries.

### Insurance Pool's boundaries

Further considerations in choosing the boundaries of what can get coverage and what cannot get coverage in an insurance pool are:

- As stated above, the ability to form an Insurance Pool Risk Assessment function
- Legal jurisdiction(s) the insurance pool operates in
- The diversity of the communities and individuals the insurance pool is consumed by
- The complexity in dealing with special or unique potential policies.

### Cost of insurance to Consumer

Consumers are charged their policies subscription fee to compensate Liquidity Providers for providing liquidity by purchasing bonds. The following steps are proposed to determine the fee that is charged to every insurance consumer.

For the purpose of the calculations below the variable BondPayout Amounts is used as an array containing the future bond maturity payouts for each day. For example the value stored at BondPayout Amounts {1} describes the bond maturity amount of **all bonds** that are maturing on the day of 1 day into the future (tomorrow).

These calculations are executed 'between' the days (at midnight) and the term _ **tomorrow** _ refers to the day that is about to start while _ **yesterday** _ refers to the day that has just ended.

The calculation of the **tomorrow's** premium undergoes the following steps:

1. **Average bond maturity payout amounts per day**

The average bond maturity payout in the future is calculated by dividing the total amount of **all maturing bonds in the future** by _Bond __Maturity Duration_. For example a value of 300 for _Bond Payout__ Average per day_ and a value of 90 for _Bond__Maturity Duration_means that over the next 90 days the average value of bonds maturing over the course of a single day is 300.

######

1. **Maximum bond payout slope per day**

Since bond maturity payout amounts are most likely distributed unevenly, the model must take that into account by calculating the maximum 'slope' of the cumulated upcoming bond maturity payouts.
 To do that for every day in the future until the BondMaturity Duration has been reached, the model has to ensure that the balance in the Bond Account remains positive by calculating the accumulated future capital demands.

######

The **daily demand** in capital to settle all maturing bonds for any given day 'i' in the future is defined as all the sum of bonds that are maturing until that day PLUS a buffer amount that should always be available in the bond account defined as 3 times the Bond PayoutsAverage per day MINUS the current balance of the Bond Account DIVIDED by 'i'.

A value of 700 for _Bond Payout_ _Slope_ _{ 8 }_ therefore means that over the course of the next 8 days a minimum of 700 per day has to be charged to ensure **appropriate solvency** of the Bond Account while also accounting for the current balance of the Bond Account.

1. **Insurance Pool's premium target for tomorrow**

The final **target premium** to be charged to all the consumers combined for tomorrow can be calculated by:

######


In this model the consumers are charged the average future cost for the insurance ( Bond PayoutAverage per day) at a minimum. The benefits of charging the average at a minimum premium is that the daily premiums charged over time are more stable as short term fluctuations in maturing bonds are compensated for. During the days when the bond maturity payouts are low the premiums charged are parked in the Bond account and are being consumed during days when bond maturity payouts are high. As a result the model provides a fairer premium model to all consumers independently of when someone joins or leaves the insurance pool.

The reasoning for using a buffer amount of 3 times the average payout amount per day is that as the name _Target Premium__Tomorrow_ suggests this is only a target premium the model is aiming for using the information that is available at a given point in time and is not guaranteed to be able to actually collect. The exact premium to be charged will only be known 24 hours later. To account for this inaccuracy a buffer of 3x suffices as compensation.

1. **Cumulative risk of all active policies within the pool**

The risk exposure of all insurance pool policies combined can be calculated as the sum of all the individual policies' risk points ('n' representing the number of currently active policies in the pool).

######


1. **Tomorrow's insurance premium (per risk point)**

By dividing the Target Premium for tomorrow by the combined risk of all currently active policies the premium for tomorrow and per risk point gets calculated.

######


Consequently a policy's premium for tomorrow is calculated by multiplying the policy's risk [points] with tomorrow's premium per risk point.

######


1. **Yesterday's combined insurance premium charged (for all active policies)**

The insurance premium that is charged to all active policies for the day of yesterday is

######


PremiumYesterday is the amount that is consequently transferred as a single payment from the Premium Account into the Bond Account.

1. **Overflow payments**

Overflow payment occur when 'excessive' funds in the Bond Account are debited and credited to the Funding Account. When this occurs the insurance pool becomes partially self-funding by bypassing Liquidity Providers. Overflow payments may occur once a day and the model calculates the amount that might be transferred as

######


If the calculated value of OverflowYesterday is positive, the corresponding amount gets transferred. This model relies on overflow payments especially during periods of growth in order to avoid the unnecessary accumulation of funds in the Bond account. This model puts these funds to 'work' by redirecting them into the Funding pool.

## 6. Insurance Pool Service Providers

### Insurance Claim Adjusters & Legal Services

The services of Claim Adjusters are required by the insurance pool to (1) investigate, (2) make decisions and (3) settle the insurance claims raised by the Consumers. The main objective of the group of adjustors is to provide consistency in handling the claims within the insurance pool (i.e. consistency in the context of all claims being handled across all adjustors). Due to the somewhat subjective nature of making insurance claim decisions, adjustors play a key role in providing a fair insurance service to the Consumers.

Independent of any particular insurance pool, Claim Adjusters do require a platform through which they can ask for support, share information and establish additional guidelines that facilitate consistency in handling claims. In addition, Claim Adjusters are supported by a set of predefined insurance pool rules, terms and conditions they have to obey in performing their service. These guidelines are also communicated to the Consumers.

Legal assistance may be required to support Claim Adjusters in settling ambiguous claims from a legal standpoint.

Claim Adjusters as well as legal service provider are compensated from the insurance pool on a claim-by-claim basis. The fee structure and compensation model for the services provided may differ from insurance pool to pool. However, and most importantly, these service providers are independent and are not incentivized to either marginalize or amplify insurance claim costs. They are incentivized in every possible way to make effective, fair and consistent decisions.

### Suppliers

Claim Adjusters engage Suppliers on a claim-by-claim basis to rectify the damage caused by the claim. The Supplier's remuneration depends on an agreement between the Supplier and the Claim Adjuster being found.

### Pool Owners / Trust / Mutual

An insurance pool model needs to provide clear instructions, rules, guidelines and procedures that can be followed by the stakeholders in engaging with the insurance pool. The claims process bears a particular challenge for the insurance Pool Operators and the claims Adjusters alike in creating rules and guidelines on how to deal with the infinite number of possible claim situations. Despite the insurance Pool Operators' best efforts, the insurance pool will likely fall short in providing enough rules and guidelines as life in its very nature is too complex and decisions are often ambiguous.

To compensate for life's gray-zones and its ambiguity, a Safety Net Insurance Service is proposed to be an integral part of the insurance pool model. The single objective of this service is to catch all those insurance claims that should have been caught initially but fell through an unintended loophole in the insurance pool's rules and guidelines.

Safety Net Insurance Services should not be confused with an entity that deals with appealed claims in a legal sense. If a Consumer appeals the decision made from a Claim Adjuster, it remains with the Claim Adjuster – and potentially legal assistance – to resolve the dispute.

Safety Net service providers are NOT bound by any rules or guidelines in making their decisions about insurance claims. They are empowered to do what they perceive to be the 'right' thing to do in a given claim. A guiding question that these individuals should ask themselves is: &quot;If a particular case was brought to the attention of every insurance pool Consumer, would the majority of these Consumers deny or acknowledge this claim?&quot; The only boundary that is imposed on them is a cap (e.g. up to 1% of total WC<sub>Exp</sub>) on the total amount they are authorized to use for settling claims that were presented to them.

Another responsibility that falls with this entity is to be the legal representative body and 'owner' of this insurance pool. As the name suggest this entity is set up as a Trust representing the interests of all involved stakeholders in this ecosystem (Consumers, Liquidity Providers, Suppliers, Claim Adjusters and Pool Operators). In addition, this Trust are the rightful owners of the 3 bank accounts required by the pool (Funding Account, Bond Account and Premium Account).

### Insurance Pool Operators

The insurance Pool Operators are the initiators and the executing body of the insurance pool. The model suggests that these operators work under the umbrella of their own legal entity (e.g. limited company; Ltd.) that is registered within the insurance pool's environment.

This entity is responsible for:

- Providing the legal infrastructure in which the pool can operate

- Providing the technical infrastructure for the pool to operate in
- Monitoring, maintaining, and auditing the insurance pool's operations
- Education of insurance pool community and external stakeholders.

To avoid any potential conflict of interest issues that may arise as a result of the tasks and duties performed by the legal entity representing the insurance Pool Operators, the model proposes a fixed fee (percentage fee of WC<sub>Exp</sub>) that is allocated to the Pool Operators. This fixed fee can be perceived as the overhead costs of running the insurance pool as this legal entity does not provide any direct and tangible benefits to any insurance pool Consumer.

## 7. Relevant Research

It is interesting to observe how small and well-established corporations alike struggle to capitalize on the value of existing and freely available research offers. It may be the case that many of the organization's stakeholders are aware of the information, but the actual implementation and the corresponding change associated with executing on it represents the bigger obstacle.

Creating a new insurance pool offers an opportunity to consider and leverage research in addressing the technical, legislative, organizational and many other challenges that need to be overcome. An area that might be easily overlooked however is the human element. A detailed examination of the relevant research would go beyond the scope of this paper. However, a list of relevant researchers and a summary of their research is outlined next.

- Dan Ariely's research (5) (9) in the field of behavioral economics might be the single most important research to consider in this context. His research focuses on the irrationality in the decision-making process of humans. Of particular interest are his findings in the field of unethical behavior and the underlying dynamics that influence this behavior.
- Barry Schwartz (10) and Sheena Iyengar's (11) research on choice and its impact on human decision making is of particular importance in defining insurance services. The central line of argumentation is that some choice is better than none but providing a Consumer with too much choice causes them to feel overwhelmed and somewhat paralyzed in making decisions.
- James Surowiecki's publication on 'The Wisdom of Crowds' (12) gives profound insight into the combined decision-making power of crowds provided the necessary preconditions are met.
- Nobel laureate Daniel Kahneman's prospect theory (13) makes an argument to take human's cognitive biases into account. An important example of a cognitive bias to consider is loss-aversion – &quot;they are more likely to act to avert a loss than to achieve a gain&quot; (14).

## 8. Conclusion

In this paper, an alternative model of insurance is presented. It builds on the aspects that are working well (sharing of risk among the insured) while eliminating some of the major flaws in this industry. The conflict of interest between the owner of the insurance and the customers has been resolved as the concept of ownership of an insurance pool has been redefined. The insurance Pool Operators (that may be perceived as the owners) are compensated through a fixed fee and hence would only destroy trust in the pool by not honoring Consumers' rights. Hence, claims Adjusters are empowered to work with a Consumer while acting as a representative and on behalf of insurance pool community.

Safety Net insurance is intended to provide an additional layer of insurance that goes beyond the fact-driven, rule-imposed way of doing things, by reintroducing humanity back into insurance. Building on the extensive research in the field of behavioral economics, Consumers are reminded during critical moments in the claims process that they are part of a community and engaging in fraudulent behavior would harm this fragile social fabric.

In honoring the model outlined, it is very likely that only insurance products that are of value to the Consumers and solve a particular need would come into existence. In addition, the simplification of the insurance terms and rules may help Consumers to make better informed decisions about their insurance requirements.

Lastly, the insurance value proposition (value for money) should increase drastically from 50% to well above 90% as arguably the only overhead cost within the proposed model is the fixed fee to be paid to the insurance Pool Operators. Since the proposed model is a clearly defined system, the flow of money, including its rationale and operating procedures, can be verified by the community. It is the loop of disclosing information and receiving ongoing feedback from the community that builds trust and may represent the strongest argument for this new model of insurance.

##


## Acronyms

**Currency Unit**** [cu]** The smallest denomination of the currency used for the insurance pool
 (Dollar Cent, Euro Cent, BTC Satoshi)

**Accounts [cu]** The insurance pools' accounts that hold currency. The pool requires the following accounts: _Funding Account, Premium Account and Bond Account._

**WC [cu]** Stands for Working Capital and refers to the monetary assets or obligations of the insurance pool.

**WC**** Bal **** [cu]** The balance of the WC in the account.

**WC**** Locked **** [cu]** Working Capital that is reserved to be used for locked but not assessed and settled claims.

**WC**** Exp **** [cu****/ day]** The anticipated expenses of running the insurance pool per day.

**WC**** Time **** [day]** The duration WC<sub>Bal</sub> is sufficient to cover anticipated claim payments without being topped up. This value can be negative!

**WC**** Delta **** [cu]** The delta demand to top up WC<sub>Bal</sub> to reach the desired WC<sub>Time</sub>

**WC**** Bond **** [cu]** The volume of units on offer to be issued as bonds to Liquidity Providers.

**WC**** Transit **** [cu]** The volume of units that are issued as bonds but the bond principal has not yet been credited to the insurance pool's account.

**CCU | CCU**** Total **** [cu****| %]** The Capital Costs per Unit of WC demanded by Liquidity Providers (i.e. the return on investment for Liquidity Providers).

**CCU**** Risk **** [cu****| %]** The Capital Costs per Unit of WC demanded by Liquidity Providers as compensation for the investment risk.

**CCU**** Interest **** [cu****| %]** The Capital Costs per Unit of WC demanded by Liquidity Providers as interest compensation.

**Yield [%]** The yield of the highest selling unit of WC<sub>Bond</sub> on offer.

**YAC [% / minute]** The Yield Acceleration Constant is a constant that describes the amount by which Yield grows exponentially.

**Gradient [%]** Gradient describes the unit-by-unit decrease in yield of the WC<sub>Bond</sub> units on offer starting from Yield.

**Bond [cu]** An Insurance Pool Bond is a means for Liquidity Providers to invest in the insurance pool.

**Bond**** Principal **** [cu]** The Bond's principal.

**Bond**** Yield **** [%]** The Bond's yield.

**Bond**** Maturity **** [day]** The time after which the bond matures in days.

**Bond Payment Period [hour]** The period in hours within the Bond's principal has to be credited to the insurance pool's bank account.

## References

1. **Wikipedia.** Insurance. [Online] 2016.
[https://en.wikipedia.org/wiki/Insurance](https://en.wikipedia.org/wiki/Insurance)
2. **Insurance Information Institute.** Insurance Fraud. [Online] January 2016. [http://www.iii.org/issue-update/insurance-fraud](http://www.iii.org/issue-update/insurance-fraud)
3. **Paperno, Alex, Kravchuk, Vlad and Porubaev, Eugene. Teambrella:** A Peer to Peer Insurance System. [Online] 2016.
[https://teambrella.com/WhitePaper.pdf](https://teambrella.com/WhitePaper.pdf)
4. **Ariely, Dan.** The (Honest) Truth About Dishonesty – How we lie to everyone – especially ourselves. London : Harper, 2012.
5. **Nakamoto, Satoshi.** Bitcoin: A Peer-to-Peer Electronic Cash System. [Online] October 2008.
[https://bitcoin.org/bitcoin.pdf](https://bitcoin.org/bitcoin.pdf)
6. **Wood, Gavin.** Ethereum: A secure decentralized generalized transaction ledger. [Online] Homestead Revision, 2015.
[http://gavwood.com/paper.pdf](http://gavwood.com/paper.pdf)
7. **World Economic Forum.** The future of financial infrastructure – An ambiguous look at how Blockchain can reshape financial services. [Online] August 2016. [http://www3.weforum.org/docs/WEF\_The\_future\_of\_financial\_infrastructure.pdf](http://www3.weforum.org/docs/WEF_The_future_of_financial_infrastructure.pdf)
8. **Ariely, Dan.** Predictably Irrational – The hidden forces that shape our decisions. New York : Harper Perennial, 2009.
9. **Schwartz, Barry.** The Paradox of Choice – Why more is less. New York : HarperCollins Publishers, 2004.
10. **Iyengar, Sheena.** The Art of Choosing. New York : Twelve Hachette Book Group, 2012.
11. **Surowiecki, James.** The Wisdom of Crowds. New York : Anchor Books, 2005.
12. **Kahneman, Daniel.** Thinking, Fast and Slow. London : Allen Lane, 2011.
13. **Wikipedia.** Thinking, Fast and Slow. [Online] 2016. [https://en.wikipedia.org/wiki/Thinking,\_Fast\_and\_Slow](https://en.wikipedia.org/wiki/Thinking,_Fast_and_Slow)
14. **Jodlbauer, Herbert.** Produktionsoptimierung – Wertschaffende sowie kundenorientierte Planung und Steuerung, 2. Auflage. Wien : Springer-Verlag, 2008.
15. **Vedantam, Shankar.** The Hidden Brain – How our unconscious minds elect presidents, control markets, wage wars, and save our lives. New York : Spiegel & Grau, 2010.
16. **Gladwell, Malcolm.** The Tipping Point – How little things can make a big difference. London : Abacus, 2000.
17. **Reputation Institute.** 2014 U.S. Industry REPTRAK: Insurance - Insurance firms struggle to move beyond average reputation. [Online] 2014. [https://www.reputationinstitute.com/getattachment/d726d475-5dea-4924-be19-293b5bccece3/2014-US-Industry-RepTrak-Insurance.pdf](https://www.reputationinstitute.com/getattachment/d726d475-5dea-4924-be19-293b5bccece3/2014-US-Industry-RepTrak-Insurance.pdf)
18. **Honest Insurance.**
[https://www.honestinsurance.net](https://www.honestinsurance.net/) [Online] 5 5, 2017.