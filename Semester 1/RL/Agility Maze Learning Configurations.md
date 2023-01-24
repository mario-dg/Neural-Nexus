## FullMaze_001

The idea on this approach is, that the agent has to follow the rule-given path. By punishing the agent, the further he gets away from the next checkpoint, we enforce collecting every checkpoint before he can reach the goal. This results in a lot of punishment, if the agent is taking a wrong path, since he will collect many wrong checkpoints, thus getting many punishments.

### Environment
- 3 x 3 Grid of Mazes
- Max Step: 20000
- Max rotation degree: 15°
- Rotation Speed: 0.275
- Decision Period: 10
- Marble mass: 1

### Behaviour

- ppo

#### Hyper Parameters
- batch_size: 512
- buffer_size: 40960
- learning_rate: 0.0003
- beta: 0.001
- epsilon: 0.2
- lambd: 0.99
- num_epoch: 3
- learning_rate_schedule: constant

#### Network Settings
- normalize: false
- hidden_units: 512
- num_layers: 2
- vis_encode_type: simple

#### Reward Signals

##### extrinsic
- gamma: 0.99
- strength: 1.0


### Observations
- Outer Board Rotation (4 floats)
- Inner Board Rotation (4 floats)
- Normalized position of the Marble (3 floats)
- Normalized velocity magnitude of the Marble (1 float)
- Normalized distance between the Marble and the next Checkpoint (3 floats)
- Ray Perception 3D in all directions, to detect the Checkpoints
- Ray Perception 2D facing slightly down to detect the Holes

```c#
public override void CollectObservations(VectorSensor sensor)
{
	sensor.AddObservation(m_innerBoard.transform.localRotation);
    sensor.AddObservation(m_outerBoard.transform.localRotation);
    sensor.AddObservation(Helper.NormalizePosition(m_marble.transform.localPosition, 
						  m_maxX, 1f, m_maxZ));
    sensor.AddObservation(m_marble.GetComponent<Rigidbody>().velocity.magnitude / 
						  m_maxVelocity);
	sensor.AddObservation(m_distanceToNextCheckpoint);
}
```

### Rewards/Punishments
- -5, if falling into a hole ⇾ Episode End
- +10, if winning ⇾ Episode End
- +2, if collected correct checkpoint
- -0.5, if collected wrong checkpoint
- +0.05 * (1 - normalized distance), if moving towards the next checkpoint
- -0.05 * (1 - normalized distance), if moving away from the next checkpoint

#### Notes
- Agents is mostly stuck in the upper left corner
- Fails the first hard part of the maze and can't recover from missing a checkpoint
- The Marble is moving pretty fast ⇾ maybe try a slower rotation speed
- Stopped at: Step: 1870000. Time Elapsed: 3876.435 s. Mean Reward: 42.858. Std of Reward: 36.729. Training.


## FullMaze_002

The second approach scaled down the rotation speed to roughly half of FullMaze_001. Maybe this will result in slower marble velocities, thus better control for the agent.

### Environment
- 3 x 3 Grid of Mazes
- Max Step: 20000
- Max rotation degree: 15°
- Rotation Speed: 0.15
- Decision Period: 10
- Marble mass: 1

### Behaviour

- ppo

#### Hyper Parameters
- batch_size: 512
- buffer_size: 40960
- learning_rate: 0.0003
- beta: 0.001
- epsilon: 0.2
- lambd: 0.99
- num_epoch: 3
- learning_rate_schedule: constant

#### Network Settings
- normalize: false
- hidden_units: 512
- num_layers: 2
- vis_encode_type: simple

#### Reward Signals

##### extrinsic
- gamma: 0.99
- strength: 1.0


### Observations
- Outer Board Rotation (4 floats)
- Inner Board Rotation (4 floats)
- Normalized position of the Marble (3 floats)
- Normalized velocity magnitude of the Marble (1 float)
- Normalized distance between the Marble and the next Checkpoint (3 floats)
- Ray Perception 3D in all directions, to detect the Checkpoints
- Ray Perception 2D facing slightly down to detect the Holes

```c#
public override void CollectObservations(VectorSensor sensor)
{
	sensor.AddObservation(m_innerBoard.transform.localRotation);
    sensor.AddObservation(m_outerBoard.transform.localRotation);
    sensor.AddObservation(Helper.NormalizePosition(m_marble.transform.localPosition, 
						  m_maxX, 1f, m_maxZ));
    sensor.AddObservation(m_marble.GetComponent<Rigidbody>().velocity.magnitude / 
						  m_maxVelocity);
	sensor.AddObservation(m_distanceToNextCheckpoint);
}
```

### Rewards/Punishments
- -5, if falling into a hole ⇾ Episode End
- +10, if winning ⇾ Episode End
- +2, if collected correct checkpoint
- -0.5, if collected wrong checkpoint
- +0.05 * (1 - normalized distance), if moving towards the next checkpoint
- -0.05 * (1 - normalized distance), if moving away from the next checkpoint

#### Notes
- Cancelled, because I wanted to check if the Checkpoint code was working correctly, so I updated the Material of the current checkpoint to be different, as well as drawing a line Gizmo to the next Checkpoint. 

## FullMaze_003

The third approach is not really different from the second one, instead of increasing the amount of parallel agents in one dimension by 1.

### Environment
- 4 x 3 Grid of Mazes
- Max Step: 20000
- Max rotation degree: 15°
- Rotation Speed: 0.15
- Decision Period: 10
- Marble mass: 1

### Behaviour

- ppo

#### Hyper Parameters
- batch_size: 512
- buffer_size: 40960
- learning_rate: 0.0003
- beta: 0.001
- epsilon: 0.2
- lambd: 0.99
- num_epoch: 3
- learning_rate_schedule: constant

#### Network Settings
- normalize: false
- hidden_units: 512
- num_layers: 2
- vis_encode_type: simple

#### Reward Signals

##### extrinsic
- gamma: 0.99
- strength: 1.0


### Observations
- Outer Board Rotation (4 floats)
- Inner Board Rotation (4 floats)
- Normalized position of the Marble (3 floats)
- Normalized velocity magnitude of the Marble (1 float)
- Normalized distance between the Marble and the next Checkpoint (3 floats)
- Ray Perception 3D in all directions, to detect the Checkpoints
- Ray Perception 2D facing slightly down to detect the Holes

```c#
public override void CollectObservations(VectorSensor sensor)
{
	sensor.AddObservation(m_innerBoard.transform.localRotation);
    sensor.AddObservation(m_outerBoard.transform.localRotation);
    sensor.AddObservation(Helper.NormalizePosition(m_marble.transform.localPosition, 
						  m_maxX, 1f, m_maxZ));
    sensor.AddObservation(m_marble.GetComponent<Rigidbody>().velocity.magnitude / 
						  m_maxVelocity);
	sensor.AddObservation(m_distanceToNextCheckpoint);
}
```

### Rewards/Punishments
- -5, if falling into a hole ⇾ Episode End
- +10, if winning ⇾ Episode End
- +2, if collected correct checkpoint
- -0.5, if collected wrong checkpoint
- +0.05 * (1 - normalized distance), if moving towards the next checkpoint
- -0.05 * (1 - normalized distance), if moving away from the next checkpoint

#### Notes
- Keeps getting stuck in the top left corner. 
- Is only moving from left to right.

## FullMaze_004

The fourth approach further reduced the rotation speed.

### Environment
- 4 x 3 Grid of Mazes
- Max Step: 20000
- Max rotation degree: 15°
- Rotation Speed: 0.075
- Decision Period: 10
- Marble mass: 1

### Behaviour

- ppo

#### Hyper Parameters
- batch_size: 512
- buffer_size: 40960
- learning_rate: 0.0003
- beta: 0.001
- epsilon: 0.2
- lambd: 0.99
- num_epoch: 3
- learning_rate_schedule: constant

#### Network Settings
- normalize: false
- hidden_units: 512
- num_layers: 2
- vis_encode_type: simple

#### Reward Signals

##### extrinsic
- gamma: 0.99
- strength: 1.0


### Observations
- Outer Board Rotation (4 floats)
- Inner Board Rotation (4 floats)
- Normalized position of the Marble (3 floats)
- Normalized velocity magnitude of the Marble (1 float)
- Normalized distance between the Marble and the next Checkpoint (3 floats)
- Ray Perception 3D in all directions, to detect the Checkpoints
- Ray Perception 2D facing slightly down to detect the Holes

```c#
public override void CollectObservations(VectorSensor sensor)
{
	sensor.AddObservation(m_innerBoard.transform.localRotation);
    sensor.AddObservation(m_outerBoard.transform.localRotation);
    sensor.AddObservation(Helper.NormalizePosition(m_marble.transform.localPosition, 
						  m_maxX, 1f, m_maxZ));
    sensor.AddObservation(m_marble.GetComponent<Rigidbody>().velocity.magnitude / 
						  m_maxVelocity);
	sensor.AddObservation(m_distanceToNextCheckpoint);
}
```

### Rewards/Punishments
- -5, if falling into a hole ⇾ Episode End
- +10, if winning ⇾ Episode End
- +2, if collected correct checkpoint
- -0.5, if collected wrong checkpoint
- +0.05 * (1 - normalized distance), if moving towards the next checkpoint
- -0.05 * (1 - normalized distance), if moving away from the next checkpoint

#### Notes
- Still stuck in top left corner
- Dies in 90% of the cases in the top left Hole
## FullMaze_005

For this approach, the agent is no longer punished for collecting the wrong Checkpoint. This hopefully leads to more exploration. But it will probably need the removal of the reward/punishing system depending on the distance to the next Checkpoint

### Environment
- 4 x 3 Grid of Mazes
- Max Step: 20000
- Max rotation degree: 15°
- Rotation Speed: 0.075
- Decision Period: 10
- Marble mass: 1

### Behaviour

- ppo

#### Hyper Parameters
- batch_size: 512
- buffer_size: 40960
- learning_rate: 0.0003
- beta: 0.001
- epsilon: 0.2
- lambd: 0.99
- num_epoch: 3
- learning_rate_schedule: constant

#### Network Settings
- normalize: false
- hidden_units: 512
- num_layers: 2
- vis_encode_type: simple

#### Reward Signals

##### extrinsic
- gamma: 0.99
- strength: 1.0


### Observations
- Outer Board Rotation (4 floats)
- Inner Board Rotation (4 floats)
- Normalized position of the Marble (3 floats)
- Normalized velocity magnitude of the Marble (1 float)
- Normalized distance between the Marble and the next Checkpoint (3 floats)
- Ray Perception 3D in all directions, to detect the Checkpoints
- Ray Perception 2D facing slightly down to detect the Holes

```c#
public override void CollectObservations(VectorSensor sensor)
{
	sensor.AddObservation(m_innerBoard.transform.localRotation);
    sensor.AddObservation(m_outerBoard.transform.localRotation);
    sensor.AddObservation(Helper.NormalizePosition(m_marble.transform.localPosition, 
						  m_maxX, 1f, m_maxZ));
    sensor.AddObservation(m_marble.GetComponent<Rigidbody>().velocity.magnitude / 
						  m_maxVelocity);
	sensor.AddObservation(m_distanceToNextCheckpoint);
}
```

### Rewards/Punishments
- -5, if falling into a hole ⇾ Episode End
- +10, if winning ⇾ Episode End
- +2, if collected correct checkpoint
- +0.05 * (1 - normalized distance), if moving towards the next checkpoint
- -0.05 * (1 - normalized distance), if moving away from the next checkpoint

#### Notes
- Manages the first part of the top left corner really well, but struggles with the fourth Checkpoint
- Realized, that the marble is rotating around itself. This results in incorrect Ray Perceptions
## FullMaze_006

In the sixth approach, I froze the rotation of the marble, so that the Perception Sensors 3D will yield correct results.

### Environment
- 4 x 3 Grid of Mazes
- Max Step: 20000
- Max rotation degree: 15°
- Rotation Speed: 0.075
- Decision Period: 10
- Marble mass: 1

### Behaviour

- ppo

#### Hyper Parameters
- batch_size: 512
- buffer_size: 40960
- learning_rate: 0.0003
- beta: 0.001
- epsilon: 0.2
- lambd: 0.99
- num_epoch: 3
- learning_rate_schedule: constant

#### Network Settings
- normalize: false
- hidden_units: 512
- num_layers: 2
- vis_encode_type: simple

#### Reward Signals

##### extrinsic
- gamma: 0.99
- strength: 1.0


### Observations
- Outer Board Rotation (4 floats)
- Inner Board Rotation (4 floats)
- Normalized position of the Marble (3 floats)
- Normalized velocity magnitude of the Marble (1 float)
- Normalized distance between the Marble and the next Checkpoint (3 floats)
- Ray Perception 3D in all directions, to detect the Checkpoints
- Ray Perception 2D facing slightly down to detect the Holes

```c#
public override void CollectObservations(VectorSensor sensor)
{
	sensor.AddObservation(m_innerBoard.transform.localRotation);
    sensor.AddObservation(m_outerBoard.transform.localRotation);
    sensor.AddObservation(Helper.NormalizePosition(m_marble.transform.localPosition, 
						  m_maxX, 1f, m_maxZ));
    sensor.AddObservation(m_marble.GetComponent<Rigidbody>().velocity.magnitude / 
						  m_maxVelocity);
	sensor.AddObservation(m_distanceToNextCheckpoint);
}
```

### Rewards/Punishments
- -5, if falling into a hole ⇾ Episode End
- +10, if winning ⇾ Episode End
- +2, if collected correct checkpoint
- +0.05 * (1 - normalized distance), if moving towards the next checkpoint
- -0.05 * (1 - normalized distance), if moving away from the next checkpoint

#### Notes
- Agent is able to go a lot further
- Probably will need to add the Walls as detectable Objects to the Perception Sensors 3D
- Max step count seems to be too low
## FullMaze_007

In the seventh approach, the max step count got removed, and the Walls were added to the detectable Objects of the first Perception Sensor 3D. These changes will result in longer Episodes and hopefully better awareness of the Marbles surroundings

### Environment
- 4 x 3 Grid of Mazes
- Max Step: 0
- Max rotation degree: 15°
- Rotation Speed: 0.075
- Decision Period: 10
- Marble mass: 1

### Behaviour

- ppo

#### Hyper Parameters
- batch_size: 512
- buffer_size: 40960
- learning_rate: 0.0003
- beta: 0.001
- epsilon: 0.2
- lambd: 0.99
- num_epoch: 3
- learning_rate_schedule: constant

#### Network Settings
- normalize: false
- hidden_units: 512
- num_layers: 2
- vis_encode_type: simple

#### Reward Signals

##### extrinsic
- gamma: 0.99
- strength: 1.0


### Observations
- Outer Board Rotation (4 floats)
- Inner Board Rotation (4 floats)
- Normalized position of the Marble (3 floats)
- Normalized velocity magnitude of the Marble (1 float)
- Normalized distance between the Marble and the next Checkpoint (3 floats)
- Ray Perception 3D in all directions, to detect the Checkpoints
- Ray Perception 2D facing slightly down to detect the Holes

```c#
public override void CollectObservations(VectorSensor sensor)
{
	sensor.AddObservation(m_innerBoard.transform.localRotation);
    sensor.AddObservation(m_outerBoard.transform.localRotation);
    sensor.AddObservation(Helper.NormalizePosition(m_marble.transform.localPosition, 
						  m_maxX, 1f, m_maxZ));
    sensor.AddObservation(m_marble.GetComponent<Rigidbody>().velocity.magnitude / 
						  m_maxVelocity);
	sensor.AddObservation(m_distanceToNextCheckpoint);
}
```

### Rewards/Punishments
- -5, if falling into a hole ⇾ Episode End
- +10, if winning ⇾ Episode End
- +2, if collected correct checkpoint
- +0.05 * (1 - normalized distance), if moving towards the next checkpoint
- -0.05 * (1 - normalized distance), if moving away from the next checkpoint

#### Notes
- Agent got stuck in top left corner again
- He collected the reward for gettings closer to next Checkpoint
- Maybe make the punishment for moving away from the next Checkpoint bigger, than getting closer
## FullMaze_008

The eighth approach added back the punishment for collection the wrong checkpoint

### Environment
- 4 x 3 Grid of Mazes
- Max Step: 0
- Max rotation degree: 15°
- Rotation Speed: 0.075
- Decision Period: 10
- Marble mass: 1

### Behaviour

- ppo

#### Hyper Parameters
- batch_size: 512
- buffer_size: 40960
- learning_rate: 0.0003
- beta: 0.001
- epsilon: 0.2
- lambd: 0.99
- num_epoch: 3
- learning_rate_schedule: constant

#### Network Settings
- normalize: false
- hidden_units: 512
- num_layers: 2
- vis_encode_type: simple

#### Reward Signals

##### extrinsic
- gamma: 0.99
- strength: 1.0


### Observations
- Outer Board Rotation (4 floats)
- Inner Board Rotation (4 floats)
- Normalized position of the Marble (3 floats)
- Normalized velocity magnitude of the Marble (1 float)
- Normalized distance between the Marble and the next Checkpoint (3 floats)
- Ray Perception 3D in all directions, to detect the Checkpoints
- Ray Perception 2D facing slightly down to detect the Holes

```c#
public override void CollectObservations(VectorSensor sensor)
{
	sensor.AddObservation(m_innerBoard.transform.localRotation);
    sensor.AddObservation(m_outerBoard.transform.localRotation);
    sensor.AddObservation(Helper.NormalizePosition(m_marble.transform.localPosition, 
						  m_maxX, 1f, m_maxZ));
    sensor.AddObservation(m_marble.GetComponent<Rigidbody>().velocity.magnitude / 
						  m_maxVelocity);
	sensor.AddObservation(m_distanceToNextCheckpoint);
}
```

### Rewards/Punishments
- -5, if falling into a hole ⇾ Episode End
- +10, if winning ⇾ Episode End
- +2, if collected correct checkpoint
- -0.5, if collected wrong checkpoint
- +0.05 * (1 - normalized distance), if moving towards the next checkpoint
- -0.05 * (1 - normalized distance), if moving away from the next checkpoint

#### Notes
- Also kept getting stuck in the top left
## FullMaze_009

The ninth approach increased the punishment for moving away from the next Checkpoint

### Environment
- 4 x 3 Grid of Mazes
- Max Step: 0
- Max rotation degree: 15°
- Rotation Speed: 0.075
- Decision Period: 10
- Marble mass: 1

### Behaviour

- ppo

#### Hyper Parameters
- batch_size: 512
- buffer_size: 40960
- learning_rate: 0.0003
- beta: 0.001
- epsilon: 0.2
- lambd: 0.99
- num_epoch: 3
- learning_rate_schedule: constant

#### Network Settings
- normalize: false
- hidden_units: 512
- num_layers: 2
- vis_encode_type: simple

#### Reward Signals

##### extrinsic
- gamma: 0.99
- strength: 1.0


### Observations
- Outer Board Rotation (4 floats)
- Inner Board Rotation (4 floats)
- Normalized position of the Marble (3 floats)
- Normalized velocity magnitude of the Marble (1 float)
- Normalized distance between the Marble and the next Checkpoint (3 floats)
- Ray Perception 3D in all directions, to detect the Checkpoints
- Ray Perception 2D facing slightly down to detect the Holes

```c#
public override void CollectObservations(VectorSensor sensor)
{
	sensor.AddObservation(m_innerBoard.transform.localRotation);
    sensor.AddObservation(m_outerBoard.transform.localRotation);
    sensor.AddObservation(Helper.NormalizePosition(m_marble.transform.localPosition, 
						  m_maxX, 1f, m_maxZ));
    sensor.AddObservation(m_marble.GetComponent<Rigidbody>().velocity.magnitude / 
						  m_maxVelocity);
	sensor.AddObservation(m_distanceToNextCheckpoint);
}
```

### Rewards/Punishments
- -5, if falling into a hole ⇾ Episode End
- +10, if winning ⇾ Episode End
- +2, if collected correct checkpoint
- -0.5, if collected wrong checkpoint
- +0.05 * (1 - normalized distance), if moving towards the next checkpoint
- -0.1 * (1 - normalized distance), if moving away from the next checkpoint

#### Notes
- Maybe try the settings from [[Agility Maze Learning Configurations#FullMaze_006]], but remove the Walls from the detectable Objects
- Also try above with small punishment for every step
## FullMaze_010

In the tenth approach, the environment is the same as in [[Agility Maze Learning Configurations#FullMaze_006]], but the max step count is set to 75000

### Environment
- 4 x 3 Grid of Mazes
- Max Step: 75000
- Max rotation degree: 15°
- Rotation Speed: 0.075
- Decision Period: 10
- Marble mass: 1

### Behaviour

- ppo

#### Hyper Parameters
- batch_size: 512
- buffer_size: 40960
- learning_rate: 0.0003
- beta: 0.001
- epsilon: 0.2
- lambd: 0.99
- num_epoch: 3
- learning_rate_schedule: constant

#### Network Settings
- normalize: false
- hidden_units: 512
- num_layers: 2
- vis_encode_type: simple

#### Reward Signals

##### extrinsic
- gamma: 0.99
- strength: 1.0


### Observations
- Outer Board Rotation (4 floats)
- Inner Board Rotation (4 floats)
- Normalized position of the Marble (3 floats)
- Normalized velocity magnitude of the Marble (1 float)
- Normalized distance between the Marble and the next Checkpoint (3 floats)
- Ray Perception 3D in all directions, to detect the Checkpoints
- Ray Perception 3D facing slightly down to detect the Holes

```c#
public override void CollectObservations(VectorSensor sensor)
{
	sensor.AddObservation(m_innerBoard.transform.localRotation);
    sensor.AddObservation(m_outerBoard.transform.localRotation);
    sensor.AddObservation(Helper.NormalizePosition(m_marble.transform.localPosition, 
						  m_maxX, 1f, m_maxZ));
    sensor.AddObservation(m_marble.GetComponent<Rigidbody>().velocity.magnitude / 
						  m_maxVelocity);
	sensor.AddObservation(m_distanceToNextCheckpoint);
}
```

### Rewards/Punishments
- -5, if falling into a hole ⇾ Episode End
- +10, if winning ⇾ Episode End
- +2, if collected correct checkpoint
- +0.05 * (1 - normalized distance), if moving towards the next checkpoint
- -0.05 * (1 - normalized distance), if moving away from the next checkpoint

#### Notes
## FullMaze_011

In the 11th approach, the Marble mass is increased and the agent will be punished for collecting the wron Checkpoint

### Environment
- 4 x 3 Grid of Mazes
- Max Step: 75000
- Max rotation degree: 15°
- Rotation Speed: 0.075
- Decision Period: 10
- Marble mass: 2.5

### Behaviour

- ppo

#### Hyper Parameters
- batch_size: 512
- buffer_size: 40960
- learning_rate: 0.0003
- beta: 0.001
- epsilon: 0.2
- lambd: 0.99
- num_epoch: 3
- learning_rate_schedule: constant

#### Network Settings
- normalize: false
- hidden_units: 512
- num_layers: 2
- vis_encode_type: simple

#### Reward Signals

##### extrinsic
- gamma: 0.99
- strength: 1.0


### Observations
- Outer Board Rotation (4 floats)
- Inner Board Rotation (4 floats)
- Normalized position of the Marble (3 floats)
- Normalized velocity magnitude of the Marble (1 float)
- Normalized distance between the Marble and the next Checkpoint (3 floats)
- Ray Perception 3D in all directions, to detect the Checkpoints
- Ray Perception 3D facing slightly down to detect the Holes

```c#
public override void CollectObservations(VectorSensor sensor)
{
	sensor.AddObservation(m_innerBoard.transform.localRotation);
    sensor.AddObservation(m_outerBoard.transform.localRotation);
    sensor.AddObservation(Helper.NormalizePosition(m_marble.transform.localPosition, 
						  m_maxX, 1f, m_maxZ));
    sensor.AddObservation(m_marble.GetComponent<Rigidbody>().velocity.magnitude / 
						  m_maxVelocity);
	sensor.AddObservation(m_distanceToNextCheckpoint);
}
```

### Rewards/Punishments
- -5, if falling into a hole ⇾ Episode End
- +10, if winning ⇾ Episode End
- +2, if collected correct checkpoint
- -0.5, if collected wrong checkpoint
- +0.05 * (1 - normalized distance), if moving towards the next checkpoint
- -0.05 * (1 - normalized distance), if moving away from the next checkpoint

#### Notes
- Try SetReward for falling into a Hole. This will hopefully lead to a more careful Agent

TODO: Make Entry for FullMaze_012
## FullMaze_012

Since the last six approaches failed to make any more progress, I decided to turn down a notch and made everything simpler. The reward system is structured more simple and the neural network size is increased.

### Environment
- 4 x 3 Grid of Mazes
- Max Step: 0
- Max rotation degree: 10°
- Rotation Speed: 0.1
- Decision Period: 10
- Marble mass: 1.5

### Behaviour

- ppo

#### Hyper Parameters
- batch_size: 512
- buffer_size: 40960
- learning_rate: 0.0003
- beta: 0.001
- epsilon: 0.2
- lambd: 0.99
- num_epoch: 3
- learning_rate_schedule: constant

#### Network Settings
- normalize: false
- hidden_units: 512
- num_layers: 2
- vis_encode_type: simple

#### Reward Signals

##### extrinsic
- gamma: 0.99
- strength: 1.0


### Observations
- Outer Board Rotation (4 floats)
- Inner Board Rotation (4 floats)
- Normalized position of the Marble (3 floats)
- Normalized velocity magnitude of the Marble (1 float)
- Normalized distance between the Marble and the next Checkpoint (3 floats)
- Ray Perception 3D in all directions, to detect the Checkpoints
- Ray Perception 3D facing slightly down to detect the Holes

```c#
public override void CollectObservations(VectorSensor sensor)
{
	sensor.AddObservation(m_innerBoard.transform.localRotation);
    sensor.AddObservation(m_outerBoard.transform.localRotation);
    sensor.AddObservation(Helper.NormalizePosition(m_marble.transform.localPosition, 
						  m_maxX, 1f, m_maxZ));
    sensor.AddObservation(m_marble.GetComponent<Rigidbody>().velocity.magnitude / 
						  m_maxVelocity);
	sensor.AddObservation(m_distanceToNextCheckpoint);
}
```

### Rewards/Punishments
- -5, if falling into a hole ⇾ Episode End
- +10000, if winning ⇾ Episode End
- +2.5 * Checkpoint Index, if collected correct checkpoint
- +0.02 * (1 - normalized distance), if moving towards the next checkpoint
- -0.02 * normalized distance, if moving away from the next checkpoint
- -10, if Marble velocity < 0.001 for 3000 steps in a row

#### Notes
```
behaviors:
  FullMaze_Checkpoints:
    trainer_type: ppo
    hyperparameters:
      batch_size: 512
      buffer_size: 40960
      learning_rate: 0.0003
      beta: 0.001
      epsilon: 0.2
      lambd: 0.99
      num_epoch: 3
      learning_rate_schedule: constant
    network_settings:
      normalize: false
      hidden_units: 1024
      num_layers: 3
      vis_encode_type: simple
    reward_signals:
      extrinsic:
        gamma: 0.99
        strength: 1.0  
    keep_checkpoints: 5
    max_steps: 50000000
    time_horizon: 1000
    summary_freq: 10000


behaviors:
  FullMaze_Checkpoints:
    trainer_type: ppo
    hyperparameters:
      batch_size: 2048
      buffer_size: 163840
      learning_rate: 0.0003
      beta: 0.001
      epsilon: 0.2
      lambd: 0.99
      num_epoch: 3
      learning_rate_schedule: constant
    network_settings:
      normalize: false
      hidden_units: 1024
      num_layers: 4
      vis_encode_type: simple
    reward_signals:
      extrinsic:
        gamma: 0.99
        strength: 1.0  
    keep_checkpoints: 5
    max_steps: 75000000
    time_horizon: 1000
    summary_freq: 10000
   
behaviors:
  FullMaze_Checkpoints:
    trainer_type: ppo
    hyperparameters:
      batch_size: 2048
      buffer_size: 163840
      learning_rate: 0.0003
      beta: 0.001
      epsilon: 0.2
      lambd: 0.99
      num_epoch: 3
      learning_rate_schedule: constant
    network_settings:
      normalize: false
      hidden_units: 2048
      num_layers: 3
      vis_encode_type: simple
    reward_signals:
      extrinsic:
        gamma: 0.99
        strength: 1.0  
    keep_checkpoints: 5
    max_steps: 75000000
    time_horizon: 1000
    summary_freq: 10000
   
behaviors:
  FullMaze_Checkpoints:
    trainer_type: ppo
    hyperparameters:
      batch_size: 2048
      buffer_size: 163840
      learning_rate: 0.0003
      beta: 0.001
      epsilon: 0.25
      lambd: 0.95
      num_epoch: 3
      learning_rate_schedule: constant
    network_settings:
      normalize: false
      hidden_units: 2048
      num_layers: 4
      vis_encode_type: simple
    reward_signals:
      extrinsic:
        gamma: 0.99
        strength: 1.0  
    keep_checkpoints: 5
    max_steps: 75000000
    time_horizon: 1000
    summary_freq: 10000
```