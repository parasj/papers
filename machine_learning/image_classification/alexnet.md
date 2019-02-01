# ImageNet Classification with Deep Convolutional Neural Networks

## What is the problem that is being solved?
 The key problem solved by AlexNet is that prior approaches to large NN training were not successful before due to compute reasons. By implementing high-performance kernels on GPUs, deeper networks learned richer representations which led to state-of-the-art performance.

## What are the metrics of success?
 1) imagenet validation accuracy
 2) is it overfitting?
 3) speed of training
 4) number of network parameters

## What are the key innovations over prior work?
 AlexNet solves 2 issues a) addresses overfitting issues with DNN training and b) uses GPUs to train larger networks

## What are the key results?
 State of the art results (almost 10% better validation accuracy)

## What are some of the limitations and how might this work be improved?
 Clear limitations of the approach as evidenced by many later works. Some key issues named by Alex: a) only useful for supervised learning but not for unsupervised learning and b) video "infero-temporal" learning

## How might this work have long term impact?
 Obvious large impact. Some interesting points that were covered in the paper but forgotten for some time: a) AlexNet was both DATA parallel and MODEL parallel. The second is a new research topic which is interesting with larger high resolution models and b) interesting conclusion that depth > breadth, which is taken for granted now.
