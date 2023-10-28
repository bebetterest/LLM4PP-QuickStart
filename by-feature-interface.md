# By Feature Interface

In this section, we pay attention to applying **LLM4PP** by feature interface which is more flexible but more challenging than language interface. You may have to know machine learning, specially how LLMs work, including the neural structures, training optimization. Since it's beyond the scope of this article, I would like to show an easy example and my plain and shallow thoughts while ignore the implementation details.

Since a LLM is a powerful neural network, it is possible that we could include (and adjust) the network to perceive and extract the specific feature in our work/study/project. So, at first, you have to obtain the feature by designed computations or machine learning methods.

In my opinions, for feature interface, here are two keys, shape alignment and mapping alignment.  &#x20;

#### Shape Alignment

Usually, the input for a LLM are a sequence feature of vectors with a certain dimension. Considering a matrix with shape (5,1024) as the input, the length of the sequence feature is 5 and the dimension of each feature is 1024. Besides, to make use of parallel capability of GPUs for acceleration, we usually construct a batch of sequences together and get the processed results at a time. The quantity of sequences is called batch size. Thus, the final input data is in the shape of (batch\_size, sequence\_length, hidden\_dimension). Moreover, the shape of the output is the same as that of the input. In addition, LLMs usually are able to process sequences of different lengths. With a batch of sequences, those with different lengths would be processed to the same length by padding or truncation.&#x20;

Hence, shape alignment is indispensable. Otherwise we could not run the pipeline. Basically, it's not difficult to align shape since you could always reshape a matrix into any shape you like. **What is challenging is how to slice and merge to keep or even enhance the representation inside the feature.** Transformer networks usually alternately do sequence element-wise interaction and fuse feature inside each element respectively. Thus, shape alignment would influence the mapping process. The shape alignment depends on the characteristics of your specific task. For example, for an image on resolution 224, if we consider each pixel as a element, we would get a sequence of 224\*224=50176. Even if some LLMs with special methods such as position interpolation would process such a long sequence, it is not efficient at all and the fusion inside each element could not work well with few information inside a pixel. As a better way, VIT (Vision Transformer, [https://arxiv.org/pdf/2010.11929.pdf](https://arxiv.org/pdf/2010.11929.pdf)) divides the image into several patch blocks of size p. The sequence length changes to (224/p)\*(224/p) while the information of a single element is enhanced a lot. However, it more or less weakens the feature interactions between pixels inside different batch blocks.

#### Mapping Alignment

Besides, even if the generalization of LLMs is amazing, **LLMs are not the answer to life, the universe, and everything**. They are just trained for language modelling (and following instructions) while are not likely to be able to directly handle your task in a rather good performance. To **align the mapping of LLMs into specific tasks with specific data**, you may need to add/insert some transforms or train additional layers.

Let's take a close look at a case as follows.

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption><p><a href="https://arxiv.org/pdf/2309.05519.pdf">https://arxiv.org/pdf/2309.05519.pdf</a></p></figcaption></figure>

In this case, to simplify, we could consider that the proposed method NExT-GPT includes the image/audio/video task into a LLMs by feature interface. First, NExT-GPT includes a trained encoder to obtain the feature in the specific task. Second, a input/output projection is applied to achieve shape alignment for the corresponding feature. In addition, since the projections are self-adaptive by end2end optimization, mapping alignment is included.

In practical, if you do not adjust the LLM and include gradient-free mapping alignment, both APIs and open-source resources are feasible. However, when the LLM has to be adjusted or gradient descent is applied to optimize the input alignment, it is likely that APIs are not available. For mapping alignment, you may also have to make changes inside the LLM.

In short, by feature interface, you would utilize an adapted LLM to further extract obtained feature. You have to pay attention to shape alignment and mapping alignment to let the LLM process the input feature. After that, the output may be either the final result or processed by the next pipeline. You are likely to utilize open-source LLMs and libraries such as transformers for adjustments and optimizations.



#### More examples

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption><p><a href="https://arxiv.org/pdf/2304.10592.pdf">https://arxiv.org/pdf/2304.10592.pdf</a></p></figcaption></figure>

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption><p><a href="https://arxiv.org/pdf/2309.16058.pdf">https://arxiv.org/pdf/2309.16058.pdf</a></p></figcaption></figure>



## to be continue
