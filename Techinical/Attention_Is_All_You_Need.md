
## This is the paper where transformers were intoduced. 

### Initial Questions

1. Why? -> LSTMs are difficult to be processed parallely, transformers leverage parallel processing.
2. How is position indicated? -> Positional embeddings are used to overcome lack of recurrence.
3. What is Attention -> The ability to amplitfy the signal from relevant part of the input sequence

### Basic Functioning

1. Processes each item in the input sequence, it compiles the information it captures into a vector called context.
2. This vetor is sent to the decoder after processing the entire sequence.
3. Context is basically a vector whose size can be set up in your model.
4. It is basically the number of hidden units in the encoder RNN.


### Encoder layer

#####  Simply stated encoders takes input sequence and maps it to different dimension. 
Maps all the input sequence into continous representation that holds the learned information for that entire sequence.

#### Multiheaded attention module
1. Self Attention -> Associate each word in the input to other word in the input.
2. 





```python

```
