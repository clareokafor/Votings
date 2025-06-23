# Voting Rules and Algorithms

## Overview

This project develops and implements multiple voting algorithms designed to determine a winning alternative from a set of options based on a group of agents’ ranked preferences. In a typical voting scenario, each of *n* agents provides a complete ranking over *m* alternatives. A voting rule is then applied to aggregate these rankings into a single winning alternative.

For instance, in a scenario with 4 agents and 4 alternatives, one possible preference profile might be:

- **Agent 1:** α ≻ γ ≻ β ≻ δ  
- **Agent 2:** α ≻ β ≻ δ ≻ γ  
- **Agent 3:** γ ≻ β ≻ α ≻ δ  
- **Agent 4:** β ≻ α ≻ δ ≻ γ  

This repository implements a variety of voting rules that extract a winner from such a profile.

## Algorithms Implemented

The following voting rules and functions are implemented:

- **Preference Generation (`generatePreferences`)**  
  Reads data (for example from an Excel file via openpyxl) and converts it into a dictionary of preference orderings. Each key is an agent (starting at 1), and the value is a list of alternative indices sorted from most to least preferred. The function uses NumPy to ease sorting and indexing, while adjusting for 1-indexing.

- **Dictatorship (`dictatorship`)**  
  Returns the top-ranked alternative chosen by a specific agent. If the agent’s ID is valid, the function simply returns the first alternative in that agent’s preference list.

- **Scoring Rule (`scoringRule`)**  
  A generic function that works with any scoring rule by assigning points to alternatives based on a score vector. It iterates over each agent’s preferences and sums scores assigned to each alternative. In the case of ties, a tie-breaking function (described below) is invoked.

- **Tie Breaking (`tieBreaking`)**  
  Resolves ties among alternatives using one of several rules:
  - **"max":** Selects the alternative with the maximum index.
  - **"min":** Selects the alternative with the minimum index.
  - **Agent-specific:** Uses the ranking provided by a designated agent to determine which alternative should win.

- **Plurality (`plurality`)**  
  Determines the winner by counting the frequency of each alternative appearing in the first position across all agents’ preference orders. In the event of a tie, the tie-breaking rule is applied.

- **Veto (`veto`)**  
  Every agent assigns 0 points to the alternative ranked last and 1 point to all the rest. The alternative with the highest total (via the scoring rule) wins, with ties handled using the designated method.

- **Borda Count (`borda`)**  
  Implements the Borda count method where each alternative receives a score based on its position in the ranking (for example, 0 points for the least preferred; higher points for higher-ranked alternatives). Ties are broken, if necessary, using the tie-breaking function.

- **Harmonic Rule (`harmonic`)**  
  Similar to Borda count, but alternative scores are determined by a harmonic series; that is, 1 point is given to the top alternative, 1/2 to the second, 1/3 to the third, and so on.

- **Single Transferable Vote (`STV`)**  
  Uses an elimination process: at each stage, the alternative with the least number of first-place votes is eliminated, the preference orders are updated, and the process is repeated until a single alternative remains. Tie-breaking is applied if necessary.

- **Range Voting (`rangeVoting`)**  
  Aggregates the values from a numerical worksheet (via openpyxl). Each alternative’s score is obtained by summing the values provided by each agent. The winning alternative is the one with the highest total score, with tie-breaking applied when needed.

## Voting Scenario and Preference Profile

The voting setup assumes:
- A group of *n* agents.
- A set of *m* alternatives.
- Each agent submits a complete ranking (preference order) of the alternatives.
- The overall task is to select a single winning alternative using one of several voting rules.

For example, in a 4-agent, 4-alternative situation, a complete preference profile is generated, and one may apply the plurality rule, Borda count, or other methods to extract the winner. This project demonstrates several approaches for differing decision contexts.

## Implementation Details

The project’s source code (e.g., in `voting.py`) includes:
- Functions to load and parse voting data from an Excel spreadsheet (using openpyxl).  
- The `generatePreferences` function converts raw cell values into a structured preference profile.
- Multiple voting rule functions that operate on this profile and return the winning alternative based on different aggregation techniques.
- Tie-breaking methods that ensure a unique winner when multiple alternatives receive the same score.

The overall goal is to provide a showcase of how different voting methodologies can be implemented and compared within a consistent framework.

---
[LICENSE](https://github.com/clareokafor/Votings?tab=MIT-1-ov-file)
