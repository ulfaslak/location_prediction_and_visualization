

List of papers
--------------

### Relavant

"Artificial Neural Networks Applied to Taxi Destination Prediction", **brebisson2015**.

*Details*

- This paper **predicts taxi destination** based on beginning of trip trajectory (and possible historical data of customer based on telephone id).
- Model output is **geographical coordinates** and accuracy is average haversine distance (avg.: 2.03489).
- Their model architecture gives a **fixed length output** from a **variable length input**.
- Winner of [Kaggle competition](https://www.kaggle.com/c/pkdd-15-predict-taxi-service-trajectory-i).

*Questions*

- How is location handled? Are they using multiple regression to predict locations coordinates or are they segmenting the map into grid squares?
- Can the same be done for human location independent of transportation mode?

<br>
"Predestination: Inferring Destinations from Partial Trajectories", **krumm2006**.

*Details*

- Predicts driver **destination from trajectory** and *driving behavior* such as types of destinations, driving efficiency, trip times.
- Uses *open-world* methodology to consider likelihood of visiting **previously unobserved locations** based on trends in data and background properties of locations.
- Method has multiple modeling components. Fuses those with **Bayesian probability estimate** to get probabilistic map of destinations.
- Treats geography as **grid cells**.
- Fig. 8 is a nice way to show that with more data the model would be even better.

<br>
"Travel Destination Prediction Using Frequent Crossing Pattern from Driving History", **kostov2005**.

*Details*

- Treats **geography as a network**. Derives *Crossing points* from locations where users paths frequently cross to simplify spatial representation. This a trip can be `Home` `->` `CP1` `->` `CP2` `->` `Work`.
- They construct a tree (FP-tree) of movement points for each starting location where root is a starting destination and leafs are destinations.
- They automatically determine time-categories. I guess they make an FP-tree for each category. Appears very data-expensive.

*Critique*

- The CP approach may not work for a very large number of patterns, since there would be too many crossing points.
- FP-trees require that a trip has already been made once before it can be predicted again. This is not very nice. May require a lot of data.

<br>
"Understanding Predictability and Exploration in Human Mobility", **cuttone2016**.

*Details*

- Investigates which dataset and analysis dependent **factors that influence** the reported performance of predictive models.
- Study references closely.

*Results*

- Exploration (25% of transitions, 70% of locations) is a major limiting factor.
- Occurance of exploration can be predicted with 41% accuracy. Getting better at predicting exploration would directly mean getting better at predicting location.
- It is easier to predict where a person is going to be in the next timebin than it is to predict what the next place (which is not the current) is. This is obviously because always guessing that the next timebin location is the current will give a relatively high accuracy that only a very good model can beat.
- Increasing timebin size enhances predictability because there are few self-transitions.
- Current location + weekhour are the minimally necessary parameters to use to get the best prediction accuracy for next location prediction (accuracy: 0.42)
- Negative correlation (-0.478) between exploration rate and user model prediction accuracy.
- Exploration may be bursty.

*Questions*

- Do they fit a logistic regression model for each location for each user? I guess they want to compute the probability that a set of state variables leads to a given location being the next one. Then how could they only make one model per user?
	- Ahhh! Their data is [current, potential next, state vars., ...] -> [bool]

<br>
"Application of neural network techniques for location predication in mobile networking", **bilbukar2002**

*Details*

- Makes a very simple neural network with three inputs (X, Y, t), four hidden states and two outputs (X, Y). X and Y are grid coordinates.
- They use very little data and don't really compare their results to anything.

<br>
"Mobility Prediction in Wireless Ad Hoc Networks using Neural Networks", **kaaniche2010**

*Details*

- Introduces the concept of mobility prediction in mobile adhod networks (MANETs). Main advantage is it can be used to predict link expiration times in order to improve routing performance. Simpler put it's important for nodes in a MANET to know how long they can expect to be close enough to each other that data packets have time to be transmitted without broken connection.
- They use a slightly more sophisticated architecture than bilbukar2002. They consider each coordinated (x, y, z) to have its own timeseries and train three networks of the same architecture. The network has three input nodes (t-1, t-2, t-3) plus a bias input, one hidden layer with three nodes and one bias, and a single output, which feeds back into the input as t-1 (i suppose only when they do long forecasting).
- The quality of their results is poorly documented and sort of impossible to evaluate. It looks like predictions follow the target, but how do they compare to a stationary process or a markov chain?


<br>
"Citizens as sensors: the world of volunteered geography", **goodchild2007**.

*Note*

- May be relevant when discussing the feasiblity of an app where users upload their location data and we **visualize** their location predictions.

<br>
"Limits of Predictability in Human Mobility", **song2010**.

*Details*

- Highly cited Science paper with Barabasi on it.
- Finds that users are highly predictable when what you try to predict is what tower a next call will be connected to. With reference to cuttone2016, this is the "easy way" to predict location. Harder would be to try to predict where the user moves to next (which cannot be the current location).

<br>
"A universal model for mobility and migration patterns", **simini2012**

- Population level mobility prediction using a stochatic process which rivals the classical gravity model of population migration.
- Not something we can use explicitly in our work, but may be relevant to cite it to clarify that we are aware of this field.

<br>
"Predictability of Individuals’ Mobility with High-Resolution Positioning Data", **lin2012**

*Details*

- This paper is in many ways stupid. They try to show how predictability (fancy math inverse entropy) changes as gridsize and temporal binsize is varied for some human mobility data.

*Critique*

- Unsurprisingly, they demonstrate that as you decrease temporal binsize the predictability increases. This is obviously because the markov chain becomes very stationary. They also show that increasing the spatial binsize increases predictability. Again this is just a mathematical consequence. In light of Cuttone's paper this is just a misleading waste of time. **Do not cite**.

<br>
###Worth noting

- "Location prediction algorithms for mobile wireless systems", cheng2003
- "A Prediction Based Location Management Using Multi-Layer Neural Networks", kumar2002


<br>
### Not relevant

"comMotion: a context-aware communication system", **marmasse1999**.

*Details*

- Provide information to users based on location.
- Has a small location classification component, which I guess is just some clustering.

<br>
"Mobility Prediction in Wireless Networks Using Neural Networks", **capka2004**

*Details*

- Uses a neural network to predict cell tower connections over time.
- Doesn't show their architecture or provide any visual quantative overview of their results.
- Don't cite, they are noobs.



<br>
Literature review
-----------------

*Bits that need to go in it*

- Location prediction has plays a vital role to call routing in cell networks \cite{cheng2003, kumar2003, bilbukar2002, capka2004}. Before a user can answer their phone the system must know which cell tower is nearest to that user. By predicting location the system can avoid using expensive paging and location update protocols.
- Location prediction has been used to data transmission in mobile ad-hoc networks (MANETs) \cite{kaaniche2010}. MANETs are self-organizing mobile networks of devices that can route information (e.g. laptops or smartphones) in a decentraliced manner. By predicting future locations of single nodes in the network, it is possible to infer when connections between pairs of routers will expire and manage the way data is propagated through the network more efficiently.
