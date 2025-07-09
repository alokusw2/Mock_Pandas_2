# Mock_Pandas_2


q-1: https://leetcode.com/problems/sales-analysis-iii/description/

Write a solution to report the products that were only sold in the first quarter of 2019. That is, between 2019-01-01 and 2019-03-31 inclusive.

Return the result table in any order.

The result format is in the following example.

-----------------------------------------------
import pandas as pd

def sales_analysis(sales: pd.DataFrame) -> pd.DataFrame:
    valid_products = sales.groupby('product_id').filter(
        lambda x: x['sale_date'].min() >= '2019-01-01' and x['sale_date'].max() <= '2019-03-31'
    )
    return valid_products[['product_id']].drop_duplicates()



------------------------------------------------


------------------------------------------------
Q-2: https://leetcode.com/problems/market-analysis-i/description/

------------------------------------------------
Write a solution to find for each user, the join date and the number of orders they made as a buyer in 2019.

Return the result table in any order.

The result format is in the following example.

------------------------------------------------

import pandas as pd

def market_analysis(users: pd.DataFrame, orders: pd.DataFrame) -> pd.DataFrame:
    feb_orders = orders[orders['order_date'].between('2019-02-01', '2019-02-28')]
    active_users = feb_orders['buyer_id'].drop_duplicates()
    users['has_ordered'] = users['user_id'].isin(active_users)
    return users[['user_id', 'join_date', 'has_ordered']]

