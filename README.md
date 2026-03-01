# Work in Progress - NOT OPEN TO PUBLIC

# Event Ticket Bidding - 2026

## Background
A significant sporting tournament featuring 100 matches is scheduled to take place in the United States. Data on the spot ticket prices, collected during the 100 hours preceding the game's start, is already available for the first 50 matches. The objective is to design a trading algorithm to automate the buying and selling of tickets for the remaining 50 matches.

---

## How It Works
For simplicity, the following assumptions and setups were defined:

### Tickets and Pricing Data
* There are only three categories of tickets for each match.
* Tickets within each category are deemed the same and the clearing price is always the same within a category at the given time.
* The data for the first 50 matches are indicative of the next 50 matches with random noises as they are deemed as similar matches (e.g., all of them are group stage matches).
* Pricing data is discrete, with the clearing price at the end of each 1-100 hours.
* For each match, the clearing data has three columns (by ticket category) and 100 rows (by time).

**Sample Pricing Data Table**

| num_hour | num_match | price_cat_1 | price_cat_2 | price_cat_3 |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 154 | | |
| 2 | 1 | 132 | | |
| 3 | 1 | 98 | | |
| ... | | | | |
| 1 | 2 | | | |
| 2 | 2 | | | |
| ... | | | | |

### Market Clearing
For simplicity, you and other participants of the contest only trade with the general market but not between yourselves. 
* At each hour, there are *x* ticket purchases by the market and *y* ticket sales demand by the general market - both at the market clearing price. 
* Note that you do not observe *x* and *y*. Both *x* and *y* are set at sufficiently high numbers that are comparable to the budget and participants in this contest.

**Buying Tickets**
You successfully buy tickets when:
1. Your bidding price is >= the clearing price.
2. You have sufficient budget.

* **Settlements between multiple bidders:** The *x* tickets are randomly distributed between all bidders that meet the above conditions.

**Selling Tickets**
You successfully sell tickets when:
1. Your asking price is <= the clearing price.
2. You have ticket holdings from prior successful bidding.

* **Settlements between multiple sellers:** The seller with the lowest asking price lower than the clearing price sells first, then the 2nd lowest, etc. When there’s a tie in the asking price and the remaining demand is less than the number of tickets that are offered, the transactions are randomly distributed.

### Budget
* You have a limited $10,000 starting budget to do your trades and you cannot borrow money.
* The profits from past transactions can be immediately used for future trades.

### Winning Evaluation
* Tickets that are unsold after each of the games start (after the 100th hour) are worth $0.
* The rest of the 50 games take place sequentially with no overlap of their 100 hours.
* Your profits from the earlier match become your budget for the next match’s trading.
* The performance of the algo is measured by the total profit net the $10,000 starting budget.

---

## Your Submissions
Two submissions are required in order to participate:
1. A table with 100 rows and 13 columns to specify your market making strategy.
2. A document that is no more than 2 pages to explain how you came up with your strategy and the key considerations of your strategy.

> **Note:** Accompanying workbooks and code can be supplied to supplement the document. Out of 100 total points that are graded for each submission, 70 points are awarded based on the final profit.

**Notes on the Table Submission**:
* Use `0` and `9999` to indicate no bidding price and no asking price accordingly if needed.
* Use `9999` to indicate bidding and selling the highest possible volume as long as the conditions permit (i.e., budget, market volume).

**Submission Data Format**

| num_hour | price_cat_1_bid_prc | price_cat_1_bid_vol | price_cat_1_ask_prc | price_cat_1_ask_vol | price_cat_2_bid_prc | price_cat_2_bid_vol | price_cat_2_ask_prc | price_cat_2_ask_vol | price_cat_3_bid_prc | price_cat_3_bid_vol | price_cat_3_ask_prc | price_cat_3_ask_vol |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 100 | 5 | 300 | 9999 | | | | | | | | |
| 2 | 132 | | | | | | | | | | | |
| 3 | 98 | | | | | | | | | | | |
| ... | | | | | | | | | | | | |
| 100 | | | | | | | | | | | | |

---

## Key Questions
Comparison to the asteroid bidding contest setting, this one is:
* Relying less on large data modeling but more strategic planning and understanding of the problem statement.
* More inclusive of different problem-solving strategies to allow entries of participants from various backgrounds (math vs. computer science).
* Lower level of effort to complete (?)
* Easier to grade on our end (?)
