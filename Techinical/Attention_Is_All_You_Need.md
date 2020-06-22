
# This is the paper where transformers were intoduced. 

## Initial Questions

1. Why? -> LSTMs are difficult to be processed parallely, transformers leverage parallel processing.
2. How is position indicated? -> Positional embeddings are used to overcome lack of recurrence. We add positional encoding vectors -- the values of which follow a specific pattern
3. What is Attention -> The ability to amplitfy the signal from relevant part of the input sequence

## Basic Functioning

1. Processes each item in the input sequence, it compiles the information it captures into a vector called context.
2. This vetor is sent to the decoder after processing the entire sequence.
3. Context is basically a vector whose size can be set up in your model.
4. It is basically the number of hidden units in the encoder RNN.


## Encoder layer

#####  Simply stated encoders takes input sequence and maps it to different dimension. 
Maps all the input sequence into continous representation that holds the learned information for that entire sequence.

### Steps:
1. The input to the encoder is a list of vectors.
2. Input is passed to the self-attention layer
3. The output from the seldf-attention layer is passed to the feed-forward neural network/
4. This output is sent to another encoder if any.


####  Self-Attention

Associate each word in the input to other word in the input. "Self-attention is the method the Transformer uses to bake the “understanding” of other relevant words into the one we’re currently processing." - Jay Allamar Blog

#### Calculation

1. From the input to the encoder (word embeddings/output of other encoders), generate a Query vector, a Key vector, and a Value vector. These vectors are created by multiplying the embedding by three matrices(Wk,Wq,Wv) that we trained during the training process.
2. Calculate score by taking the dot product of the query vector with the key vector
3. Divide the score by the square root of dimension of the key vector (8 for the paper) and pass through softmax (sums to 1 and positive). This softmax score determines how much each word will be expressed at this position.
##### This score will be high if the word is at correct position, for "incorrect" positions this score will be low.
4. Multiply each value vector with this score, this way only the correct position value will be propagated, and then sum up these vectors.
##### Though calculated for each word, we can pass input in form of a matrix to work on all the words in the input.

#### MULTI-HEAD

1. As mentioned in the def of self-attention, it focus on a word being at a relevant position.
2. So it is necessary to look at a word from different perspectives (relevant positions or as mentioned in the blog what will the word "it" refer to), this is referred as giving the attention layer multiple “representation subspaces”.
3. So this is achieved by means of multiple heads. 
4. Each head has its own set of trainable vectors and in the end we combine their outputs.
5. We concatenate these outputs and multiply by another matrix, which is also trained, to obtain the final output of the self attention layer.


## Decoder Layer

Most of the components mentioned on the encoder are also mentioned on the decoder side as well. 


### Steps

1. The output of the top encoder is then transformed into a set of attention vectors K and V. 
2. These are to be used by each decoder in its “encoder-decoder attention” layer. 
3. Step 2 enables the decoder focus on appropriate places in the input sequence.
4. Decoder continues till the EOS character is reached.
5. As we are trying to map input to output it is neccessary that we decoder should not be able to see the entire output sequence at once, thus the input to the decoder is only the words which have been generated previosly by the decoder.
6. The “Encoder-Decoder Attention” layer works just like multiheaded self-attention, except it creates its Queries matrix from the layer below it, and takes the Keys and Values matrix from the output of the encoder stack.
 
## Linear and softmax layer

1. Output of the decoder is vector of floats and not words, this translation is done by the linear layer followed by the softmax layer.
2. Linear layer is a FC network that projects the vector produced by the stack of decoders, into a much, much larger vector called a logits vector. 
3. Each cell of logits vector corresponding to the score of a unique word.
4. The softmax layer then turns those scores into probabilities (all positive, all add up to 1.0). The cell with the highest probability is chosen, and the word associated with it is produced as the output for this time step.



```python

```
