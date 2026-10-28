Representation of a Real-World Problem as a Markov Decision Process (Smart Water Bottle)
Aim
To identify the Smart Water Bottle as a real-world sequential decision-making problem and represent it as a Markov Decision Process (MDP) by defining its states, actions, transition probabilities, reward function, and discount factor using Python dictionaries.

Problem Statement
Problem Description
The Smart Water Bottle is an intelligent system that monitors the amount of water remaining in a bottle and helps a person maintain proper hydration. The system considers three states: Bottle Full, Bottle Half Full, and Bottle Low.

The agent can perform two actions: Drink Water and Refill Bottle. When the person drinks water, the water level decreases. When the person refills the bottle, the water level becomes full.

The system assigns rewards for maintaining sufficient water and refilling the bottle when necessary. A negative reward is assigned when the bottle is low and the person continues drinking without refilling it. The objective is to encourage proper hydration and timely refilling using a Markov Decision Process.

MDP Components
A Markov Decision Process is represented as:
\[
MDP = (S, A, P, R, \gamma)
\]

Symbol	Meaning
\(S\)	Set of states
\(A\)	Set of actions
\(P\)	Transition probability function
\(R\)	Reward function
\(\gamma\)	Discount factor


State Space
The state space represents all possible water levels in the Smart Water Bottle.
S = {
    S1: Bottle Full,
    S2: Bottle Half Full,
    S3: Bottle Low
}


- S1 – Bottle Full: The bottle contains sufficient water.
- S2 – Bottle Half Full: The bottle contains half of its capacity.
- S3 – Bottle Low: The bottle contains very little water and needs refilling.

Sample State
Sample State: S3 – Bottle Low

The bottle contains very little water. The system should encourage the person to refill the bottle to maintain sufficient water availability.

Action Space
The action space represents the actions available to the agent.
A = {
    A1: Drink Water,
    A2: Refill Bottle
}


- A1 – Drink Water: The person drinks water from the bottle, decreasing its water level.
- A2 – Refill Bottle: The person refills the bottle, restoring it to the full state.

Sample Action
Sample Action: A2 – Refill Bottle

When the bottle is low, the agent selects the Refill Bottle action. The bottle transitions to the Bottle Full state and receives a reward of +10.

Transition Probability
The transition probability specifies the probability of reaching the next state after performing an action in the current state.
\[
P(s' \mid s,a)
\]

The transition probabilities for the Smart Water Bottle are:
Current State	Action	Next State	Probability
Bottle Full	Drink Water	Bottle Half Full	1.0
Bottle Full	Refill Bottle	Bottle Full	1.0
Bottle Half Full	Drink Water	Bottle Low	1.0
Bottle Half Full	Refill Bottle	Bottle Full	1.0
Bottle Low	Drink Water	Bottle Low	1.0
Bottle Low	Refill Bottle	Bottle Full	1.0

All transition probabilities are 1.0, meaning each action produces a deterministic transition in this simplified model.

Reward Function
The reward function defines the feedback received by the agent after performing an action.
\[
R(s,a,s')
\]

The rewards are assigned as follows:
Current State	Action	Reward	Reason
Bottle Full	Drink Water	+5	Encourages drinking water
Bottle Full	Refill Bottle	+1	Small reward for refilling
Bottle Half Full	Drink Water	+5	Encourages hydration
Bottle Half Full	Refill Bottle	+8	Encourages maintaining sufficient water
Bottle Low	Drink Water	-5	Discourages drinking when water is nearly exhausted
Bottle Low	Refill Bottle	+10	Strongly encourages refilling

A higher reward indicates a preferred action, while a negative reward discourages an undesirable action.

Graphical Representation
The MDP can be represented using the following state transitions.
S1: Bottle Full

Drink Water · P = 1.0 · R = +5
S2: Bottle Half Full

Drink Water · P = 1.0 · R = +5
S3: Bottle Low



Refill transitions
- S1 → S1: Refill Bottle, P = 1.0, R = +1
- S2 → S1: Refill Bottle, P = 1.0, R = +8
- S3 → S1: Refill Bottle, P = 1.0, R = +10
  
  At S3, Drink Water keeps the bottle in S3 with P = 1.0 and R = −5.


Python Representation
The following Python program uses dictionaries to represent the states, actions, transition probabilities, reward function, and discount factor.
print("Name: Rakisha R")print("Register Number: 212224240031")# State Spacestates = {    "S1": "Bottle Full",    "S2": "Bottle Half Full",    "S3": "Bottle Low"}# Action Spaceactions = {    "A1": "Drink Water",    "A2": "Refill Bottle"}# Transition Probabilitiestransitions = {    ("S1", "A1"): ("S2", 1.0),    ("S1", "A2"): ("S1", 1.0),    ("S2", "A1"): ("S3", 1.0),    ("S2", "A2"): ("S1", 1.0),    ("S3", "A1"): ("S3", 1.0),    ("S3", "A2"): ("S1", 1.0)}# Reward Functionrewards = {    ("S1", "A1"): 5,    ("S1", "A2"): 1,    ("S2", "A1"): 5,    ("S2", "A2"): 8,    ("S3", "A1"): -5,    ("S3", "A2"): 10}




Output
Name: Rakisha R
Register Number: 212224240031

--- MDP DETAILS ---
State              Action          Transition         Reward     Probability
Bottle Full        Drink Water     Bottle Half Full   5          1.0
Bottle Full        Refill Bottle   Bottle Full        1          1.0
Bottle Half Full   Drink Water     Bottle Low         5          1.0
Bottle Half Full   Refill Bottle   Bottle Full        8          1.0
Bottle Low         Drink Water     Bottle Low         -5         1.0
Bottle Low         Refill Bottle   Bottle Full        10         1.0

Discount Factor (Gamma): 1.0
Future rewards are not discounted.



Result
Thus, the Smart Water Bottle problem was successfully represented as a Markov Decision Process using Python dictionaries. The state space, action space, transition probabilities, reward function, and discount factor were defined. The program displays all possible state transitions, their corresponding rewards, and transition probabilities, demonstrating how an MDP can model real-world sequential decision-making.
