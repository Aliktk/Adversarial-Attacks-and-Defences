# Major Project
[asdas](#Architecture)
<h3> Title : An integrated Auto Encoder-Block Switching defense approach to prevent adversarial attacks </h3>
<p align="justify"> According to the recent studies, the vulnerability of state of the art Neural Networks to adversarial input samples has increased drastically. Neural network
is an intermediate path or technique by which a computer learns to perform tasks using Machine learning algorithms. Machine Learning and Artificial Intelligence model has become
fundamental aspect of life, such as self-driving cars, smart home devices, so any vulnerability is a significant concern. The smallest input deviations can fool these extremely
literal systems and deceive their users as well as administrator into precarious situations. This article proposes a defense algorithm which utilizes the combination of an auto-
encoder and block-switching architecture. Auto-coder is intended to remove any perturbations found in input images whereas block switching method is used to make it more robust
against White-box attack. Attack is planned using FGSM model, and the subsequent counter-attack by the proposed architecture will take place thereby demonstrating the feasibility
and security delivered by the algorithm.</p>

<h2>Dataset :</h2><pre>It is subset of Imagenet Dataset
Source : <a href="https://imagenet.stanford.edu/" >ImageNet </a>
<img src="Dataset/1.jpg"  style="width:100%">    <img src="Dataset/29.jpg"  style="width:100%">    <img src="Dataset/213.jpg"  style="width:100%">   <img src="Dataset/53.jpg"  style="width:100%"></pre>



<a name="Architecture"><h2>Architecture :</h2></a>
<pre>        <img src="Dump/Architecture.jpeg"  style="width:100%"></pre>
<h2>ML Models Used :</h2>
<pre>   1. <a href="https://www.tensorflow.org/api_docs/python/tf/keras/applications/resnet">Resnet</a>
   2. <a href="https://www.tensorflow.org/api_docs/python/tf/keras/applications/MobileNetV2">MobileNetV2</a>
   3. <a href="https://blog.keras.io/building-autoencoders-in-keras.html">Auto-Encoder</a>
   4. <a href="https://www.tensorflow.org/api_docs/python/tf/keras/applications/DenseNet121">DenseNet</a></pre>
<h2>Adversarial Attack :</h2>

1. Fast Gradient Sign Method(FGSM) - [Goodfellow, I. J., Shlens, J., and Szegedy, C. Explaining and harnessing adversarial examples. arXiv preprint arXiv:1412.6572, 2014b.](https://arxiv.org/abs/1412.6572)
```python
   def create_adversarial_pattern(input_image, input_label):
     with tf.GradientTape() as tape:
       tape.watch(input_image)
       prediction = pretrained_model(input_image)
       loss = loss_object(input_label, prediction)
     gradient = tape.gradient(loss, input_image)
     signed_grad = tf.sign(gradient)
     return signed_grad
```
<h2>Defense Architecture :</h2>
<table>
  <tr>
     <td><pre>Module 1 : Auto Encoder</td></pre>
    <td>Auto-encoders can be used for Noise Filtering purpose. By feeding them noisy data as inputs and clean data as outputs, it’s possible to make them remove noise from the input image. This way, auto-encoders can serve as denoisers.</td>
  </tr>

  <tr>
    <td><pre>Module 2 : Block Switching</td></pre>
    <td>Switching block in this experiment consists of multiple channels. Each regular model is split into a lower part, containing all convolutional layer. lower parts are again combined to form single output providing parallel channels of block switching while the other parts are discarded. These models tend to have similar characteristics in terms of classification accuracy and robustness, yet different model parameters due to random initialization and stochasticity in the training process</td>
  </tr>
  <tr>
    <td><pre>Module 3 : Grad-CAM</td></pre>
    <td>Grad-CAM ( Activation Maps )uses the gradients of any target concept (say logits for “dog” or even a caption), flowing into the final convolutional layer to produce a coarse localization map highlighting the important regions in the image for predicting the concept.”</td>
  </tr>

</table>
<pre><h3>   Auto Encoder :</h3>  Input – Adversarial image
   Output – Clean image after removing noise
   Auto-encoders can be used for filtration purpose.
   It is possible for them to remove adversarial noise from an input image.
   <img src="Dump/AE_output.PNG"  style="width:100%"></pre>
Project Organization
------------

    ├── README.md                         <- The top-level README for developers using this project.
    ├── Resources
    │   ├── AE_output.PNG                 <- Intermediate data that has been transformed
    │   ├── Architecture.jpeg             <- The final, canonical data sets for modeling
    │   ├── metrics.PNG                   <- The final, canonical data sets for modeling
    │   ├── result.PNG                    <- The final, canonical data sets for modeling
    │   └── gradcam.PNG                   <- The original, immutable data dump
    │
    ├── Dataset                           <- A set of markdown files with documented best practices, guidelines and rools for collaborative projects
    │
    ├── Dataset.zip                       <- Trained and serialized models, model predictions, or model summaries
    │
    ├── Full_Implementation.ipynb         <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g
    │                         `1.0-jqp-initial-data-exploration`
    │
    ├── Source_Code.py                    <- Data dictionaries, manuals, and all other explanatory materials.
    │
    └── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
  


--------
