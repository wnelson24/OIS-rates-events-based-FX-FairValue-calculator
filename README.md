# OIS-rates-events-based-FX-FairValue-calculator


- **Positive imbalance → USD under-priced (FX lagging dovish repricing)**  
- **Negative imbalance → USD over-priced (FX overreacting to hawkish repricing)**  

---

## 🧠 What It Does

1. Pulls daily data for:
   - Effective Fed Funds rate (`DFF`)
   - 2-Year Treasury yield (`DGS2`)
   - EURUSD spot (Yahoo Finance)

2. Calculates rate differentials and changes (`ΔRate_Spread`).

3. Fits a rolling regression (20-day window) to estimate EURUSD sensitivity to front-end repricing.

4. On days with large policy repricings (|ΔRate_Spread| > 5 bps), computes:
   - **Fair Value EURUSD** = previous spot × (1 + β × ΔRate_Spread)
   - **Imbalance** = Actual – Fair Value

5. Outputs and visualizes:
   - A table of recent events
   - A chart comparing actual vs. policy-implied EURUSD

---

## 🔍 Example Output

| Date | EURUSD | ΔRate_Spread | β | FairValue | Imbalance |  
|------|---------|---------------|--|------------|------------|  
| 2025-09-02 | 1.1716 | +0.07 | 0.0469 | 1.1657 | +0.0059 |  
| 2025-10-10 | 1.1566 | −0.08 | −0.0181 | 1.1753 | −0.0186 |

**Interpretation:**  
- *Positive imbalance → short EURUSD (USD under-reacted)*  
- *Negative imbalance → long EURUSD (USD rich to policy)*  

---

## 🧩 Next Steps

The current model is a **mathematical fair-value baseline** — pure policy transmission.

Future extensions:
- Adjust fair values for **macro sentiment** (VIX, SPX, credit spreads)  
- Incorporate **cross-market drivers** (global OIS differentials, commodities)  
- Use **standard deviation of imbalance** as a dislocation signal  
- Expand across **G10 FX** to map global policy alignment

---

## 🛠️ Dependencies

- `fredapi`
- `yfinance`
- `numpy`
- `pandas`
- `matplotlib`
- `scikit-learn`

---

## ⚙️ Usage

```bash
python OIS_to_FX_eventsdriven.py
