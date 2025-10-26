## 🏆 Top 10 Predicted Products (Simulated User)

The dashboard's "Top 10 Predicted Products" section uses the trained Random Forest model to rank products by **predicted purchase likelihood**.  

**Example Output (Simulated User):**

| Rank | Product ID | Predicted Score | Total Orders | Reorder Rate |
|------|------------|----------------|--------------|--------------|
| 1    | 24852      | 126,398        | 149,684      | 0.844       |
| 2    | 13176      | 99,960         | 119,871      | 0.834       |
| 3    | 21137      | 64,074         | 82,627       | 0.775       |
| 4    | 21903      | 59,511         | 76,838       | 0.775       |
| 5    | 47209      | 54,960         | 68,567       | 0.802       |
| 6    | 47766      | 42,450         | 55,907       | 0.759       |
| 7    | 27845      | 35,728         | 42,920       | 0.832       |
| 8    | 47626      | 33,590         | 48,328       | 0.695       |
| 9    | 27966      | 33,271         | 43,278       | 0.769       |
| 10   | 16797      | 31,821         | 45,392       | 0.701       |

### 🔍 Analysis

- **Predicted Score:** Represents the model's confidence that the product will be purchased next by a user. Higher score → higher likelihood.  
- **Total Orders:** Popularity indicator; products with more historical orders are more likely to appear in top recommendations.  
- **Reorder Rate:** Loyalty metric; higher reorder rates indicate products frequently repurchased.  

### 📊 Observations

1. **High Popularity & Reorder:**  
   - Top-ranked products (e.g., `product_id 24852` and `13176`) combine high total orders and high reorder rates (≈0.83–0.84), showing consistent customer demand.  

2. **Moderate Popularity, Strong Affinity:**  
   - Products like `27845` have lower total orders but high reorder rate (0.832), suggesting niche products with loyal buyers.  

3. **Diverse Mix:**  
   - The list balances **high-volume items** (many orders) and **high-affinity items** (high reorder rate), providing effective recommendations even without a user-specific profile.  

4. **Business Insight:**  
   - Focusing marketing, promotions, or inventory planning on these top predicted products can increase basket size and reorder probability.  
   - The simulated user predictions allow the dashboard to provide **immediate insights** even when individual `user_id` data is unavailable.  

> **Note:** This is a simulated ranking for demonstration purposes; real user-specific predictions would require `user_id` features.

---

**Integration in Dashboard:**  

- The Streamlit dashboard displays this Top 10 list dynamically.  
- Users can filter by product-level metrics or explore feature importance to understand why certain products rank higher.
