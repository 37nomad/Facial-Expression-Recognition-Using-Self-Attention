# Facial Expression Recognition Using Self Attention


> 

## Abstract

Facial expression recognition (FER) is a critical task in computer vision, aimed at identifying human emotions from facial images. This project leverages deep learning techniques to classify facial expressions into distinct categories, such as happiness, sadness, anger, surprise, fear, disgust, and neutral. We utilize a convolutional neural network (CNN) architecture with a ResNet18 backbone (till layer 3) integrated with CBAM, also combined with patch extraction block and attention mechanisms to enhance the model’s ability to capture subtle facial features critical for accurate classification. Our dataset comprises labeled images representing each expression, and we apply data augmentation techniques to improve generalization and performance. We employ various optimizers and regularization techniques to minimize overfitting and maximize accuracy. Experimental results demonstrate the model's effectiveness, achieving substantial accuracy and robustness across different expressions.

## Dataset Description

Dataset used for this project for training and testing was RAF-DB. The dataset was extracted from Kaggle it consisted around 13000 images for training set and around 3000 images for test set. Images in this database are of great variability in subjects' age, gender and ethnicity, head poses, lighting conditions, occlusions, (e.g. glasses, facial hair or self-occlusion), post-processing operations (e.g. various filters and special effects), etc. 

![FER Readme/image.png](FER%20Readme/image.png)

Following transform function was applied to the training data set :

![FER Readme/image 1.png](https://github.com/37nomad/Facial-Expression-Recognition-Using-Self-Attention/blob/main/FER%20Readme/image%201.png)

## **Literature Review**

In this project, several key topics and techniques have been explored to enhance the effectiveness of facial expression recognition. These topics form the foundation of our approach and contribute significantly to the project’s overall performance and accuracy.

### CBAM (Convolutional Block Attention Mechanism)

CBAM amalgamates CAM and SAM within a sequential framework, yielding superior outcomes compared to models reliant solely on CAM. The configuration of the CBAM network is depicted in Figure , where F signifies the feature image
derived from the convolution layer, Mc(F) represents the generated channel attention image, F’ corresponds to the feature image obtained by multiplying F with Mc(F), Ms(F’) signifies the spatial attention image generated, and F’’ denotes the feature image derived from the multiplication of F’ and Ms(F’).

![image.png](https://github.com/37nomad/Facial-Expression-Recognition-Using-Self-Attention/blob/main/FER%20Readme/image%202.png)

### Patch Extraction

Patch extraction block consists of three different convolutional layers, the first two being depth wise separable convolutional layers and the last being a pointwise convolutional layer. Operating on feature maps from the ResNet18 backbone producing the feature map dimension 32*14*14*256 (where 32 is batch size, 14*14 are spatial dimension, 256 is no of channels), the first separable convolutional layer is responsible for splitting the feature maps into four patches while learning higher-level features from its input. Subsequently, the second separable convolutional layer and the pointwise convolutional layer are responsible for learning the higher-level features from the patched feature maps, resulting in output with a dimension of 2 × 2. Instead of the standard convolutional layer used in conventional CNNs, the depth wise separable convolutional layer is selected for this model. This design decision improves the classification performance of the proposed method on challenging subsets while reducing the number of model parameters.  

![patch extraction.png](https://github.com/37nomad/Facial-Expression-Recognition-Using-Self-Attention/blob/main/FER%20Readme/patch_extraction.png)

### Self Attention

Self-attention mechanism where the attention weights are computed as a dot product between the query vector and the key vector, divided by the square root of the dimension of the key vectors. Self attention, is a mechanism that allows a neural network to focus on specific parts of its input during computation selectively. The idea behind self-attention is to allow the network to learn a set of attention weights that indicate how important each input element is to the output of the network. It has become a popular technique in natural language processing and computer vision tasks as it can help improve performance by selectively attending to the most relevant parts of the input.

Let Q, K, and V be the query, key, and value vectors, respectively, and dq = dk. The dot-product self attention score can be computed as follows:

![image.png](https://github.com/37nomad/Facial-Expression-Recognition-Using-Self-Attention/blob/main/FER%20Readme/image%203.png)

where dk is the dimensionality of the key vectors. The SoftMax function is applied to the dot-product similarity scores to obtain a set of attention weights that sum up to 1. These weights are used to compute a weighted sum of the value vectors, resulting in the final attention output.

## Model Architecture

![model.png](https://github.com/37nomad/Facial-Expression-Recognition-Using-Self-Attention/blob/main/FER%20Readme/6b5a58f1-124d-46c9-8b26-78dce190b9c1.png)

Here Self Attention has 1 head.

Optimizer : Adam with Weight Decay

Criterion : Cross Entropy Loss

Learning Rate : 0.001

Batch Size : 32

## Experiments and Results

We have tried to use various architectures for this project like incorporation of Self Cure Network, Patch Gated Unit etc. but they haven't shown satisfactory results. Also tried using various backbones for the architecture and for this also the results weren't that satisfactory. 

Incorporation of Self Attention has significantly improved the classification and incorporating it with patch extraction block has provided an accuracy of 78.16% at 15th epoch on test dataset which was trained for 20 epochs. From here it was trained on augmented training data and the generalization of the model improved and provided an increment of accuracy to 82.2% which was trained for 12 epochs.

Here is the following Confusion Matrix on the test dataset :

![Untitled.png](https://github.com/37nomad/Facial-Expression-Recognition-Using-Self-Attention/blob/main/FER%20Readme/Untitled.png)

## Discussion

In this facial expression recognition project, we implemented a customized architecture based on ResNet-18, enhanced with the Convolutional Block Attention Module (CBAM) and multi-head self-attention. These additions provided significant performance gains over a standard ResNet baseline. The CBAM module selectively emphasized important features in both channel and spatial dimensions, allowing the model to focus on salient facial regions, such as eyes and mouth, which are critical for expression analysis. Additionally, the integration of a self-attention mechanism helped the model capture global dependencies within an image, facilitating a deeper understanding of context beyond local patterns. By employing patch extraction, the model effectively broke down the image into localized patches, allowing the self-attention module to further capture interactions among different facial regions, enhancing feature representation.

These architectural enhancements, combined with extensive data augmentation, enabled better generalization across diverse facial expressions and lighting conditions. The use of AdamW as an optimizer further improved model performance by decoupling weight decay from adaptive gradient calculations, resulting in more stable updates and reduced overfitting. As a result, the model achieved superior accuracy and robustness in predicting nuanced facial expressions, making it highly effective for real-world applications where subtle expression variations are critical.

## References

Following Research Papers have helped me doing this project :

https://arxiv.org/pdf/1706.03762 

https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=10287346&tag=1 

https://arxiv.org/pdf/2002.10392

https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8545853

