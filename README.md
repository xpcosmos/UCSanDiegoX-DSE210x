# Monte Carlo Simulation for Card Probability

This project replicates an example presented in the course "Probability and Statistics in Data Science using Python." The scenario involves three cards placed inside a box, each with specific color characteristics. The goal is to determine the probability that, when one card is randomly drawn from the box, both sides have the same color. We'll achieve this by implementing a Monte Carlo simulation.

## Introduction to the Problem

In this scenario, we have three cards:

1. The first card has one blue side and one red side.
2. The second card has both sides blue.
3. The third card has both sides red.

Our task is to find the probability that, when randomly selecting a card from the box, both sides have the same color.

## Coding the Solution

We will simulate this scenario using Python. First, we define the possible events representing the card combinations: 'RR' (both sides red), 'BB' (both sides blue), 'RB' (one side red and one side blue), and 'BR' (one side blue and one side red).

```python
import pandas as pd 
import numpy as np
import matplotlib.pyplot as plt

# Defining the possible events:
events = np.array(['RR', 'BB', 'RB', 'BR'])

# Where n = number of simulations 
def simulate(n):
    # Creating variables referring to events where the cards are equal or different
    equal_card = 0
    different_card = 0

    # Simulation. The number of simulations is equal to 100, but it can be modified
    for i in range(n):
        
        # Defining choosing a random event.
        chosen_event = np.random.choice(events)
        
        # Calculation the sum of occurrences for a specific event
        if chosen_event in ['RR', 'BB']:
            equal_card += 1
        elif chosen_event in ['RB', 'BR']:
            different_card += 1

    # Consolidating the results 
    return {'equal_card': equal_card, 'different_card': different_card}

print(simulate(100))
```

This code simulates the scenario 100 times and returns the count of occurrences for equal and different cards.

## Creating Probability Distribution

To further analyze the results, we create a probability distribution by running the simulation 100,000 times and calculating the difference between the counts of equal and different cards.

```python
distribution = []

for i in range(100_000):
    list_of_values = list(simulate(1000).values())
    difference = list_of_values[0] - list_of_values[1]
    distribution.append(difference)

plt.hist(np.array(distribution))
```

## Results

Considering that the mean of the differences in the probability distribution is 0 and the difference between probabilities tends towards 0, we can confidently conclude that both events (equal and different cards) have equal probabilities of occurring. This aligns with the intuition that if the events occur with the same frequency, the difference between them should be 0.

For more details and insights into the Monte Carlo simulation results, refer to the Jupyter Notebook in this repository.
