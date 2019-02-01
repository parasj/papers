# Variational Auto Encoders

## What is the problem that is being solved?
 Autoencoders effectively learn dimensionality reduction. The hope is that they learn semantically meaningful embeddings of inputs into some lower dimensional space and filter the noise in the input.

## What are the metrics of success?
 SSIM/PSNR and other image similarity metrics

## What are the key innovations over prior work?
 * Denoising autoencoder: remove corruption from an image
 * VAE: control distributions of latent space to synthesize new unseen samples

## What are the key results?
 Can reconstruct images (eg MNIST) with high similarity scores. The technique can also learn semantic-aware embeddings.

## What are some of the limitations and how might this work be improved?
 VAE and GANs seem to have similar goals of extracting meaningful signal from data. I would be interested to see what a waveform interpretation of VAEs would look like. How does adversarial attacks fit into this framework?

## How might this work have long term impact?
 This would has had a lot of interesting impact in training high-accuracy DNNs and a lot of impact on GANs.
