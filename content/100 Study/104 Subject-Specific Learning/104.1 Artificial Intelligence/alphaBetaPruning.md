---
title: Alpha-beta Pruning
---
Search algorithm that decreases the number of gate states to evaluate in [[braitenbergVehicle|Braitenberg Vehicle]] in the game tree.
- Stopping condition: It does not evaluate further when it realizes that there is already an existing better alternative.
Note: It's the same final output as the [[minimaxAlgorithm|Minimax Algorithm]], just a more efficient way of going about it.
##### High-level Overview
Like minimax,
- Each node in the game tree represents a possible situation in the game
- Each endgame situation is assigned a value

As we go through the game tree, we keep track of two values,
- Alpha: Minimum value the max player can get, initially set to -∞
- Beta: Maximum value the min player can get, initially set to +∞