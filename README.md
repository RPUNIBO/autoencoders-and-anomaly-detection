# autoencoders-and-anomaly-detection
In this notebook we build a simple auotencoder for Mnist data, and show how to use it for anomaly detection.

Both the encoder and the decoder are just composed by a couple of dense layers. The latent dimension is 16. That means that each input is reduced from an initial dimensions of 28*28=784 to a an internal dimension of just 16 floats.

Most of the relevant information is preserved, as testified by the fact that we are able to reconstruct, out of this 16 values, an image very similar to the original one.

As loss function we can take mse or categorical crossentropy, as you prefer.

After loading the datatet, we normalize it in the range [0,1]. We are not using labels.

We fit the model. Observe that the ground truth we need to compare with is in this case the input itself. In other words, the loss is the distance between the inout  X  and its reconstruction  X^

After checking the result.
We compute all reconstructions for images in the test set.

Then we plot the result. We pick ten random images, and for each of them we show the original and the reconstruction obtained from the autoencoder.

Wethen want to show how we can use an autoencoder for anomaly detection.

The genral idea is that the encoding learned by the autoenoder is data-specific. This means that if we apply the autoencoder to an outlier, the resulting reconstruction should be sensibily worse than usual, and we may exploit this simple fact to detect the anomaly.

The first step of the procedure is to identify the canonical expected reconstruction error on true data, and the associated standard deviation.
Now we create an "anomaly". We simply take a normal image from the dataset, and rotate it of 90 degrees.
For this example, we use image no 15 in the test set.

Observe that the reconstruction is not particularly good, but still the loss (0.207) is more or less on std away from the mean, that is a normal behaviour.
Now, let us rotate it and repeat the computation.

The mse in this case is 0.052, more than 3 std away form the mean, that is surely an anomaly!!
