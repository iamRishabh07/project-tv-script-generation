# project-tv-script-generation

<div align="center">
<img src="https://s3.amazonaws.com/video.udacity-data.com/topher/2018/October/5bbaed49_project-3-lesson/project-3-lesson.jpg" height="300" width="300" />
<br />
<h1>Generate TV Scripts</h1>
</div>

## Project Overview

In this project, I have generated my own Seinfeld TV scripts using RNNs. I have used a Seinfeld dataset of scripts from 9 seasons. The Neural Network will generate a new, "fake" TV script.

## What is it?
This project generates Seinfeld TV scripts using RNNs.  

Udacity provided part of the Seinfeld dataset of scripts from 9 seasons. The Neural Network generates a new ,"fake" TV script, based on patterns it recognizes in this training data.   

Sample generated script:
```
jerry: king jet, 1992, deceived, deceived.

[new witness: pharmacist?

george: what? i don't even think this is it.

elaine: what?

jerry: yeah.

kramer: oh, that's right.

george: hey, you know, you know, maybe it was a lot of people could be in the country, and i will be going to get to see you.

george: you know what?

elaine: yeah.

kramer: hey, hey, what's the difference?

hoyt: well i guess i could be dating the defendants of a day. you know what the worst would spend it up for a while.

george: what?

george: well, i can't eat it anymore.

hoyt: so, what's going on?

jerry: no, no.

hoyt: i don't know. i don't know how much money. i was employed.

kramer: oh. i know.

george: what?

george: no, not a good sandwich.

kramer: well, maybe you have a good chance to go.

jerry: well, you can get out with you.

jerry: you know, i think i was in the same birthday party and i can go to the bathroom.

elaine: what?

kramer: i don't know.

jerry: so you can tell him how much i was going to do that. i had it to hell and i had to go see that i had to be a little bit of a friend of humor.

elaine: yeah.

elaine: i can't stand without the pen. it's a little anxious.

elaine: yeah, yeah, i don't know.

elaine: oh, no, no!

jerry: so, you have to tell you what.

elaine: well, it's a good sandwich. you know, i was thinking of thinking to you, and the whole country was king.

elaine: what? why?

jerry: you
```

## What did I do?   

I implemented data loading and pre-processing as well as the RNN network.  

## Choosing the hyperparameters
Choosing the hyperparameters requires not only knowledge, but also luck, intuition, and patience. *Especially*, patience. One epoch takes more than an hour and it's really hard to observe the training and not to try to improve it at the same time.  


### Learning rate = 0.001
0.01 is a good starting point. 0.001, 0.0001, and 0.1 are also good values.  

I tried 0.01, but the network was not learning, while 0.001 allows the network to improve the loss fast.

### Sequence length = 10
I didn't find specific recommendations about sequence length, the common answer is, "it depends."   
I noticed that shorter sequence length makes faster iterations with good improvements in the loss.  

I started with sequence length = 200 and every epoch was literally talking hours. Decreasing the sequence length was the most impactful decision in this project as it allowed the model to train _much_ faster (<15 minutes per epoch) while almost not affecting the loss.  
Setting a low sequence length allowed me to experiment with other parameters.

### Batch size = 100
According to the course, recommended starting point is 32. 32 to 256 are potentially good starting values.
Larger size may computational boost due to optimized matrix multiplication, but it can stuck in local minimum.  

I also tried 64, it was slightly faster and producing slightly better loss.


### Embedding dimension = 300
The example architectures use embedding dimension from 100 for text summarization to 1000 for translation.   
After experiment with other values (e.g., 200), I chose a value in between: 300 to give the network more capacity to learn.  

### Long Short-Term Memory (LSTM) or Gated Recurrent Unit (GRU)? LSTM
There is no universal advice on whether to use LSTM or GRU.  
I started with LSTM, and also tried GRU. LSTM was producing better results.

### Number of RNN layers = 2
General recommendation is to choose two or three layers. I chose three layers to give my network more capacity to learn.

### Hidden dimension = 300
The example architectures use size from 200 for text summarization to 1000 for speech recognition for large vocabulary.  
I chose 300 because my embedding dimension was 300. Intuitively, the hidden dimension should be greater than the embedding dimension.  
I also tried 200 while using 200 for the embedding dimension.  

I chose `Embedding dimension = 300` and `Hidden dimension = 300` because their training loss was slightly better than for lower values while almost not affecting the training time. 

[MIT](https://choosealicense.com/licenses/mit/)
