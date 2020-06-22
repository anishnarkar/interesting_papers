
### Federated Learning

1. Large Scale distribution training on sensitive data is termed as federated learning.
2. Designed to train with  millions of participation who have unbalanced, non iid distribution.
3. The main goal to implement this is to improve performance and scalability.

### Issues with Federated Learning

1. Privacy and robustness are important issues.
2. Original design does repeated averaging of model updates from small participants, making it sensitive to outliers.
3. This makes the model vulnerable to malicious users who might affect the model's robustness.
4. Updates and final  model can leak data which affects privacy aspect.


### Differential Privacy

1. To limit the leakage of training data, federated learning has been combined with differential privacy
1. Equation mentioned ( Refer the equation in paper of form G(t) = G(t-1) + ..) gives differential difference, where S is the clippinng bound and N(0, Sig) is the noise.
2. Local training is done at each participant on a model which is send to them by a central server, which creates G(0).
3. In each round (say t), the server selects a subset of 'm' participantst from sample pool Q of size n and sends the current model G(t-1).
4. Each particpants updates the local model on local data and send the resulting model Pi(t) to server.
5. Server thenn updates the local model with the above equation.
6. Selection of clipping bound and noise is done by (sig, S), deterimines degree of level of participation's update and adds random noise.

#### Note

1. FM model can perform well on the global dataset but poorly on individual's personal dataset.
2. This reduces the incentive to participate in study.
3. More noise you distort the model greatly.

### Paper's recommendation

1. Observation of the paper indicates that federated model are less accurate than the model trained on their own datasets for majority of the partipants, which questions the who excerise of distribution training.
2. Local adaptation is recommended to convert federate model into individual model to solve issues with respect to privacy and robustness.
3. The following are the mechanisms mentioned:
    A. Fine Tuning
    B. Multitask Learning
    C. Knowledge Distillation

#### Fine Tuning

1. Retrains all the model pararmeters from federated model(FM) on local data, using the hyper parameters mentioned.
2. Utitizes feature extraction network of FM instead of learning from scratch.
3. Freeze Base version freezes base layers and fines only top layer.
4. Fine tuning by adapting the learning rate and freezing the layers should improve accuracy. 


#### Multitask Learning Learning (MTL)

1. With non-iid distribution, local data may be very different between participants, leading to overfitting.
2. To mitigate this, local adaptation can be treated as a multi-task learning problem. 
3. Task X requires high performance on the union of all participants.
4. Task Y requires high performance on a single participant.
5. We take the federated model GT optimized for task X to create an adapted model A which is optimized for task Y.
6. But it is possible that the model might forget the information from the base mode (Catastrohic forgetting) this is avoided by Elastic weight consolidation
7. Elastic weight consolidation  which selectively slows down learning on the weights important for task X.


#### Knowledge Distribution(KD)

1. We treat the federated model GT as the teacher and the adapted model A as the student.
2. Both models are based on the same dataset but the student is much simpler than the teacher.
3. Knowledge distillation extracts information from a “teacher” model into a “student” model.
4. Both models have the same structure and A is initialized to GT
5. The dataset on which A is trained is a small subset of the dataset on which GT is trained.
6. Similarity of logits between GT and A using the loss function helps mitigate overfitting on the small dataset.




```python

```
