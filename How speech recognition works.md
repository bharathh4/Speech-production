Essentially list all states. SIL_AA_0, SIL_AA_1 .. Z_SIL_0, Z_SIL_1, Z_SIL_3. You classify a frame using the acoustic models for all these states. So a frame and state have a score. You pick the next state based on the acoustic score and the transition probability. Actually you keep track of multiple paths. You are trying to get a state sequence or a alignment that is most likely to have produced the observation. It is an alignment problem. One can have a transition from any state to any state. AA_0 can transition to EY_2. It is unlikely. But if your acoustic model is really good, you can do that. In practice, you take a balance. The acoustic model gives the likelihood of being in a state. You make a transition based on transition likelihoods and acoustic likelihood. WFST help you with emitting labels at the right point besides being an excellent datastructure for search.

In the days before WFST, dynamic search was more common. The concept of Tokens has been around since 1989. On the fly tree or graph construction was very common. When making cross word transitions (say a word happens at the end of a 3rd state of the last phoneme in a word), language weights/costs were dynamically applied. These days these are done automatically uses WFST compostions easily. 


|    States   |     10ms    |    20ms     |            |             |    400ms    |    410ms    |   420ms     |  
| ----------- | ----------- | ----------- |----------- | ----------- | ----------- | ----------- | ----------- |
|   SIL_AA_0  |     Here    |             |            |             |             |             |             | 
|   SIL_AA_1  |             |     Here    |            |             |             |             |             | 
|   .         |             |             |     -      |             |             |             |             | 
|   .         |             |             |            |     -       |             |             |             | 
|   Z_SIL_0   |             |             |            |             |    Here     |             |             | 
|   Z_SIL_1   |             |             |            |             |             |             |    Here     | 
|   Z_SIL_3   |             |             |            |             |             |    Here     |             | 

