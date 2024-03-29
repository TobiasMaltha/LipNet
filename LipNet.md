# LipNet
## Introduction
LipNet is a neural network architecture for lipreading, it differs from earlier research within the field, because it maps whole sentences instead of detecting individual words or phoneme’s classification [1] (“A phoneme is the smallest unit of sound in a word that makes a difference in its pronunciation, as well as its meaning, from another word”[2]). When done by humans lipreading is a difficult practice, this is due to fact that most of the movement besides that of the lips, tongue and teeth are latent and it can be difficult to interpret the words without the context of the sentence. In the perspective of machine lipreading the task is challenging, because it must factor in both the position and the motion of the mouth as features from a video input. Despite of these challenges LipNet has showed promising results regarding lipreading [1].

## Data and preprocessing
LipNet is trained on the GRID corpus dataset, this consists of 34 persons who each narrates 1000 sentences. However, there are some missing and corrupt videos which results in 28775 videos, that are used for the training of LipNet. The dataset is based on a specific sentence structure, which is: “command(4) + color(4) + preposition(4) + letter(25) + digit(10) + adverb(4); where the number denotes how many word choices there are for each of the 6 word categories” resulting in a sentence such as “place red at C zero again” [1]. 

They augment the dataset with some simple transformation to reduce overfitting. This is done by training the model on the regular data, horizontally mirrored images, and the videos duplicated at various speeds [1]. 

## Architecture
The architecture of the LipNet consist of many different layers, the first layer is the input of the data, which are frames that changes over time. The next layer is three STCNN layers which includes a pooling layer at each STCNN. This leads to a two layered Bidirectional GRU and their outputs are processed by a linear layer and a SoftMax that determines the words/sentences. The model is trained with CTC loss [1].

STCNN stands for Spatiotemporal Convolutions Neural Network, which is a type of CNN. The CNN is used for analyzing the frame, however to capture all the frames in the videos, the spatiotemporal is used. Spatiotemporal works by processing many frames over time and by convolving across time [1].

The spatial pooling layer functions as a normal pooling layer, however it is flexible towards small shifts in the frames, like a moving mouth. The pooling layer is used as a way of preserving the features in the frames while getting different perspectives. Pooling also helps with preventing overfitting [1][3]. 

The Bi-GRU is an RNN which holds onto data, while selecting which data goes to the output of the Bi-GRU layer. Furthermore, by being bidirectional it looks through the data in different ways [1].

Linear layers can learn the average rate of correlation between the input and the output. At the end of it is a softmax [4][1].

The compiling of the model has been done with Connectionist Temporal Classification (CTC) loss. A rough explanation would be that it computes the probability of a specific sequence by looking at all the sequences that is defined as the specific sentence [1].


![alt text](https://github.com/TobiasMaltha/LipNet/blob/master/arch.PNG "LipNet Arhitecture")



## Visualization of LipNet
The following is a visualization of LipNet’s learned behavior in relation to the pronunciation of the word “lay”. Here the first 6 pictures shows the tongue coming into contact with the alveolar ridge (“a small protuberance just behind the upper front teeth” [6]). Frames 7-9 depicts the tongue coming down again, and this is what LipNet seems to be focusing on [1]. 

![alt text](https://github.com/TobiasMaltha/LipNet/blob/master/lay.PNG "Visualization of the word Lay")

## Results
The table below shows existing lipreading methods, datasets and accuracy. As earlier explained LipNet is the first method with sentences as an output, compared to earlier methods which often only predict isolated words. Furthermore, LipNet reaches a state of the art accuracy of 95.2% were previous single word prediction at the GRID dataset by Gergen et al. 2016 only reached 86.4% accuracy [1].

![alt text](https://github.com/TobiasMaltha/LipNet/blob/master/result.PNG "Results")


Compared to hearing-impaired humans on the same dataset, LipNet performs 1.69 times better with an accuracy of 88.6% opposite the 52.3% of hearing-impaired, when using unseen speakers/subjects. Whereas LipNet obtains a 95.2% sentence-level word accuracy with overlapped speakers [1].

## Critics
The results of LipNet has been accused of being exaggerated, because of the limited GRID dataset that is used for training. The criticism of the dataset is based on how it is constructed of a limited amount of words, a fixed structure, with short sequences of only three seconds, and this results in sentences that are far from everyday speech [5].

Some have suggested that there would be no more secrets due to LipNet, hinting that it can be used for surveillance. However, the authors behind LipNet have clearly stated that they have no interest in the world of surveillance, since lipreading would require to clearly see the subjects tongue, meaning that the video needs to be straight on, well-lit and at the correct frame rate, making it hard to obtain satisfying data. However, if these requirements were to be fulfilled with a quality camera, the camera would also often have a microphone equipped, that could be used for voice recognition instead [5].

## Usage and applications
Despite the criticisms the authors believe that LipNet could be used on more advanced datasets [5]. Moreover, the authors imagine that LipNet can be used in applications such as improving hearing aids, silently dictating and as an alternative to speech recognition in noisy environments [1][5]. The last suggestions can be seen in this YouTube video:  


<a href="http://www.youtube.com/watch?feature=player_embedded&v=YTkqA189pzQ
" target="_blank"><img src="http://img.youtube.com/vi/YTkqA189pzQ/0.jpg" 
alt="IMAGE" /></a>

## References: 
[1] LIPNET: END-TO-ENDSENTENCE-LEVELLIPREADING (https://arxiv.org/pdf/1611.01599.pdf)

[2] https://literarydevices.net/phoneme/ 

[3] https://www.quora.com/What-is-spatial-pooling-in-computer-vision

[4] https://medium.com/datathings/linear-layers-explained-in-a-simple-way-2319a9c2d1aa

[5] https://www.theverge.com/2016/11/7/13551210/ai-deep-learning-lip-reading-accuracy-oxford

[6] https://www.britannica.com/science/phonetics#ref583946 
 

