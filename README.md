# Simulating the Emergence of Innovation

> “Innovation distinguishes between a leader and a follower. ” — Steve Jobs
![Preview Image](https://images.squarespace-cdn.com/content/v1/5a29de216957dab4049b897d/1579390829957-M1VORLXNKM21MD7BJZST/ke17ZwdGBToddI8pDm48kMG2yjkrZkbHb--rkMsT21YUqsxRUqqbr1mOJYKfIPR7LoDQ9mXPOjoJoqy81S2I8N_N4V1vUb5AoIIIbLZhVYwL8IeDg6_3B-BRuF4nNrNcQkVuAT7tdErd0wQFEGFSnIxXzMyEP4oFWls1viF_rYmRAYbvdTbRvEsZ5WjAjeiG3CO7jxEzb7REKBWZmQDDHQ/Simulating%252BInnovation.jpg?format=2500w)

### Introduction
For 200,000 years, human has survived and thrived. Such development is inseparable from our ability to innovate. For this reason, we continuously explore ways to foster innovation in society. Innovation has no exact definition. McKinsey defines innovation as “creativity plus delivery” (McKinsey & Company, 2019). On the other hand, the Cambridge Dictionary defines innovation as “the use of a new idea or method” (The Cambridge English Dictionary, 2019). A popular explanation is that innovation differs from an invention because it causes a change in behaviors or interactions (Walker, 2015). These definitions and explanations have one thing in common; they all suggest that innovation has two aspects, idea and impact. In this project, innovation is defined as an idea that leads to a significant impact. 

Innovation is a difficult topic to study because it has a massive scope and lacks precise data. This project uses pure computational modeling to study innovation from another perspective. In specific, a Monte Carlo simulation is used together with cellular automata to simulate how innovation emerges in systems. It is found that decreasing the probability of idea generation and increasing the probability of social interaction can help to foster innovation. 


### Model
This model uses a two-dimensional cellular automata with von Neumann neighborhood and periodic boundaries to simulate the emergence of innovation. The method is used due to its spacial simplicity and visual clarity. The simulation can also be classified as a Monto Carlo simulation because it involves multiple layers of randomization that explores the distribution of possible outcomes. 

The goal of the model is to explore how to foster innovation in a system. In specific, the model should be able to measure the number of innovations created from a system after a defined time step. The parameters of the model are: n (the scale of the space),  ps(probability of sharing/gaining idea), and p_i (probability of creating a new idea).  

In the beginning, all the agents are at the zero states (meaning they have no ideas). At each time step, all the agents will be updated. ps percent of the agents will share ideas to one of their neighbor. The rest 1-ps percent of the agents will work on an idea on their own. They have pi probability of coming up with a new idea, and 1-p_1 probability of updating an old idea.  
![Update rule visualization](https://images.squarespace-cdn.com/content/v1/5a29de216957dab4049b897d/1577122405847-HGW9DE0HNUAUA2G2RUW4/ke17ZwdGBToddI8pDm48kF674s35-Md0Oo9VG-CHPyAUqsxRUqqbr1mOJYKfIPR7LoDQ9mXPOjoJoqy81S2I8N_N4V1vUb5AoIIIbLZhVYy7Mythp_T-mtop-vrsUOmeInPi9iDjx9w8K4ZfjXt2ds1582C_vmUdNXOlLonRbvWTG_o2OUV1ovDO6eOsToF1CjLISwBs8eEdxAxTptZAUg/Screen+Shot+2019-12-23+at+6.33.17+PM.png?format=1500w)

An agent can have multiple ideas, but only one idea is active at each time step. For the active idea, the idea’s stage will be upgraded by one. For the non-active ideas, the idea stage will decay by half (Figure 2). The agent chooses an idea to share or upgrade based on the probability distribution of the idea stages. In other words, an idea at a high stage is more likely to be chosen than an idea at a low stage. For example, with the idea stage data {1:5, 2:1, 3:4}, 1’s probability of being chosen to update is the greatest, and it is 5/(5+1+4) = 50%. At each time step, an idea that is active for ≥1/3 of the agents is classified as an innovation. If the idea is a new innovation, meaning that there is no past circumstance where it covers ≥1/3 of the agent, then the idea is classified as a unique innovation. The interest is to measure how many unique innovation emerges through the system after a large time step. 
![Visualization of possible idea stage](https://images.squarespace-cdn.com/content/v1/5a29de216957dab4049b897d/1577122543043-Y39ZSDRHZRDXUPWXB4UM/ke17ZwdGBToddI8pDm48kDCnuYvD6-OsXbW_B7ffObcUqsxRUqqbr1mOJYKfIPR7LoDQ9mXPOjoJoqy81S2I8N_N4V1vUb5AoIIIbLZhVYy7Mythp_T-mtop-vrsUOmeInPi9iDjx9w8K4ZfjXt2drHxVL8hOFvJn88BjfmUJoZLLM5TtnVQmvdnoyJmn8YUCjLISwBs8eEdxAxTptZAUg/Screen+Shot+2019-12-23+at+6.35.24+PM.png?format=2500w)

There are several key assumptions of this model. They are listed and justified below: 

1. *A two-dimensional cellular automata with von Neumann neighborhood and periodic boundaries can to some extent represents human network.* Although cellular automata scale downs the complexity of the real-world network, it consists of spacial property that allows ideas to flow through the system. This is a good starting point for simulating innovation. 

2. *At each time step, an individual can only focuses on one activity.* At each time step, an agent either share an idea, come up with a new idea, or update an old idea. This is based on the finding that human can hardly multitask (Adams, 2019). 

3. *At each time step, an individual can maximumly interact with one individual.* This assumption is used to simplify the complex scenario. With the assumption, p_s can be adequately applied. Indeed, group sharing is possible in real life. Further study can incorporate the ability of group sharing. 

4. *Ideas will be upgrade in linear manner.* This assumption is used to simplify the complex scenario. There can be many leapfrog in idea development. Further study can incorporate another level of randomness on the step of idea sharing. 

5. *Ideas will be decay in exponential manner.* The decay function references the well-known forgotten curve (Shrestha, 2019). 

6. *A innovation can be classified as an idea that pass certain level of impact.* This point is justified in the introduction and clearly stated in the definition. 

### Mathematical Analysis 
This section proposes two strategies to foster innovation based on mathematical analysis. The two strategies are decreasing pi and increasing p_s.  

At each time step, the probability of sharing an idea with others or being shared an idea is ps. Because this model assumings one on one interaction, the probability of being introduced an idea or introducing an idea to others is p_s/2. 

At each time step, the probability that an agent does not interact with others is 1-p_s. In this case, the agent may come up with a new idea with probability p_i, so overall the probability is . On the other hand, an agent will choose an old idea to update with the probability 1-p_i, so overall the probability is (1-p_s)(1-p_i). 

![Update rule visualization](https://images.squarespace-cdn.com/content/v1/5a29de216957dab4049b897d/1577123021258-U44G2AJALCY7LYRM9N3S/ke17ZwdGBToddI8pDm48kF674s35-Md0Oo9VG-CHPyAUqsxRUqqbr1mOJYKfIPR7LoDQ9mXPOjoJoqy81S2I8N_N4V1vUb5AoIIIbLZhVYy7Mythp_T-mtop-vrsUOmeInPi9iDjx9w8K4ZfjXt2ds1582C_vmUdNXOlLonRbvWTG_o2OUV1ovDO6eOsToF1CjLISwBs8eEdxAxTptZAUg/Screen+Shot+2019-12-23+at+6.33.17+PM.png?format=2500w)

At a time step when an innovation i is formed, the innovation cannot come from a new idea (case 3), because the new idea only covers one cell that generated it. This suggests that Case(3) should happen <2/3 of the time, because ≥1/3 is the threshold for innovation. Therefore, (1-p_s)pi<2/3 should be satisfied on average. The two strategies of satisfying this constraint is to increase p_s or reduce p_i. 

In case(1) and case(4), the possibility that idea i is chosen to be updated or shared is dependent on the memory of the idea at each cell. The greater the stage memory of idea i, the more likely that idea i will be chosen. Case(2), on the other hand, is dependent on case(1). For case(1) to happen more frequently, the strategy is to increase p_s. For case(4) to happen more frequently, the stratgey is to decrease p_i.  

Based on the above analysis, I predict that as long as p_i>0 so that there will be ideas in the system, innovation happens more frequent when p_i is low or when p_s is high. 

### Simulation Result
The following example simulation is performed on a 10 by 10 grid with parameters p_s=1, p_i=1. With the combination of parameters, each cell will come up with a unique idea in the first time step. At all the following steps, all cells will share ideas with neighbors. As shown in Figure 2, clusters are gradually formed.  

![Step 1, 2, 3 of an example simulation visualization](https://images.squarespace-cdn.com/content/v1/5a29de216957dab4049b897d/1577123191391-XWQKZ2RQX9EVVTR8I2FY/ke17ZwdGBToddI8pDm48kO4KIQuIbq8QPh5IzOwOj6QUqsxRUqqbr1mOJYKfIPR7LoDQ9mXPOjoJoqy81S2I8N_N4V1vUb5AoIIIbLZhVYy7Mythp_T-mtop-vrsUOmeInPi9iDjx9w8K4ZfjXt2dpk06B7xt7Vs8bS0FHgvPbVSE7K1GY99uiv2a-EjtTnaCjLISwBs8eEdxAxTptZAUg/Screen+Shot+2019-12-23+at+6.46.24+PM.png?format=2500w)

When running a set of parameters for multiple times, the program may generate different results for the number of innovation due to the random nature of the model. The following graph visualizes the result of running 1,000 times on a 5 by 5 grid with parameters p_s=0.5 and p_i=0.5 for 100 time steps. 

![Histogram of repetitively running the same set of parameters for 1,000 iterations.](https://images.squarespace-cdn.com/content/v1/5a29de216957dab4049b897d/1577123260170-CSNV9DJXTQ4CASMMW0GW/ke17ZwdGBToddI8pDm48kDdqaj6AJ5b6JyVYNNqvXh0UqsxRUqqbr1mOJYKfIPR7LoDQ9mXPOjoJoqy81S2I8N_N4V1vUb5AoIIIbLZhVYy7Mythp_T-mtop-vrsUOmeInPi9iDjx9w8K4ZfjXt2dhRDlneo-5l5mmiDnUAYyKawOsyDUE-Ip0qgtfybuNnECjLISwBs8eEdxAxTptZAUg/Screen+Shot+2019-12-23+at+6.47.34+PM.png?format=2500w)

As shown in Figure 4, the number of unique innovation does not differ much from each other. However, the possibility of having 1 or 2 unique innovations are high and similar. 

One of the proposed strategy to foster innovation is to decrease the parameter p_i. To test the effectiveness of this stratgey, the parameter p_s=0.5 is used on a 5 by 5 grid. 100 evenly spaced p_i are used, rangeing from 0 to 1. The simulation records the average number of unique innovation after 100 updates with 20 iterations. The result is presented in Figure 5.  

As shown in Figure 5, as p_i increases, the average unique innovation within 100 updates decreases. However, when p_i=0, there is no innovation. This causes a great leap in the beginning trend. The result suggests that decreasing p_i while keeping p_s constant may foster innovation, as long as p_i≠0.  

![Changing p_i while keeping p_s=0.5.](https://images.squarespace-cdn.com/content/v1/5a29de216957dab4049b897d/1577123427866-UWF5I0FFUW9SDOF5YT1C/ke17ZwdGBToddI8pDm48kHiykHIjs9O42AgOWYUv24oUqsxRUqqbr1mOJYKfIPR7LoDQ9mXPOjoJoqy81S2I8N_N4V1vUb5AoIIIbLZhVYy7Mythp_T-mtop-vrsUOmeInPi9iDjx9w8K4ZfjXt2dsUm1n6rKz7h2L1uSQXgmu0n6a6qCfCMf1NfpfOfxi4YCjLISwBs8eEdxAxTptZAUg/Screen+Shot+2019-12-23+at+6.50.04+PM.png?format=2500w)

The other proposed strategy to foster innovation is to increase the parameter p_s. To test the effectiveness of this stratgey, the parameter p_i=0.5 is used on a 5 by 5 grid. 100 evenly spaced p_s are used, the range is from 0 and 1. The simulation records the average number of unique innovation after 100 updates with 20 iterations. The result is presented in Figure 6.  

As shown in Figure 6, as p_s increases, the average unique innovation within 100 updates increases. When p_i=0, there is no innovation. The trend increases faster when p_s is low, and slower when p_s is high. The result suggests that increasing p_s while keeping p_i constant may foster innovation. Comparing strategy 2 to stratgey 1, the graph shows that strategy 2 will be more effective when p_s<0.5 due to its fast growth rate.  

![Changing p_s while keeping p_i=0.5](https://images.squarespace-cdn.com/content/v1/5a29de216957dab4049b897d/1577123593260-IR9Q7FPIQ30EWGO4E3C3/ke17ZwdGBToddI8pDm48kD_i1iiuv3uuO8ziX1pJu0MUqsxRUqqbr1mOJYKfIPR7LoDQ9mXPOjoJoqy81S2I8N_N4V1vUb5AoIIIbLZhVYy7Mythp_T-mtop-vrsUOmeInPi9iDjx9w8K4ZfjXt2ds0OsoGWBiARuDP4CeYx6241_issaDSBeO_KcBcXJriPCjLISwBs8eEdxAxTptZAUg/Screen+Shot+2019-12-23+at+6.52.55+PM.png?format=2500w)

The previous approaches only address change one parameter at a time. To further test the strategies, more combinations of p_s and p_i are tested on a 5 by 5 grid. 10 values of p_s and 10 values of p_i are used. The calculation iterates 10 times for each combo, and the mean out of these iterations are taken as the result and stored in a matrix. 

Figure 7 visualizes the result. The darker grids are the parameter combos with more unique innovations, and the lighter grids are the parameter combos with less unique innovations. The figure supports the previous finding that decreasing p_i or increasing p_s can foster innovation, as long as p_i≠0.  

![Combinations of p_i and p_s and their resulting number of unique innovations.](https://images.squarespace-cdn.com/content/v1/5a29de216957dab4049b897d/1577123771322-ZCVUR3RBESWQPHAMLP07/ke17ZwdGBToddI8pDm48kO5eXOxKdKfFEkoUFhDyq0IUqsxRUqqbr1mOJYKfIPR7LoDQ9mXPOjoJoqy81S2I8N_N4V1vUb5AoIIIbLZhVYy7Mythp_T-mtop-vrsUOmeInPi9iDjx9w8K4ZfjXt2di-Fy7Lu_MP6BIB_HX6u7M9wgOv49w5P7kRr97gtf4B3CjLISwBs8eEdxAxTptZAUg/Screen+Shot+2019-12-23+at+6.56.00+PM.png?format=2500w)

### Critics
There are several strengths and weaknesses of this model. These are listed and analyzed in this section. 

##### Pros
1. *Only two main parameters.* Only two main parameters are used in this model. This significantly reduce the complexity of simulating innovation. Also, it makes all analysis within three dimensions.  

2. *Randomization.* Randomization techniques are covered in multiple levels in this model to simulate how innovation emerges from a system. How ideas are chosen randomly based on a distribution that gives greater weight to higher level ideas are especially well designed.  

3. *Clear visuals.* Cellular automata has the strengths that each cell has a clear space coordinate. This helps with creating very clear visuals. 

##### Cons
1. *No consideration of network effect.* In the real world, network effect is crustal when it comes to innovation. People are continuously forming and breaking relationships. In addition, individuals with high popularity are more influential. In further studies, this aspect can be captured in the model. 

2. *No consideration of quality of ideas.* In this model, the birth stage of idea is 1, and it upgrades linearly or decays exponentially. This model does not capture the quality of the idea. 

3. *No consideration of dominance of ideas.* This is my main concern of the model. I observed that in most cases, an idea will eventually dominant the entire space so that another innovation cannot be born. Ideally, the number of innovation should scale as the number of update increases. However, I have observed that the number of innovation does not scale much as the number of update increase. In future studies, one can study how to eliminate the idea dominance case so that a society is actively changing and upgrading instead of stuck with one old tradition. 

![Number of unique innovation as update increase](https://images.squarespace-cdn.com/content/v1/5a29de216957dab4049b897d/1577123920065-2ES648VZAXFXJJ997RKZ/ke17ZwdGBToddI8pDm48kNyaqg816yidvS3BvjLVsOYUqsxRUqqbr1mOJYKfIPR7LoDQ9mXPOjoJoqy81S2I8N_N4V1vUb5AoIIIbLZhVYy7Mythp_T-mtop-vrsUOmeInPi9iDjx9w8K4ZfjXt2dhKkbia5pPkQAgQWN2PRQGAwqAQrn6aCVGiauj4GsOShCjLISwBs8eEdxAxTptZAUg/Screen+Shot+2019-12-23+at+6.58.03+PM.png?format=2500w)

### Insights and Conclusion
Based on the findings of the study, several suggestions are concluded for people that are interested in fostering innovation in their organization. 

1) *Create a culture so that people are comfortable sharing ideas.* The result suggests that increasing p_s is useful for fostering innovation. Hence, it would be great if people in one environment feels comfortable sharing their ideas. 

2) *Make sure each person has the opportunity to come up with something creative.* When p_i=0, there will be no innovation. Although there is no need for an organization to let agents come up with too much ideas, it is necessary that the agents at least have the time and opportunity to come up ideas. 

3) *Educate people so that less but better ideas are created at the first place.* A surprising finding of this project is that decreasing idea creation rate can foster innovation. This can be explained by the fact that too many ideas would disturb the best ideas from developing. However, I do not suggest to implement straight forward idea constraint because there is a risk of decreasing the value to 0. A better way to interpret the result is that an organization can educate people so that ideas are created focusing on quality, not quantity. 

### Conclusion 

This project establishes a non-deterministic cellular automata model and performs a Monte Carlo simulation on simulating innovation. It is found that when ensuring that ideas can be generated, decreasing the probability of idea generation and increasing the probability of social interaction can help to foster innovation. The finding suggests that creating a culture so that people are comfortable sharing ideas is helpful for society. Also, educating people so that ideas are generated focusing on quality, not quantity, can foster innovation. 

### Appendix

Code: https://drive.google.com/file/d/1IARzaNeATga6qx32ccAHX1OlCE2tLE4I/view?usp=sharing

### Citation

Adams, C. (2019, February 17). Can People Really Multitask? Retrieved December 20, 2019, from https://www.thoughtco.com/can-people-really-multitask-1206398.

McKinsey & Company. (2019). Growth & Innovation. Retrieved December 20, 2019, from https://www.mckinsey.com/business-functions/strategy-and-corporate-finance/how-we-help-clients/growth-and-innovation.

Shrestha, P. (2019, June 16). Ebbinghaus Forgetting Curve. Retrieved December 20, 2019, from https://www.psychestudy.com/cognitive/memory/ebbinghaus-forgetting-curve.

The Cambridge English Dictionary. (2019). INNOVATION. Retrieved December 20, 2019, from https://dictionary.cambridge.org/dictionary/english/innovation.

Walker, B. (2015, August 7). Innovation vs. Invention: Make the Leap and Reap the Rewards. Retrieved December 20, 2019, from https://www.wired.com/insights/2015/01/innovation-vs-invention/.
