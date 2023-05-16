# Votings
In this project, I devised and implemented multiple voting algorithms. The objective of these algorithms is to determine a winning alternative within a voting scenario. The scenario involves a group of n agents and a set of m alternatives. Each agent possesses a preference ordering, denoted as ≻, where α ≻ β signifies that the agent prefers alternative α over alternative β. A preference profile encompasses n preference orderings, one for each agent. For instance, considering a voting scenario with 4 agents and 4 alternatives, a potential preference profile might be as follows:

Agent 1: α≻γ≻β≻δ
Agent 2: α≻β≻δ≻γ
Agent 3: γ≻β≻α≻δ
Agent 4: β≻α≻δ≻γ

A voting rule is a function that takes the preferences of a group of agents as input and produces the winning alternative as output.
