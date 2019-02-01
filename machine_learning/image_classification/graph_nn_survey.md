# Graph Neural Networks: A Review of Methods and Applications

## What is the problem that is being solved?
 Graphs are hard to process for neural networks as they are in a non-euclidean space and are sparse. Graph Neural Networks aim to learn representations for graphs that are semantically meaningful embeddings.

## What are the metrics of success?
 Reconstruction error, application specific metrics?

## What are the key innovations over prior work?
 Pre-deep learning: Spectral methods
Recent work: Graph attention networks, GGNN, GLSTM

## What are the key results?
 Can learn meaningful embeddings of the structure of graphs, with promising results in program verification, genomics, etc.

## What are some of the limitations and how might this work be improved?
 I am suspicious of the metrics. There should be a clearer benchmark for how to apply these methods. I think some limitations are a tradeoff between local structure and global structure of graphs. Some problems rely on local structure (program verification) while others apply to the graph as a whole (spectral methods).

## How might this work have long term impact?
 I think a lot of impact will occur in the program synthesis and program verification fields. Programs are naturally represented as graphs.
