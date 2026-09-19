An initial dummy model was developed; read the full issue: https://www.brighty.space/essays/revenue-defensibility-for-stablecoins

The model relies on two important variables: Migration Cost and Correlation. For the sake of robustness and simplicity, the V1 research aims to address solely correlation as it relates to the defensibility of stablecoin revenue. 

Some 2-3 tractable metrics were derived as subsets of the function:

- Infrastructural correlation: Correlation that is a consequence of shared or common infrastructure and a potential avenue for capital coordination for or against the stablecoin network

- Economic correlation: Correlation in-which players have a common or shared economic incentive, a result of which could form genuine coordination to affect the network 

- Structural Dependency (initially termed as structural correlation): Structural dependency, as a result of the network's architecture, measures the stablecoin's dependency on a single entity. This is still a gray area in terms of its classification; it has some really fitting aspects for correlation but might not be robust if treated only as a derivative of correlation


## Infrastructural Correlation C(I)

#### Data & Coverage

The current C(I) implementation uses wallet-level stablecoin holdings mapped to identifiable entities and, where possible, aggregated to their underlying infrastructure operators. The present analysis covers five stablecoins (USDT, USDC, USDe, USDtb, USDH) and is based on the currently available entity/operator mappings.

Because infrastructure attribution is incomplete for some of the observed entities, unresolved entities are excluded from operator-level concentration calculations. Consequently, C(I) should currently be interpreted as a measure of concentration within the observed and successfully mapped infrastructure universe, rather than the total stablecoin infrastructure concentration.

#### Methodology

##### **Objective**

Infrastructural correlation, $C(I)$ measures the extent to which a stablecoin’s economic activity is concentrated across a small number of infrastructure operators that could serve as material coordination points.

The underlying hypothesis is that greater concentration of stablecoin activity across a small number of economically distinct infrastructure operators creates greater coordination pressure and therefore potentially weaker revenue defensibility.

$C(I)$ is therefore a proxy for coordination pressure, not an absolute that states concentration as a necessity for coordination.

---

## **1. Infrastructure universe**

The analysis begins by classifying observed entities according to their functional role in the stablecoin ecosystem.

The baseline infrastructure universe includes:

- Centralized exchanges (CEX)
- Exchanges
- DeFi
- Smart contract / protocol infrastructure
- Wallet infrastructure
- Custody
- Blockchain infrastructure
- Bridges
- Issuers
- Protocol infrastructure

These categories are included because they can represent material points of capital concentration, custody, issuance, liquidity, interoperability, or settlement through which stablecoin activity can converge.

The baseline excludes:

- Applications
- Government / financial institutions
- Market makers
- Funds / institutional entities
- Individuals / other
- Restricted entities

Applications are excluded from the primary infrastructure measure because the category is too heterogeneous to establish a consistent infrastructure function across applications. Where an application genuinely performs an infrastructure role, it can instead be functionally reclassified into the appropriate infrastructure category.

Similarly, government or institutional status alone does not constitute infrastructure. An institution would enter the infrastructure universe only where it directly operates a relevant issuance, custody, settlement, distribution, or other infrastructure function.

---

## **2. Operator aggregation**

Raw wallet-level observations are first mapped to entities and then to their underlying infrastructure operators. The relevant unit for $C(I)$ is therefore the operator, rather than the individual wallet or entity.

For each stablecoin, the amount attributed to operator i is:

$A_i=\sum_{j\in i}A_j$

where $A_j$ represents the observed stablecoin amount associated with entity j.

Operator shares are then calculated as:

$s_i=\frac{A_i}{\sum_{k=1}^{N}A_k}$

where $N$ is the number of infrastructure operators in the relevant stablecoin universe.

Unresolved entities are not self-mapped to themselves. Instead, they remain unresolved and are excluded from the operator-level concentration calculation until a defensible operator mapping is available. This prevents the unidentified entities from appearing as an independent infrastructure operator.

---

## **3. Infrastructure concentration**

Infrastructure concentration is measured using concentration ratios across the largest operators:

$CR_n=\sum_{i=1}^{n}s_i$

where $CR_n$ represents the share of observed stablecoin activity controlled by the largest n infrastructure operators.

The primary concentration windows are:

$CR_1,\ CR_5,\ CR_{10},\ CR_{20}$

These capture concentration at progressively broader coordination thresholds, from a single dominant operator through the largest twenty. The methodology deliberately retains the individual operators rather than aggregating smaller operators into a single “Others” category. Doing so would incorrectly treat economically independent infrastructure as if it were a single coordinated actor.

---

## **4. Operator diversity**

Concentration ratios alone do not fully describe the structure of the infrastructure layer. Two stablecoins could have similar top-N concentration while differing substantially in how activity is distributed across the remaining operators.

$C(I)$ therefore incorporates normalized Shannon diversity:

$D_E= \frac{-\sum_{i=1}^{N}s_i\ln(s_i)} {\ln(N)}$

where:

- $p_i$ = operator $i’s$ share of observed activity
- $N$ = number of infrastructure operators

$D_E$ ranges from approximately 0 to 1:

- $D_E=0$: complete concentration
- $D_E\rightarrow1$: maximum observed diversity

The concentration-pressure component is therefore:

$1-D_E$

A lower diversity score produces greater coordination pressure.

---

## **5. C(I) construction**

The weighted concentration component is:

$CR_W= w_1CR_1+w_5CR_5+w_{10}CR_{10}+w_{20}CR_{20}$

The baseline specification uses top-heavy weights:

$CR_W= 0.4CR_1+ 0.3CR_5+ 0.2CR_{10}+ 0.1CR_{20}$

The rationale is that $C(I)$ is intended to capture coordination points, rather than simply describe the distribution of activity. A single dominant infrastructure operator therefore receives greater weight than marginal increases in concentration among the twentieth-largest operators.

The final infrastructure correlation score is:

$\boxed{ C(I)= \left( 0.4CR_1+ 0.3CR_5+ 0.2CR_{10}+ 0.1CR_{20} \right) (1-D_E) }$

The score is bounded approximately between 0 and 1.

---

## **6. Interpretation**

$C(I)$ should be interpreted as coordination pressure arising from infrastructure concentration.

| **$C(I)$** | **Interpretation**                                                          |
| ---------- | --------------------------------------------------------------------------- |
| Low        | Activity is distributed across a relatively diverse infrastructure set      |
| Medium     | Material activity is concentrated across several infrastructure operators   |
| High       | Activity is strongly concentrated around one or a small number of operators |

Importantly: Concentration does not imply coordination.

A high $C(I)$ score indicates that the infrastructure structure _permits greater potential coordination or dependency_. It does not demonstrate that operators are actually coordinating, colluding, or exercising control over the stablecoin. This is important because the ultimate objective is not to measure concentration for its own sake. $C(I)$ is one component of the broader revenue-defensibility framework.

---

## **7. Robustness testing**

Because $C(I)$ contains methodological choices that could influence its magnitude, the methodology is stress-tested across several dimensions:

1. **Weight sensitivity**  
    Compare the baseline top-heavy specification against $CR1-heavy$, $CR20-heavy$, and equal-weight specifications.
2. **Infrastructure-scope sensitivity**  
    Test whether results depend materially on the inclusion or exclusion of infrastructure categories such as issuers, CEXs, applications, or institutional entities.
3. **Operator-mapping sensitivity**  
    Test the effect of uncertain or lower-confidence entity-to-operator mappings.
4. **Diversity-measure sensitivity**  
    Compare normalized Shannon diversity with alternative diversity formulations.
5. **Concentration-window sensitivity** Test alternative concentration windows such as $CR_{1,5,10,25}$ and $CR_{1,5,15,25}$.

The purpose of these tests is not to find a specification that produces the preferred ranking. It is to determine whether the conclusions are robust to reasonable methodological alternatives.

---

## **8. Baseline result**

Under the baseline specification, the current $C(I)$ ranking is:

| **Stablecoin** | **C(I)**   |
| -------------- | ---------- |
| USDH           | 0.9380     |
| USDTB          | 0.5845 |
| USDE           | 0.5515 |
| USDT           | 0.4876 |
| USDC           | 0.3486 |

The stress testing shows that USDH remains the highest-C(I) stablecoin across every tested specification, while the magnitude of C(I) varied depending on the weighting scheme. The relative ordering of the five stablecoins remains unchanged across these specifications.

## **9. Stress-Test Results**


 ### Weight Specification Sensitivity

| Stablecoin | Baseline / Top-Heavy | CR1-Heavy | CR20-Heavy | Equal Weights |
| ---------- | -------------------: | --------: | ---------: | ------------: |
| **USDH**   |               0.9380 |    0.9384 |     0.9447 |        0.9414 |
| **USDTB**  |               0.5845 |    0.5883 |     0.6448 |        0.6146 |
| **USDe**   |               0.5515 |    0.5590 |     0.6337 |        0.5926 |
| **USDT**   |               0.4876 |    0.4945 |     0.5718 |        0.5297 |
| **USDC**   |               0.3486 |    0.3592 |     0.4514 |        0.4000 |

#### Interpretation

The weight sensitivity analysis produces relatively stable results for USDH, while the magnitude and relative ordering of the remaining stablecoins are more sensitive to the weighting specification.

USDH remains the highest-C(I) stablecoin under all four tested specifications. USDTB, USDe, USDT, and USDC maintain the same relative ordering across the specifications, although the magnitude of $C(I)$ changes materially under the $CR20-heavy$ specification.

This suggests that the broad ordering observed in the current sample is more stable than the absolute $C(I)$ values themselves. However, the sample remains limited to five stablecoins, and broader testing is required before assessing whether this robustness persists across a larger stablecoin universe.

## **10. Current limitations** 

- **Limited sample**: The current implementation of this research covers only five stablecoins
- **Entity attribution**: Everything within means has been done to map the wallets to corresponding entities, but they might not always be reliable
- **Observed activity**: C(I) currently operates on the successfully mapped/observed universe rather than necessarily the entire stablecoin supply
- **Infrastructure classification**: Functional classification can be ambiguous where an entity performs multiple roles
- **Coordination assumption**: Infrastructure concentration identifies potential coordination points but does not accurately establish actual coordination
- **Cross-Infrastructure dependence**: Operators may share ownership, liquidity, governance, or some technical dependencies that are not captured by simple operator aggregation
- **Temporal dynamics**: Current work represents a point-in-time structure and has not yet established how infrastructural correlation evolves through market cycles and events
- **Weight specification**: Although the current ordering is stable across tested weight specifications, absolute c(I) values remain sensitive to the weighting scheme.


### Potential Application 

The longer-term objective is to determine whether C(I), alongside the other components of the broader defensibility framework, can become a standardized analytical primitive for stablecoin research. If sufficiently robust, the framework could potentially be incorporated into DeFiLlama’s existing stablecoin analytics and eventually exposed through Llama AI, allowing users to query not only the size and revenue of a stablecoin’s economic base, but also the structural properties that may affect the defensibility of that revenue. 
