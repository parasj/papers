# Inception-v4, Inception-ResNet and the Impact of Residual Connections on Learning

## What is the problem that is being solved?
 Inception v3 worked on distbelief but not on tensorflow. Key problem is to design an inception variant that trains quickly and can utilize tensorflow.

## What are the metrics of success?
 a) can it run on tensorflow
 b) architectural simplicity
 b) *validation accuracy*
 d) training time

## What are the key innovations over prior work?
 By using tensorflow, memory was no longer a constraint. So residual connections were now a design option. Inception v4 simplifies prior architectures and slims the network. Residual connections improve training speed without affecting accuracy.

## What are the key results?
 Faster training. Same validation accuracy. Simpler architecture

## What are some of the limitations and how might this work be improved?
 This work does not seem novel. It mostly looks like it's a reengineering of earlier design choices with the availability of a better system.

## How might this work have long term impact?
 It has been cited, but I don't think this paper (v4 specifically) has had much impact. Earlier paper revisions have had much more impact though. The idea of factorizing training and multiscale filters have carried into blocks like atrous spatial pyramid pooling (ASPP) for example.
