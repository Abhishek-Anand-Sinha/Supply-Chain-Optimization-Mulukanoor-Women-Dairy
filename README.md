# The 30km Profit Cliff: Simulating Mulukanoor Dairy's Logistics

### Executive Summary
**The Strategy Question:** The *Mulukanoor Women's Cooperative Dairy* (MWCD) operates on a strict **30km Compact Area** model. Should the cooperative expand its operational radius to 60km to double its milk volume, or would logistics costs erode profitability?

**The Solution:** I built a **Unit Economics Simulation** in Python to model the trade-offs between linear revenue growth and exponential transport costs.

**The Verdict:** The simulation identified a mathematical **"Profit Cliff" at 45km**. Expanding beyond the current 30km radius would turn the cooperative's razor-thin net margin (0.16%) into a loss.

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
