# montecarlo
Marketing Campaign

import numpy.random as rnd
import numpy as np

result = []
def monte_carlo_coin(probability):
    r = rnd.uniform()
    return int(r < probability)

def profit(n_sales, n_contacts):
    avg_income_sale = 10.0
    avg_costs_contact = 2.0
    return n_sales*avg_income_sale - n_contacts*avg_costs_contact
    
    
    
    
for min_probability in np.arange(0.0,0.9,0.1):
    for max_probability in np.arange(min_probability+0.1,1.0,0.1):
        # uplift
        target_group = data.probabilities.between(min_probability, max_probability)
        data_after_contact = data.copy()
        data_after_contact.ix[target_group, 'probabilities'] = data.ix[target_group].probabilities + 0.1
        
        prof = 0
        for _ in range(10):
            # simulation
            data_after_contact['sales'] = data_after_contact['probabilities'].apply(monte_carlo_coin)

            # results
            sales = data_after_contact['sales'].sum(axis=0)
            calls = target_group.sum(axis=0)
            prof += profit(sales, calls)
        prof /= 10
        result.append((min_probability, max_probability, sales, calls, prof))
