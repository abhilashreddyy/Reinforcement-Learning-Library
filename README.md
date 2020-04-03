# Reinforcement-Learning-Library

## Twin Delayed Deep Deterministic Poly Gradient network (T3D)

### This github repo explains T#D algorithm

Let us start withthe code 

### Step 1: 
- Initialise the replay buffer wiht "n" random records
![image](/images/replay_buffer.jpg)

### Step 2:
- Initialise Actor model and Actor target \
\
![image](/images/step2.jpg)

- Each actor model structure is as following image
![image](/images/actor.jpg)

### Step 3:
- Initialise Critic models and critic targets
- In our case we took 2 - Critic Models and 2 corresponding Critic Targets\
\
![image](/images/step3.jpg)
- Each Critic model Structure is as following image
![image](/images/critic.jpg)

### Step 4:
- Import a batch of transition records from replay buffer as showin in step1
- Each record consists of (current state, next state, current action , next record, batch done)

### Step 5:
- Predict Target for next action trough Actor Target
![image](/images/step5.jpg)

### Step 6:
- Add gaussian noise to the next action prediction
- This will help the Actor to explore new paths or stratigies to perform better

### Step 7:
- Predict Q values to the next state and next action from the critic Target
  \
![image](/images/Step7.jpg)

### Step 8:
- Calculate minimum Q value from all the critic targets
- This prevents too optmistic estimates of the value of next states
  \
![image](/images/step8.jpg)

### Step 9:
- calculate the final target Q value including the reward
- Q = Reward + gamma * minimum(all target Q values)
- If we observe the above step carefully it is Bellmen ford equation we are using to rain the agent
- Observe the following diagram and formula and compare it with what is happening in current step
  \
![image](/images/recapf.PNG)
![image](/images/recapi.PNG)

### Step 10:
- Calculate Critic model current Q-values from current state and action \
  \
![image](/images/Step10.jpg)

### Step 11:
- Now as we have already calculated current steps expected Max Q-value from step 9 we can calculate Loss for the Critic model just by calculating difference between Q calculated in step 9(Target Q-value) and step 10(Current Q-value) as shown in figure.
- here MSE() refers to mean square error
  \
![image](/images/Step11.jpg)

### Step 12:
- Back propagate all the Ctitic models from the loss calculated in step 11\
  \
![image](/images/Step11.jpg)

### Step 13:
- repeat step 4-12 for policy_freq iterations
- After every policy_freq iterations  back propagateActor model using the loss calculated from critic model as shown below
  \
![image](/images/Step13_1.jpg)
  \
  \
  -------------------------------------------------------------------------------------------------------------------------
  \
  \
![image](/images/Step13_2.jpg)

