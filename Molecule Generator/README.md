**VARIATIONAL AUTOENCODER TO GENERATE DRUG MOLECULES FROM SCRATCH**

**About** (Examples are shown below)<br/> 
The attached script consists of a Variational Autoencoder (VAE) Model that is able to create new drug molecules.
Given as input an existing molecule and choice of how similar you want the generated molecule to be,
 a new molecule is created that is compliant with Smile notation.

**Dataset**<br/>
Smile dataset consisting of 100k drug molecules. Available at: https://figshare.com/projects/GuacaMol/56639

**About the Model**<br/>
The Smile encoded molecules are converted into a one-hot-encoded an array with shape (Number of samples, length largest molecule, number of possible characters).
This is used to train the Variational Autoencoder model.

An Autoencoder is a pair of two connected networks, an encoder and a decoder. 
The encoder takes in an input and converts it into a smaller representation, called the latent space, which the decoder network converts back to the original input.
As the latent layer has far less units than the input, the encoder must choose to discard information. The encoder learns to preserve as much of the relevant information as possible in the limited encoding, and intelligently discard irrelevant parts. 

Variational Autoencoders are a variant of the Autoencoder.
Compared to the traditional Autoencoder, a VAE makes its encoder not output an encoding vector of size n, rather, outputting two vectors of size n: a vector of means, μ, and another vector of standard deviations, σ. From these two vectors, we sample the latent space.

The loss function consists of two parts:
-Cross-entropy between the output and the input, to reduce the difference between the input and output. <br/>
-Kullback–Leibler divergence between  μ, σ and the standard distribution. This pushes the latent space to mimic a standard distribution.  

More information about Vae's can be found at https://towardsdatascience.com/intuitively-understanding-variational-autoencoders-1bfe67eb5daf.

Optimizing the two together, results in the generation of a latent space which maintains the similarity of nearby encodings on the local scale via clustering, yet globally, is very densely packed near the latent space origin. As a consequence, their latent spaces are continuous. This is crucial as it allows easy random sampling and interpolation, which is not possible with a classic Autoencoder.

**How a new sample is generated**<br/>
An existing molecule is given as input. Following, the model outputs the corresponding μ and σ. 
From these two parameters the latent space is created. By playing with the variance, the resulting latent space is either similar or very different to the input molecule.
Finally, the created latent space goes trough the decoder which outputs a new generated molecule.

**Example**<br/>
The following molecule is used as input:<br/>
![alt text](https://github.com/Yvesvc/Machine-and-Deep-learning/blob/master/Molecule%20Generator/Image/base.PNG)

Now what happens when we want to create very similar molecules:<br/>
![alt text](https://github.com/Yvesvc/Machine-and-Deep-learning/blob/master/Molecule%20Generator/Image/8.PNG)
![alt text](https://github.com/Yvesvc/Machine-and-Deep-learning/blob/master/Molecule%20Generator/Image/7.PNG)
![alt text](https://github.com/Yvesvc/Machine-and-Deep-learning/blob/master/Molecule%20Generator/Image/4.PNG)

Let's make the new molecule a bit more different: <br/>
![alt text](https://github.com/Yvesvc/Machine-and-Deep-learning/blob/master/Molecule%20Generator/Image/5.PNG)

I want a very different molecule:<br/>
![alt text](https://github.com/Yvesvc/Machine-and-Deep-learning/blob/master/Molecule%20Generator/Image/1.PNG)
