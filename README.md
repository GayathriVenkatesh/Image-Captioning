# Image Captioning using CNN-LSTM

## Architecture Used

InceptionV3 and ResNet50 has been used for feature extraction, because:  
- They take less memory (in the range of 90-100 MB), and  
- Less parameters (approximately 25 million parameters or less)  

The model takes in two inputs:  
  - The output of the RNN which takes in the partial caption as input, and  
  - The image vector  

The model uses activation functions like ReLU and softmax to return two quantities:  
  - Predicted word (based on maximum probability distribution)  
  - Next word for the current partial caption.  

### Flow of the partial caption:  
  - The input layer takes in an array of indices corresponding to partial captions.  
  - Every index in this partial caption gets mapped to a 200-dimensional feature vector in the embedding layer.  
  - We have used dropout layers to prevent overfitting of the model.  
  - This is then passed to the LSTM. This will help the model learn about the ‘ordering’ of words in a sentence.  

### Flow of image vector:  
  - The input layer thales in a feature vector of dimension 2048.  
  - There is another dropout layer to minimise overfitting, which is then passed to the dense layer.  
At the end of these two steps that run parallely, the output of both are of dimension (batch size, 256), and
are hence merged into a single vector.  

The output layer uses softmax to generate probability distribution across all the words in the vocabulary,
based on which the final prediction will be made.  

## Model Description:
- Total params: 1,483,648
- Trainable params: 1,483,648
- Non-trainable params: 0

### The following were used:
- Activation Function: ReLU
- Regularization: 50% dropout and batch normalization
- Hyperparameters:
  - Learning Rate: 0.01
  -   Batch Size: 100
  -   Number of epochs: 200
- Loss Function: Categorical Cross-Entropy
- Optimizer: Adam

Final BLEU score on the Flickr 8k dataset : 0.5184
