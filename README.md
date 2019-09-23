# DL_text_analysis_novels
text detection - plagiarism detector trained on classic novels

### Data cleaning/prep: Four novels were chosen from the gutenberg project
* The Picture of Dorian Gray
* The Life of Frederick Douglass
* War & Peace
* Wizard of Oz

I frankly chose these novels for their diverse subject matter, style, and time of being written. While this may be "cherry picking", in some sense, the goal is to demonstrate feasibility, and I happen to just like these books/thought they'd be interesting. 

### Results & Discussion, Dense model
* Note: with stock HPs from template, we achieve 84% (training) accuracy with the dense model

* Round 2: 2000 train / 100 test
* - Increased max sentence length by 50% (30 words)
* - Increased word embedding by 50% (8 --> 12)
* - Updated epochs to 15 (also 50% increase)
* - Result: 92.3% train accuracy, 78.5% test accuracy

* Round 3: 4000 train, 800 test
* - Sentence length unchanged (30 words)
* - Unchanged (embedding depth 12)
* - Unchanged epochs (15)
* - Result: 93% train accuracy, 76% test accuracy
* -- NOTE: test set is significantly larger here - 4000 train, 800 test

* Round 4: added extra dense layers and a few conservative dropout layers. 
* - Model converges faster to a higher training accuracy (96.5%), but we achieve similiar performance (71%) on validation set (test set). 
* - Note that this value is lower than the best achieved in prior at tempts, which ultimately/likely has to do with random sampling of the test set after having to reset runtimes while working in the notebook. 

### Results, using an RNN (LSTM):
* 92% training accuracy
* 71% test accuracy
* - note that no changes were made to the input word embeddings for apples to apples comparison. 

Round 2 - updated dimensionality of LSTM output from 32 to 64. 
* This yielded worse results (~90% train, 69% test)

Round 3 - extended word embeddings (15->30), returned to LSTM unit depth of 32
* 94% training, 76% test

Round 4 - added dense layers from "round 4" of the feedforward baseline after the LSTM layer
* takes longer to train
* lower training accuracy
* equivalent validation accuracy (71%)

Round 5 - removed one dense layer and dropout layer.
* Faster to train
* Improvement in trainign accuracy
* Equivalent validation acc

### Discussion - Decision to use dense model for web deployment
* Given that this is basically equivalent performance to the dense/feed-forward approach, and there is not a significant difference in the number of parameters, we will stick with the dense network to deploy into our webpage. 
* It's also worth noting that both models achieved very similar levels of performance on the latest test set (~71%). Furthermore, it's somewhat surprising that the training score for the dense model exceeded that of the LSTM- I would have thought that the use of "directional" context would have improved the model's ability to fit to the training data. 


