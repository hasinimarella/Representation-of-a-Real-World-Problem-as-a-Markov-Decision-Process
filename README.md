# Representation-of-a-Real-World-Problem-as-a-Markov-Decision-Process


## Aim
To identify a real-world sequential decision-making problem and represent it formally as a Markov Decision Process by defining its states, actions, rewards, transitions, and Python representation.

---

## Problem Statement
Smart thermostats must decide when to heat, cool, or stay idle in order to keep a room at a comfortable temperature while minimizing energy usage. Since the room's next temperature depends only on its current temperature and the action taken (not on the full history), this problem can be modeled as a Markov Decision Process. The goal is to define the states, actions, transition probabilities, and rewards for this system so that an optimal climate-control policy can eventually be learned.
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
```



---

## Sample State


A sample state is one specific example from the state space.

s = "Cold"

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


A sample action is one action selected from the action space.

a = "Heat"

---

## Transition Probability

Write your answer here.

The transition probability explains how the environment moves from one state to another after an action is taken.

General form:

$$
P(s' \mid s,a)
$$

This means:

> Probability of reaching next state $s'$ after taking action $a$ in current state $s$.


---

## Reward Function

Write your answer here.

The reward function defines the feedback received by the agent after taking an action.

General form:

$$
R(s,a,s')
$$



---

## Graphical Representation

Write your answer here.

Draw the MDP graph.

The graph should include:

1. States as nodes.
2. Actions as arrows.
3. Rewards on transitions.
4. Transition probabilities if applicable.


---

## Python Representation

Write your code here.

Use Python dictionaries to represent the MDP.


```python
# MDP Representation using Python
# print("Name:       ")
# print("Register Number:     ")

```
---
## Output

Write your Python output here.


---

## Result

Write your result here.



---

