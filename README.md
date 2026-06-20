# Quickbytes Food Delivery Crisis Recovery

- Domain: Food & Beverages
- Function: Strategy

This is a data-driven crisis recovery and business intelligence project for food-tech startup QuickBite Express. It leverages sales, delivery operations, and sentiment data to diagnose a massive 2025 operational outage and brand crisis, providing targeted roadmaps to stabilize merchant partnerships and reactivate churned high-value users.

Link to the [Challenge](https://codebasics.io/challenges/codebasics-resume-project-challenge/23)

Link to the [Interative Dashboard]

## Problem Statement

QuickBite Express is a Bengaluru-based food-tech startup (founded in 2020) that connects customers with nearby restaurants and cloud kitchens.

In June 2025, QuickBite faced a major crisis. A viral social media incident involving food safety violations at partner restaurants, combined with a week-long delivery outage during the monsoon season, triggered massive customer backlash. Competitors capitalized with aggressive campaigns, worsening the situation.
 
The challenges were severe: 
- A large portion of active users disengaged within a short period. 
- Daily orders saw a sharp decline compared to earlier months. 
- Customer satisfaction scores fell sharply, signaling trust issues. 
- Many partner restaurants shifted to competing platforms. 
- Customer acquisition costs rose significantly. 
- QuickBite has allocated a major recovery budget, overhauled food safety protocols, and upgraded its delivery infrastructure.
 
The management expects detailed insights into the following: 
- Customer Segments: Identify which customers can be recovered and which need new strategies. 
- Order Patterns: Analyse order trends to uncover behavioral changes across phases (pre-crisis, crisis, recovery). 
- Delivery Performance: Assess delivery times, cancellations, and SLA compliance to pinpoint operational gaps. 
- Campaign Opportunities: Recommend targeted initiatives to rebuild trust and loyalty across demographics. 
- Restaurant Partnerships: Predict which partnerships are most valuable for long-term retention. 
- Feedback & Sentiment: Monitor real-time ratings, reviews, and sentiment to guide ongoing recovery efforts. 

## Task

- Go through the metadata and analyse the datasets thoroughly. This is the most fundamental step. 
- Begin your analysis by referring to the provided questions and datasets. You can use any tool of your choice (Python, SQL, Power BI, Tableau, Excel) to analyse and answer these questions. 
- Design a recovery dashboard with your metrics and analysis. The dashboard should be self-explanatory and easy to understand. 
- Present your analysis and recommendations to the leadership team with actionable insights.


## Learnings:

### 1. Analytical Strategy & Storytelling Shift:
- Prioritized mapping out the core data story on paper before touching a single visual layout.
  - Outlined the chronological timeline of the operational collapse first saved me from getting backed into a corner where I had to force-fit a narrative around whatever random charts I had already dragged onto the canvas.
- Flipped the dashboard's focus from descriptive reporting to deep diagnostic tracking.
  - Moved past surface-level descriptive data ("Revenue crashed by 70.74%") and intentionally building diagnostic comparisons ("Kitchen prep times are flat across both phases, which means the breakdown is 100% caused by courier transit delays") to answer the executive "why."
- Enforced a strict visual auditing discipline to stay honest and kill personal assumptions.
- Forced myself to slow down and cross-examine new DAX calculations to protect core business logic from warping.


### 2. Technical Data Modeling & Debugging Realities:
- Exposed systemic database logging flaws instead of trusting raw data blindly.
  - Discovered that 5,635 out of 11,112 cancelled orders had missing (NaN) delivery_partner_id values, proving that the vast majority of cancellations happened in a pre-assignment stage before a rider was ever locked in.
- Untangled a major financial mapping error caused by orphaned records.
  - Realized that when the system dropped orders, it zeroed out revenue and left the restaurant_id unmapped. This structural bug falsely dumped the entire ₹3.91M gross loss estimation (11,112 rows × ₹351.75 AOV) straight into the "Independent / Local" bucket.
- Stabilized visual charts across wildly inconsistent historical data phases.
  - Built an internal hardcoded DAX DATATABLE to force empty categories like "Power Users" to remain structurally visible on the X-axis during the crisis phase, even when the underlying data rows dropped to zero.
- Fixed a common Power BI filter glitch caused by restaurant franchises operating in different cities.
  - Tried to display restaurant names right next to their cities in a single visual broke my charts because over 19,600 rows had identical names (like Annapurna Biryani Adda) across different regions. I fixed this by keeping the visual focused strictly on the restaurant itself, and letting the dashboard's city slicer handle the geographic filtering naturally.


 ### 3. Real-World Food Tech Domain Knowledge:
 - Discovered just how fragile a food delivery network really is when logistics break down.
   - Tracked how a seemingly small 15-minute delivery delay triggers an immediate customer backlash, instantly crashing average ratings from an excellent 4.5 stars down to a terrible 2.3.
- Uncovered the real reason restaurants suddenly pull out and quit using the app.
  - Learned that owners turn off their order tablets not because of high platform commissions, but because late drivers leave freshly cooked food sitting cold on the counter; which completely ruins the restaurant's own hard-earned reputation.
- Noticed that operational reliability matters way more to customers than menu prices or food types during a crisis.
  - Found that expensive luxury orders dropped at the exact same rate as cheap budget meals. It proved that hungry customers don't care about discounts or premium branding if they aren't confident the food will actually show up.

## Insights:

- The 18.1-minute average SLA deficit is nearly uniform across all cities, workforce models (contract vs. full-time), and vehicle types (bikes, cars, scooters).
- Kitchens and Couriers are blameless. Physical distances (~4.50 km) and kitchen prep times (~65% completed under 25 minutes) remained completely stable. Top-performing restaurants with prep times under 15 minutes still saw a 94% order drop.
- On-Time Delivery (OTD%) plummeted instantly from 43.10% in May to 12.02% in June, pointing strictly to a broken core dispatch matching algorithm.

  
- Revenue collapsed by 70.92% (dropping from a pre-crisis baseline of ₹37.62M to ₹10.94M).
- The primary financial driver was a ₹25.20M loss due to a systemic customer volume drop, vastly outstripping losses from actual order cancellations (₹1.48M).
- The ~71% drop is identical across all food items (Salads, Juices, Biryani), price tiers (Affordable vs. Premium), and dietary profiles, which maintained a locked 2:1 Veg to Non-Veg ratio.


- The platform suffered a catastrophic 83.81% macro churn rate. Attrition reached a absolute 100.00% for both regular and top 5% VIP customer cohorts exposed to the crisis.
- Some of the Marketing budget was wasted. 12K new customers were acquired during the crisis, but order frequency flatlined at 1.09. Paid channels brought in 14K churned users versus only 3K retained, effectively burning capital.
- Customers begin leaving 1-star reviews at the 40-minute mark; 5-star ratings completely vanish after 55 minutes. Average delivery times of 60.1 minutes have forced the platform entirely into this toxic zone, driving negative sentiment (-0.25).
- The top negative review drivers are "poor food quality" and "stale food." Because kitchen timelines are stable, this proves the platform's transit delays are actively causing meals to spoil before delivery. The bulk of the blame is borne by the restaurants.


- Active merchant supply nearly halved, shrinking 47.19% (from ~13.5K to 7K restaurants).
- Of the remaining base, 50.90% are at "Critical" or "High" risk of churning, with the threat heavily concentrated in Bengaluru, followed by Delhi and Mumbai.


## Strategy:

- Algorithmic Rollback:
  Instantly roll back the dispatch routing, batching, and driver-assignment codebase to the stable mid-May 2025 configuration to resolve matching latency.

- Operational Throttling:
  Temporarily enforce strict order-throttling and shrink delivery radiuses to guarantee no active order is generated with an estimated delivery time exceeding 40 minutes.

- Turn off all paid, social, and referral marketing spend immediately. Stop acquiring new users into a broken machine that yields a 1.09 order frequency.

- Deploy 50% of partner retention and field support resources exclusively to the Bengaluru market to save the highest concentration of "Critical" risk merchants.

- Implement temporary commission relief (such as 0% commission on the next 100 orders) specifically for the 50.90% of merchants sitting in high-risk tiers.

- Stop automated restaurant suspensions triggered by "stale food" or "taste" text reviews. Subsidize thermal/insulated packaging during the interim to protect food integrity against transit delays.

- Automate system triggers to issue an immediate apology and high-value wallet credit within 30 minutes of any delivery that breaches the 40-minute threshold. This actively targets the 5.33-hour average customer "retaliation lag."

- Isolate the data for the 3,684 high-value churned customers. Once delivery metrics normalize under 40 minutes, execute a direct concierge outreach program with high-value financial compensation to win back the platform's core revenue drivers.







