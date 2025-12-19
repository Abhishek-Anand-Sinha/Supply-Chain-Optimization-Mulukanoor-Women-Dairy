# The 30km Profit Cliff: Simulating Mulukanoor Dairy's Logistics

### Executive Summary
**The Strategy Question:** The *Mulukanoor Women's Cooperative Dairy* (MWCD) operates on a strict **30km Compact Area** model. Should the cooperative expand its operational radius to 60km to double its milk volume, or would logistics costs erode profitability?

**The Solution:** I built a **Unit Economics Simulation** in Python to model the trade-offs between linear revenue growth and exponential transport costs.

**The Verdict:** The simulation identified a mathematical **"Profit Cliff" at 45km**.
* **Current State (30km):** Profit Maximization Zone.
* **Expansion State (>45km):** Logistics costs outweigh revenue growth.
* **Conclusion:** The 30km limit is not just a policy rule; it is a financial necessity to maintain the cooperative's net margin.

![Profit Cliff Chart](Supply_Chain_Chart.png)
*(Fig 1: The Green Line shows Net Profit peaking at 35km before crashing due to transport inefficiencies.)*

---

### The Business Physics (Simulation Logic)
The model simulates the P&L (Profit & Loss) for every operational radius from **10km to 85km**. It is built on three core assumptions derived from the FY2024-25 Balance Sheet:

| Variable | Logic | Trend |
| :--- | :--- | :--- |
| **Revenue** | Grows with Area Coverage (More villages = More cows). | 🟢 **Linear Growth** |
| **Transport Cost** | Fuel + Empty Returns + Driver Overtime + Vehicle Wear. | 🔴 **Exponential Growth** (`Cost ^ 1.2`) |
| **Spoilage** | Distance = Time. Milk bacteria multiplies exponentially after 4 hours. | 🔴 **Step Function** (Jumps to 10% loss >60km) |

---

### Key Insights (The Optimization Curve)
The simulation reveals three distinct economic zones:

1.  **Zone of Efficiency (10-35km):**
    * Economies of scale kick in. Fixed plant costs (electricity/salaries) are spread over higher volumes.
    * **Net Profit peaks at ~35km.** This validates the current management strategy.

2.  **The Breakeven Point (55km):**
    * Revenue continues to grow, but the "Cost of Distance" (Fuel + Spoilage) eats 100% of the gross margin.

3.  **The Profit Cliff (>60km):**
    * Net Profit turns **Negative**.
    * *Strategic Implication:* Expanding to 60km would increase top-line revenue but destroy shareholder value. The cost of collecting the "marginal liter" of milk exceeds its selling price.

---
## 🧐 Deep Dive: The Business Physics
*For a detailed breakdown of the simulation logic and mathematical assumptions.*

### 1. The P&L Equation
The model calculates the Daily Net Profit for every radius ($r$) from **10km to 85km** using this fundamental equation:

$$\text{Net Profit} = \text{Revenue} - (\text{Member Payout} + \text{Transport Cost} + \text{Spoilage Loss} + \text{Fixed Ops})$$

### 2. Variable Breakdown & Assumptions

#### **A. Revenue (Linear Growth)**
* **Logic:** As the radius expands, the catchment area increases, leading to more villages and more cows.
* **Formula:** $\text{Revenue} = r \times \text{Revenue per km}$
* **Assumption:** We assume linear density for simplicity.

#### **B. Member Payout (The Fixed Anchor)**
* **Logic:** Unlike private firms, a cooperative cannot lower the procurement price to cover inefficiencies.
* **Constraint:** Based on the FY2024-25 Balance Sheet, **74%** of Total Revenue is strictly allocated to women farmers.
* **Impact:** This leaves a razor-thin **26% Margin** to cover all processing and logistics.

#### **C. Transport Cost (Exponential Growth)**
* **Logic:** Driving 60km is more than twice as expensive as driving 30km due to empty return trips, driver overtime, and vehicle wear-and-tear.
* **Formula:**
$$\text{Transport Cost} = \text{Base Cost} \times \left( \frac{r}{30} \right)^{1.2}$$
* **Why the 1.2 Exponent?** In logistics modeling, a linear factor ($1.0$) underestimates cost. The $1.2$ factor accounts for "Diseconomies of Scale" at longer distances.

#### **D. Spoilage (The "Step Function")**
* **Logic:** Distance equals Time. Milk is highly perishable. Bacteria growth is non-linear.
* **Thresholds:**
    * **0-30km:** Safe Zone (0.5% Loss).
    * **30-45km:** Risk Zone (2% Loss).
    * **>60km:** Danger Zone (10% Loss).

---

### ⚙️ Simulation Methodology
The Python script (`Supply_Chain_Simulation.py`) performs the following operations:
1.  **Vectorization:** Uses `NumPy` to create an array of 15 different distance scenarios (10km, 15km... 85km).
2.  **Iteration:** Runs the P&L equation through a loop for each scenario.
3.  **Optimization:** Uses `Pandas` to identify the exact kilometer where Net Profit is maximized (`df['Net Profit'].max()`).

---

### Tech Stack
* **Python (NumPy):** For vectorizing the simulation scenarios.
* **Pandas:** For structuring the financial output tables.
* **Matplotlib:** For visualizing the intersection of Cost and Revenue curves.

### 📂 Repository Structure
* `Supply_Chain_Simulation.py`: The Python engine modeling Revenue vs. Logistics.
* `MWCD_Supply_Chain_Simulation.csv`: The generated dataset showing P&L at every 5km increment.
* `Supply_Chain_Chart.png`: The visual proof of the Profit Cliff.

---
*Created by Abhishek Anand Sinha | TISS Hyderabad | Public Policy & Governance*
