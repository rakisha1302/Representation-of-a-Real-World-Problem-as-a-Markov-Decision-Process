# EXPERIMENT: REPRESENTATION OF A REAL-WORLD PROBLEM AS A MARKOV DECISION PROCESS (SMART WATER BOTTLE)

## 1. AIM

To identify the Smart Water Bottle as a real-world sequential decision-making problem and represent it as a Markov Decision Process (MDP) by defining its state space, action space, transition probabilities, reward function, and discount factor using Python dictionaries.

## 2. PROBLEM STATEMENT

The Smart Water Bottle is an intelligent system that monitors the amount of water remaining in a bottle and helps a person maintain proper hydration. The system consists of three states: Bottle Full, Bottle Half Full, and Bottle Low.

The agent can perform two actions: Drink Water and Refill Bottle. Drinking water decreases the water level, whereas refilling restores the bottle to its full capacity.

The system assigns positive rewards for maintaining sufficient water and refilling the bottle when necessary. A negative reward is assigned when the bottle is low and the person continues drinking without refilling it. The objective is to encourage proper hydration and timely refilling using a Markov Decision Process.

## 3. THEORY

A Markov Decision Process (MDP) is a mathematical framework used to model sequential decision-making problems in which an agent selects actions based on the current state and receives rewards.

An MDP is represented as:

\[
MDP=(S,A,P,R,\gamma)
\]

Where:

- **S – State Space:** Set of all possible states.
- **A – Action Space:** Set of actions available to the agent.
- **P – Transition Probability:** Probability of reaching the next state after taking an action.
- **R – Reward Function:** Immediate reward received after performing an action.
- **γ – Discount Factor:** Determines the importance of future rewards.

## 4. STATE SPACE

The state space represents all possible water levels in the Smart Water Bottle.

```python
states = {
    "S1": "Bottle Full",
    "S2": "Bottle Half Full",
    "S3": "Bottle Low"
}
```

The states are described as follows:

- **S1 – Bottle Full:** The bottle contains sufficient water.
- **S2 – Bottle Half Full:** The bottle contains approximately half of its capacity.
- **S3 – Bottle Low:** The bottle contains very little water and needs refilling.

**Sample State:** S3 – Bottle Low.

When the bottle is low, the system should encourage the person to refill it to maintain sufficient water availability.

## 5. ACTION SPACE

The action space represents the actions available to the agent.

```python
actions = {
    "A1": "Drink Water",
    "A2": "Refill Bottle"
}
```

The available actions are:

- **A1 – Drink Water:** Decreases the water level in the bottle.
- **A2 – Refill Bottle:** Restores the bottle to its full state.

**Sample Action:** A2 – Refill Bottle.

When the bottle is low, the agent can select the Refill Bottle action, causing a transition to the Bottle Full state and receiving a reward of +10.

## 6. TRANSITION PROBABILITY

The transition probability specifies the probability of reaching the next state after performing an action in the current state.

\[
P(s' \mid s,a)
\]

The transition probabilities are defined as follows:

| Current State | Action | Next State | Probability |
|---|---|---|---:|
| Bottle Full | Drink Water | Bottle Half Full | 1.0 |
| Bottle Full | Refill Bottle | Bottle Full | 1.0 |
| Bottle Half Full | Drink Water | Bottle Low | 1.0 |
| Bottle Half Full | Refill Bottle | Bottle Full | 1.0 |
| Bottle Low | Drink Water | Bottle Low | 1.0 |
| Bottle Low | Refill Bottle | Bottle Full | 1.0 |

All transition probabilities are 1.0, indicating that the model uses deterministic transitions. Each state-action pair leads to exactly one next state.

## 7. REWARD FUNCTION

The reward function defines the feedback received by the agent after performing an action.

\[
R(s,a,s')
\]

The reward values are assigned as follows:

| Current State | Action | Reward | Reason |
|---|---|---:|---|
| Bottle Full | Drink Water | +5 | Encourages hydration |
| Bottle Full | Refill Bottle | +1 | Assigns a small reward for refilling |
| Bottle Half Full | Drink Water | +5 | Encourages hydration |
| Bottle Half Full | Refill Bottle | +8 | Encourages maintaining sufficient water |
| Bottle Low | Drink Water | -5 | Discourages drinking when water is nearly exhausted |
| Bottle Low | Refill Bottle | +10 | Strongly encourages refilling |

A positive reward encourages desirable behaviour, while a negative reward discourages undesirable behaviour.

## 8. DISCOUNT FACTOR

The discount factor determines the importance of future rewards in comparison with immediate rewards.

\[
\gamma = 1.0
\]

Since the discount factor is 1.0, future rewards are not discounted. Immediate and future rewards are considered equally important in the discounting calculation.

## 9. GRAPHICAL REPRESENTATION

The state transitions of the Smart Water Bottle MDP are represented below.

```text
                  Drink Water
       +--------------------------------+
       |                                v
+----------------+              +---------------------+
| S1: Bottle Full|              | S2: Bottle Half Full|
+----------------+              +---------------------+
       ^                                |
       |                                | Drink Water
       |                                v
       |                         +----------------+
       |                         | S3: Bottle Low |
       |                         +----------------+
       |                                |
       |                                | Drink Water
       |                                v
       |                         +----------------+
       |                         | S3: Bottle Low |
       |                         +----------------+
       |
       +---------- Refill Bottle --------+
```

Additional refill transitions:

- S1 → S1: Refill Bottle, P = 1.0, R = +1.
- S2 → S1: Refill Bottle, P = 1.0, R = +8.
- S3 → S1: Refill Bottle, P = 1.0, R = +10.

The transition S3 → S3 occurs when the agent selects Drink Water, with P = 1.0 and R = -5.

## 10. PYTHON PROGRAM

```python
print("Name: Rakisha R")
print("Register Number: 212224240031")

# State Space
states = {
    "S1": "Bottle Full",
    "S2": "Bottle Half Full",
    "S3": "Bottle Low"
}

# Action Space
actions = {
    "A1": "Drink Water",
    "A2": "Refill Bottle"
}

# Transition Probabilities
transitions = {
    ("S1", "A1"): ("S2", 1.0),
    ("S1", "A2"): ("S1", 1.0),
    ("S2", "A1"): ("S3", 1.0),
    ("S2", "A2"): ("S1", 1.0),
    ("S3", "A1"): ("S3", 1.0),
    ("S3", "A2"): ("S1", 1.0)
}

# Reward Function
rewards = {
    ("S1", "A1"): 5,
    ("S1", "A2"): 1,
    ("S2", "A1"): 5,
    ("S2", "A2"): 8,
    ("S3", "A1"): -5,
    ("S3", "A2"): 10
}

# Discount Factor
gamma = 1.0

# Display MDP Details
print("\n--- MDP DETAILS ---")
print(f"{'State':<20}{'Action':<18}"
      f"{'Transition':<22}{'Reward':<10}"
      f"{'Probability':<12}")

for (state, action), (next_state, probability) in transitions.items():
    print(f"{states[state]:<20}"
          f"{actions[action]:<18}"
          f"{states[next_state]:<22}"
          f"{rewards[(state, action)]:<10}"
          f"{probability:<12}")

print(f"\nDiscount Factor (Gamma): {gamma}")
print("Future rewards are not discounted.")
```

## 11. OUTPUT

```text
Name: Rakisha R
Register Number: 212224240031

--- MDP DETAILS ---
State               Action            Transition           Reward    Probability
Bottle Full         Drink Water       Bottle Half Full     5         1.0
Bottle Full         Refill Bottle     Bottle Full           1         1.0
Bottle Half Full    Drink Water       Bottle Low            5         1.0
Bottle Half Full    Refill Bottle     Bottle Full           8         1.0
Bottle Low          Drink Water       Bottle Low           -5         1.0
Bottle Low          Refill Bottle     Bottle Full           10        1.0

Discount Factor (Gamma): 1.0
Future rewards are not discounted.
```

## 12. RESULT

Thus, the Smart Water Bottle problem was successfully represented as a Markov Decision Process using Python dictionaries. The state space, action space, transition probabilities, reward function, and discount factor were defined. The program successfully displays all possible state transitions, their corresponding rewards, and transition probabilities, demonstrating how an MDP can model a real-world sequential decision-making problem.
