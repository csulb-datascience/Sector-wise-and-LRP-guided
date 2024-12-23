# Innovations in Dropout Techniques with Sector-wise and LRP-guided Approaches
This repository is the official implementation of "Enhancing Generalization in Neural Networks: Innovations in Dropout Techniques with Sector-wise and LRP-guided Approaches" paper.
The Sector-wise dropout approach systematically divides the nodes in each layer into sectors, applying deactivation based on a fixed dropout probability to ensure a more structured network architecture. LRP-guided Dropout leverages scores from Layer-wise Relevance Propagation (LRP), computed subsequent to parameter updates, to selectively deactivate nodes positioned within the highest percentile of LRP scores. Through empirical evaluation, we establish that these innovative approaches markedly enhance the balance and generalization capacity of neural networks, thus representing a significant progression in mitigating the overfitting conundrum.

<img width="753" alt="image" src="https://github.com/csulb-datascience/Sector-wise-and-LRP-guided/assets/44173994/d499504f-4b98-49d8-9d2d-934f9c350cc9">

A conceptual diagram of the classical dropout method and the proposed methods. (a) Standard network. (b) Sub-network
generated by the classical dropout. (c) Nodes within each layer form sectors, and a subset of these nodes is randomly dropped at a given dropout rate p. (d) LRP relevance scores are computed for all nodes in each layer. Subsequently, a proportion of top p × 100% of the nodes in the layer are selectively dropped out, based on their LRP relevance scores.

## Methods
### Sector-wise dropout
Proposed sector-wise dropout technique, applied to a hidden layer, involves dividing the nodes in the hidden layer into several sectors. Each sector contains n nodes, where n is generally chosen so that it is a divisor of the total number of nodes, although this is not a strict requirement. With the sector-wise dropout, we randomly deactivate m nodes in each sector, ensuring that the ratio m n matches the intended dropout probability p. This method differs significantly from the classical dropout approaches. The sector-wise dropout precisely aligns the proportion of deactivated nodes in each sector with the predetermined dropout rate p, offering a more controlled approach to node deactivation.

<img width="387" alt="image" src="https://github.com/csulb-datascience/Sector-wise-and-LRP-guided/assets/44173994/65bcc6e9-7410-4bf5-8bb1-895720401216">


### LRP-guided dropout
Our research introduces a novel approach called LRP-guided dropout to enhance network training. This method leverages relevance scores from LRP to refine training. By the LRP algorithm, starting from the output and moving towards the input layer, each node is assigned a relevance score. A key feature of this method is its focus on the absolute values of these relevance scores. During back-propagation, nodes with the highest absolute relevance scores in each layer are identified and selectively disabled based on the dropout rate. This approach recognizes the equal importance of both highly positive and negative values in the affect of network behavior and performance.

<img width="366" alt="image" src="https://github.com/csulb-datascience/Sector-wise-and-LRP-guided/assets/44173994/b2ed599a-6a9e-4759-bc75-9c6684c95f23">

## Results
### Sector-wise dropout
<img width="367" alt="image" src="https://github.com/csulb-datascience/Sector-wise-and-LRP-guided/assets/44173994/cbf7a38b-61dd-4449-a355-6ea2dfde5755">

In this study, we investigate the effects of various dropout rates on neural network performance utilizing the California Housing Price (CHP) dataset, which includes 20,640 instances with 8 numeric attributes: median income in a block group, median house age in a block group, average number of rooms per household, average number of bedrooms per household, block group population, average number of household members, and block group geographical coordinates (latitude and longitude). The objective of the model is to accurately forecast the housing price, with the target variable expressed in units of hundreds of thousands of dollars.

<img width="833" alt="image" src="https://github.com/csulb-datascience/Sector-wise-and-LRP-guided/assets/44173994/3dabfff1-4c09-48ff-8923-44bb666e3047">

Comparison of training loss and validation loss as a function of dropout rate between classical dropout and Sector-wise dropout
methods. The results from our experiments illustrate that with an increase in sector size, the performance of Sector-wise dropout begins to
closely mirror that of classical dropout.


### LRP-guided dropout

This study investigates the impact of implementing LRP-guided low dropout, a methodology that involves deactivating the lowest nodes based on their absolute relevance scores.

The empirical evidence presented in Figure 5 demonstrates the effectiveness of the LRP-guided dropout method. This approach not only accelerates the early stages of learning but also establishes a more stable training regime. Notably, the training loss trajectory deviates from a monotonically decreasing pattern, exhibiting minor elevations at points where the validation loss levels off, further illustrating the stabilizing effect of this method on the training dynamics.

In the context of mitigating overfitting, the traditional dropout technique exhibits a distinct pattern characterized by an initial decrease in validation loss followed by an increase after a certain number of epochs. This trend is indicative of the onset of overfitting, as depicted in Figure 5. In contrast, the proposed method, the LRP-guided dropout, significantly diminishes this pattern. The validation loss under our method not only declines more rapidly at the beginning of training but also maintains consistently lower levels throughout the training duration, free from the characteristic increase associated with overfitting. This observation suggests that the LRP-guided dropout effectively prevents overfitting by modulating the training loss and enhancing regularization capabilities.
