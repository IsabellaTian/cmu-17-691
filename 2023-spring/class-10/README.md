# Appling ML Concepts to DA
## Decision
### Classical Decision # vs. Analysis Effort
- CDT is a normative approach that assumes people make decisions by selecting the option that maximizes their expected utility.
- Analysis Effort is the amount of time and resources invested in analyzing a decision problem before making a decision.
- The Classical Decision Theory vs. Analysis Effort curve shows the tradeoff between decision accuracy and analysis effort.
- At low levels of analysis effort, decisions are made quickly and may be suboptimal due to important information being overlooked.
- As analysis effort increases, decision quality improves and the likelihood of making an optimal decision increases.
- ![image](https://user-images.githubusercontent.com/59854195/233735482-dd66fe50-f655-4df3-90c6-cba1d577f15b.png)

### Decision Modeling Characteristics
#### Clairvoyance
## In-Class Exercise
Using your function, assuming model sensitivity and specificity are the same, find the point of model quality (sensitivity and specificity) we are indifferent to having the sensor/model.
Plot the value of data (difference between not buying the sensor and buying the sensor) against various sensitivity/specificity (range 0-1 by .01 increments). Paste this plot and your answer to the previous task on your team slide.

```python
def predidct_value(p_storm, sensitivity, specificity, payout_of_harvest, payout_of_no_harvest_storm, payout_of_no_harvest_and_no_storm):
    p_dns = (specificity * (1 - p_storm) + p_storm * (1 - specificity))
    p_ns_dns = specificity * (1 - p_storm) / p_dns
    p_ds = (sensitivity * p_storm) + ( 1 - p_storm) * (1 - sensitivity)
    p_s_ds = (sensitivity * p_storm) / p_ds
    value_no_storm = max(payout_of_harvest, p_ns_dns * payout_of_no_harvest_and_no_storm + (1 - p_ns_dns) * payout_of_no_harvest_storm)
    value_storm = max(payout_of_harvest, p_s_ds * payout_of_no_harvest_storm + payout_of_no_harvest_and_no_storm * (1 - p_s_ds))
    value_no_harvest = p_dns * value_no_storm + p_ds* value_storm
    return abs(value_no_harvest - payout_of_harvest)
```
These code calculate the overall expected value (value_no_harvest) based on the probabilities of a storm and no storm, and the expected values of harvesting and not harvesting. It then returns the absolute difference between the expected value and the payout of harvesting.

```python
import matplotlib.pyplot as plt
fig, ax = plt.subplots()

x = [x/100 for x in range(1, 101)]
y = [predidct_value(0.75, x/100, x/100, 1000, 500, 1500) for x in range(1,101)]
ax.plot(x, y)


ax.grid(True)
plt.show()
```
![image](https://user-images.githubusercontent.com/59854195/233735445-93e77abb-157c-4a4f-8a34-86d7ebc6d3c5.png)

The code above is using the matplotlib library to create a graph of the output of the predict_value function for different values of sensitivity and specificity. 
From 0.25 to 0.75, model quality (sensitivity and specificity) we are indifferent to having the sensor/model.
