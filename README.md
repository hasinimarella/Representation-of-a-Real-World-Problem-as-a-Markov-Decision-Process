# Representation-of-a-Real-World-Problem-as-a-Markov-Decision-Process


## Aim
To identify a real-world sequential decision-making problem and represent it formally as a Markov Decision Process by defining its states, actions, rewards, transitions, and Python representation.

---

## Problem Statement

Design a Smart Thermostat Climate Control System that decides whether to Heat, Cool, or Stay Idle based on the current room temperature to maintain occupant comfort while minimizing energy consumption. Model this decision-making process as a Markov Decision Process (MDP) by defining its states, actions, transition probabilities, and rewards.

### Problem Description

A smart thermostat must decide, at each time step, whether to heat, cool, or stay idle in order to keep a room's temperature within a comfortable range while minimizing energy use. Since the next temperature depends only on the current temperature and the action taken (not on past history), this decision-making problem can be formally modeled as a Markov Decision Process.


---

## MDP Components

A Markov Decision Process is represented as:

$$
MDP = (S, A, P, R, \gamma)
$$

Where:

| Symbol | Meaning |
|---|---|
| $S$ | Set of states |
| $A$ | Set of actions |
| $P$ | Transition probability function |
| $R$ | Reward function |
| $\gamma$ | Discount factor |

---

## State Space

Write your answer here.

The state space should list all possible situations in which the agent can exist.

Example format:

```text
S = {
    Too_Cold,       # < 16°C
    Cold,           # 16–19°C
    Comfortable,    # 20–24°C
    Warm,           # 25–28°C
    Too_Hot         # > 28°C
}
}
```



---

## Sample State
s = "Cold"

A sample state is one specific example from the state space.



---

## Action Space



The action space should list all possible actions available to the agent.

Example format:

```text
A = {
    Heat,     # turn on the heater
    Cool,     # turn on the air conditioner
    Idle      # take no action
}
```


---

## Sample Action

a = "Heat"

A sample action is one action selected from the action space.



---

## Transition Probability

The transition probability P(s' | s, a) gives the probability of moving to a next state s' given the current state s and action a. Taking Heat biases the system toward warmer states, Cool biases toward colder states, and Idle allows natural drift (usually toward Comfortable or staying the same, since rooms without intervention tend to equalize with drift/noise).

Example — from state Cold:
```
```
<img width="801" height="412" alt="image" src="https://github.com/user-attachments/assets/f853efd0-b268-40f2-9de6-3a19d7e8a329" />


This is written formally as, e.g.:
```
P(Comfortable | Cold, Heat) = 0.7
P(Cold | Cold, Heat) = 0.2
P(Warm | Cold, Heat) = 0.1
```

Reward Function
```
R(s, a, s') gives the feedback the agent receives. The reward is designed to:

Give a high reward for reaching/staying in Comfortable.
Give a penalty for extreme states (Too_Cold, Too_Hot) since occupant discomfort is costly.
Give a small energy penalty whenever Heat or Cool is used (since running the appliance costs electricity), and zero energy cost for Idle.
```
Example reward values:
```
R(s, a, "Comfortable") = +10   (any transition landing in Comfortable)
R(s, a, "Too_Cold")    = -10
R(s, a, "Too_Hot")     = -10
Energy penalty: Heat -> -2, Cool -> -2, Idle -> 0  (added to the above)
So overall reward = comfort_reward(s') + energy_cost(a)
```

---

## Graphical Representation


Draw the MDP graph.

The graph should include:

1. States as nodes.
2. Actions as arrows.
3. Rewards on transitions.
4. Transition probabilities if applicable.

<img width="1174" height="1339" alt="ChatGPT Image Aug 3, 2026, 01_23_58 PM" src="https://github.com/user-attachments/assets/95d21608-5964-4128-b091-ef31bedac432" />



---

## Python Representation

Use Python dictionaries to represent the MDP.
```python
# MDP Representation using Python
print("Name: MARELLA HASINI")
print("Register Number: 212223240083")

# ---- State Space ----
states = ["Too_Cold", "Cold", "Comfortable", "Warm", "Too_Hot"]

# ---- Action Space ----
actions = ["Heat", "Cool", "Idle"]

# ---- Transition Probability Function P(s' | s, a) ----
# Structure: P[state][action] = { next_state: probability, ... }
P = {
    "Too_Cold": {
        "Heat": {"Too_Cold": 0.2, "Cold": 0.7, "Comfortable": 0.1},
        "Cool": {"Too_Cold": 1.0},
        "Idle": {"Too_Cold": 0.8, "Cold": 0.2},
    },
    "Cold": {
        "Heat": {"Cold": 0.2, "Comfortable": 0.7, "Warm": 0.1},
        "Cool": {"Too_Cold": 0.6, "Cold": 0.4},
        "Idle": {"Too_Cold": 0.4, "Cold": 0.6},
    },
    "Comfortable": {
        "Heat": {"Comfortable": 0.6, "Warm": 0.4},
        "Cool": {"Cold": 0.4, "Comfortable": 0.6},
        "Idle": {"Comfortable": 1.0},
    },
    "Warm": {
        "Heat": {"Warm": 0.4, "Too_Hot": 0.6},
        "Cool": {"Comfortable": 0.7, "Warm": 0.2, "Cold": 0.1},
        "Idle": {"Warm": 0.6, "Too_Hot": 0.4},
    },
    "Too_Hot": {
        "Heat": {"Too_Hot": 1.0},
        "Cool": {"Warm": 0.7, "Too_Hot": 0.3},
        "Idle": {"Too_Hot": 0.8, "Warm": 0.2},
    },
}

# ---- Reward Function R(s, a, s') ----
comfort_reward = {
    "Too_Cold": -10,
    "Cold": -2,
    "Comfortable": 10,
    "Warm": -2,
    "Too_Hot": -10,
}
energy_cost = {"Heat": -2, "Cool": -2, "Idle": 0}

def reward(state, action, next_state):
    return comfort_reward[next_state] + energy_cost[action]

# ---- Discount Factor ----
gamma = 0.9

# ---- Demonstration: simulate one step from a sample state/action ----
import random

def take_action(state, action):
    outcomes = P[state][action]
    next_states = list(outcomes.keys())
    probs = list(outcomes.values())
    next_state = random.choices(next_states, weights=probs, k=1)[0]
    r = reward(state, action, next_state)
    return next_state, r

sample_state = "Cold"
sample_action = "Heat"
next_state, r = take_action(sample_state, sample_action)

print(f"\nCurrent state: {sample_state}")
print(f"Action taken: {sample_action}")
print(f"Next state: {next_state}")
print(f"Reward received: {r}")
print(f"Discount factor (gamma): {gamma}")
```
---
## Output

<img width="222" height="142" alt="image" src="https://github.com/user-attachments/assets/977f480b-fb6a-45d1-856f-798f6f3aa718" />



---

## Result
The smart thermostat problem was successfully modeled as an MDP with defined states, actions, transitions, and rewards, and implemented in Python — confirming it satisfies the Markov property and can be effectively represented using MDP formalism.



---

