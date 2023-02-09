1. Introduction
	- Short paragraph about RL and some use-cases
	- Explain briefly what the project is, and why it's created
	- Describe what happens in which chapter
2.  Game Implementation
	1. Game board
		- Board game implemented in Unity engine
		- Heavily focused on Skill, pretty hard for a human
		- Physics based
		- Wooden board, tilt on 2 axes to steer a marble
		- Follow the given path to manoeuvre through the maze till end is reached
		- Train agent to do exactly that
	2. Unity Game board
		- Game board modelled with Blender
		- Control tilt via keyboard, happens on two axes separately
		- Marble has Rigidbody3D, enables physics simulation
		- Walls and Game board have Collider3D
		- Holes in Ground have Trigger3D
		- On Top of board is also invisible collider, to prevent jumping
1. RL Implementation
	1.  Unity ML-Agents
		- Briefly explain what ML-Agents is and how it works
	2. Basics
		- Briefly explain how PPO it works and why we use it
		- Explain Curriculum Learning, how and why it can be better for complex environments
	3. Environment
		1. Action Space
		2. Observation Space
		3. Rewards
		4. Hyperparameters
	4. Training
		- Explain how training was set up, 10 runs for both methods with the best hyperparameters found, statistical best and worst
		1. Default RL
			- Talk about used hyperparameters, network size, etc.
		2. Curriculum Learning
			- Describe and show how the levels were set up
			- Talk about used hyperparameters, network size, etc.
2. Metrics and Results
	- Describe what metrics are used to analyse and compare performance
	- Show and evaluate graphs of those metrics
	- Interpret result
3. Conclusion and Outlook
	- Give outlook into future attempts
	- Critic this approach
	- What can be improved, where should be more time invested in