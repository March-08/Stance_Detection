<!--
*** Thanks for checking out this README Template. If you have a suggestion that would
*** make this better, please fork the repo and create a pull request or simply open
*** an issue with the tag "enhancement".
*** Thanks again! Now go create something AMAZING! :D
-->





<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->




<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://github.com/othneildrew/Best-README-Template">
    <img src="https://github.com/March-08/Stance_Detetion/blob/master/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">Stance Detection</h3>

  <p align="center">
    A Bert based model for stance detection
    <br />
    <a href="https://github.com/othneildrew/Best-README-Template"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/othneildrew/Best-README-Template">View Demo</a>
    ·
    <a href="https://github.com/othneildrew/Best-README-Template/issues">Report Bug</a>
    ·
    <a href="https://github.com/othneildrew/Best-README-Template/issues">Request Feature</a>
  </p>
</p>



<!-- TABLE OF CONTENTS -->
## Table of Contents

* [About the Project](#about-the-project)
  * [Built With](#built-with)
* [Getting Started](#getting-started)
  * [Prerequisites](#prerequisites)
  * [Installation](#installation)
* [Usage](#usage)
* [Roadmap](#roadmap)
* [Contributing](#contributing)
* [License](#license)
* [Contact](#contact)
* [Acknowledgements](#acknowledgements)

## Abstact

**English**. This  paper  describes  the  UNI-TOR system that participated to the StanceDetection  in  Italian  tweets  (Sardistance)task  within  the  context  of  EvalIta  2020.UNITOR implements a transformer-basedarchitecture  whose  accuracy  is  improvedby  adopting  a  Transfer  Learning  tech-nique. In particular, this work investigatesthe  possible  contribution  of  three  auxil-iary tasks related to Stance Detection, i.e.,Sentiment Detection, Hate Speech Detec-tion and Irony Detection.  Moreover, UN-ITOR relies on an additional dataset auto-matically downloaded and labeled throughdistant  supervision.    The  UNITOR  sys-tem ranked first in the competition.  Thisconfirms the effectiveness of Transformer-based architectures and the beneficial im-pact of the adopted strategies.

**Italiano** .Questo  lavoro  descrive  UNI-TOR  il  sistema  che  ha  partecipato  alloStance Detection in Italian tweet (SardiS-tance)   task,   nell’ambito   della   compe-tizione  Evalita  2020.UNITOR  imple-menta  un’architettura  neurale  basata  suTransformer,   la   cui   accuratezza   vienemigliorata   adottando   una   tecnica   diTransfer  Learning.    In  particolare,  ven-gono  aggiunti  tre  auxialiary  taks  rela-tivi  ai  task  di  Sentiment  Detection,  HateSpeech Detection e Irony Detection..   In-oltre,  l’addestramento  di  UNITOR  con-sidera  un  insieme  di  dati  aggiuntivi  chesono  scaricati  ed  etichettati  automatica-mente attraverso la tecnica di Distant Su-pervision.   Il  sistema  si  é  classificato  alprimo  posto  nella  competizione,  confer-mando l’efficacia delle architetture basatesu Transformer e il contributo delle strategie adottate.

## Introduction
Stance detection aims at detecting if the author ofa text is in favor of a target topic, or against it (Kre-jzl et al., 2017). In this task, a text pair is generallyconsidered: one text expresses the topic, while theother reflects the author’s judgments.  In a possi-ble variant to such a setting, the topic is implicitwithin an entire document collection over whichthe stance detection is applied.In this work, we will consider this last setting,as defined in the in the Stance Detection in Ital-ian Tweets (SardiStance) task ((Cignarella et al.,2020))  within  the  Evalita  2020  evaluation  cam-paign.   A  set  of  texts  (here  tweets)  is  provided,almost all concerning the same topic, i.e., the Sar-dines Movement1. The goal is to recognize if eachtweet is for or against (or neither) such topic, onlyexploiting textual information.  According to thetask  definition,  this  corresponds  to  the  so-calledTask A. This is quite challenging problem, sinceit  requires  at  the  same  time  to  discover  if  a  textrefers to the target topic and the author’s orienta-tion, only relying on short messages written in avery conversational style.We  present  the  UNITOR  system  participatingto  the  SardiStance  task.The  system  is  basedon a Transformer-based architecture for text clas-sification  (Devlin  et  al.,  2019)  that  is  directlypre-trained over a large-scale document collectionwritten  in  Italian,  namely  UmBERTo.   In  a  nut-shell,  the  adopted  architecture,  which  has  beendemonstrated achieving state-of-the-art results inmany NLP tasks (Devlin et al., 2019) takes in in-put a message and associates it to one of the targetclasses,  which in turn express if the author is in Favourto the Movement, isAgainstit or neu-tral, as represented byNoneclass.Moreover,  due  to  the  task  complexity  and  thesmall size of the dataset, in order to improve thegeneralization capabilities of the neural network,we adopted a Transfer Learning approach (Pan andYang, 2010).  Our main assumption is that StanceDetection is tied to other tasks involving EmotionRecognition (such as Sentiment Analysis or IronyDetection) even though important differences doexist  among  them.   As  a  simplified  example,  letus consider a message such as “I like the SardinesMovement”:   it  clearly  expresses  a  positive  sen-timent,  also  being  in  favour  of  the  target  topic.However,  a  message  such  as  “I  like  the  EvalItacampaign.”  is positive as well but it does not ex-press  any  support  or  opposition  to  the  Sardines.As a consequence, it should be associated to theNoneclass.  We thus speculate that an automaticsystem trained over an auxiliary task (such as Sen-timent Classification) is beneficial, but the trans-fer process must be carefully designed in order toavoid catastrophic forgetting or catastrophic inter-ference problems (Mccloskey and Cohen, 1989).In this work, we investigate the possible contri-bution of three auxiliary tasks involving the recog-nition of emotions according to different settings,i.e., Sentiment Detection and Classification, HateSpeech Detection and Irony Detection.  We adoptthree  different  classifiers  (one  for  each  auxiliarytask) and use them to add additional information tothe tweets provided in the SardiStance dataset. Asan example,  when considering the auxiliary taskinvolving Hate Detection, the corresponding clas-sifier will augment each input tweet by expressingif this expresses hate or not.  After this step,  thefinal classifier is expected to learn the associationbetween messages and the stance categories, “be-ing aware” (with some unavoidable noise) if themessage  expresses  some  sort  of  hate,  irony  andmore generally, sentiment. Finally, we investigatethe  possibility  of  augmenting  the  training  mate-rial by automatically downloading messages andlabeling them through distant supervision (Go etal., 2009).  We first selected few hashtags clearlyin favour (or not) of the target topic to downloadand label a set of set of messages.  Then, in orderto add a set of neutral messages, we selected a setof news titles concerning the Sardines Movement.The UNITOR system ranked first in the com-petition,   suggesting   that   the   combination   of the Transformer-based learning with the adoptedstrategies of Transfer Learning and Data Augmen-tation is beneficial.In the rest of the paper, Section 2 describes theadopted  Tranformers-based  architecture  and  theunderlying our transfer learning approach. In Sec-tion 3, the performance measures of the system arereported while Section 4 derives the conclusions.
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<!-- ABOUT THE PROJECT -->
## About The Project


This project was developed for the [Web Mining and Retrivial class (CS)](http://ai-nlp.info.uniroma2.it/basili/didattica/WmIR_18_19/) at the [University of Tor Vergata](http://www.informatica.uniroma2.it/).<br/>
Under the supervision of **prof. Roberto Basili** and **prof. Danilo Croce**, we were able to develop a Stance Detection Classifier based on Bert model, that was released by Google, and that was published for the firt time in the following paper ["BERT: Pre-training of Deep Bidirectional Transformers for
Language Understanding"](https://arxiv.org/pdf/1810.04805.pdf)

While working on this project we took the opportunity to partecipate to the [EVALITA 2020](http://www.evalita.it/) competition.
EVALITA is a periodic evaluation campaign of Natural Language Processing (NLP) and speech tools for the Italian language, born in 2007.
This year EVALITA provided a task called [SardiStance](http://www.di.unito.it/~tutreeb/sardistance-evalita2020/index.html), that is basically a stance detection task, using a data-set containing Italian tweets about the [Sardines Movement](https://en.wikipedia.org/wiki/Sardines_movement).

### Task Description
The task is a three-class classification task where the system has to predict whether a tweet is in favour, against or neutral/none towards the given target, exploiting only textual information, i.e. the text of the tweet.
The dataset will include short documents taken from Twitter.
The evaluation will be performed according to the standard metrics known in literature (accuracy, precision, recall and F1-score)



### Built With
* [Google Colab](https://colab.research.google.com/github/tensorflow/examples/blob/master/courses/udacity_intro_to_tensorflow_for_deep_learning/l01c01_introduction_to_colab_and_python.ipynb)
* [PyTorch](https://pytorch.org/)

## Our Strategy

The main issue facing this task was that the dataset provided was very poor, it consisted in of 3,242 instances, in fact simply by using UmBERTo we obtained a low accuracy, about 56%.
**UmBERTo** is an Italian Language Model thatinherits from RoBERTa base model architecture which improves the initial BERT.
So we thought to train UmBERTO on differents but similiars tasks, and to use the resulting model to tag the tweets of our original dataset.
In this way each tag could give a hint about the sentence it was associated with.
The tasks we used for this purpose are:
- sentiment analysis
- hate speech detection
- irony detection

### Sentiment Analysis
The task consists in automatically annotating messages from the popular microblogging platform Twitter1 with a tuple of boolean values indicating the message’s subjectivity and polarity (positive or negative).
We used the dataset provided by EVALITA for the [SENTIPOLC](http://www.evalita.it/2016/tasks/sentipolc) challenge.
We trained our model with the sentipolc dataset, and we obtained an accuracy of, NUMERO%.
In this way we could tag with [PRO] [CONTRO] every sentence of the SardiStance dataset, using the model obtained from the sentiment task.
At the end, we processed our new dataset (cointaining the new tag for each tweet), and we observed that the mean accuracy over 10 cross folder validation improved from the first simple Bert model, we obtained an mean accuracy of NUMERO%, with a standard deviation of NUMERO%.


### Hate Speech Detection
This is a binary classification task aimed at determining whether the message contains Hate Speech or not
We used the dataset provided by EVALITA for the [HATE SPEECH](http://www.di.unito.it/~tutreeb/haspeede-evalita18/index.html) challenge.
We trained our model with the hate speech dataset, and we obtained an accuracy of, NUMERO%.
In this way we could tag with [ODIO] [NON ODIO] every sentence of the SardiStance dataset, using the model obtained from the hate speech detection task.
At the end, we processed our new dataset (cointaining the new tag for each tweet), and we observed that the mean accuracy over 10 cross folder validation improved from the first simple Bert model, we obtained an mean accuracy of NUMERO%, with a standard deviation of NUMERO%.


### Irony Detection
This is a classification task where the system has to predict whether a tweet is ironic or not, so given a message, decide whether the message is ironic or not.
We used the dataset provided by EVALITA for the [IronITA ](http://www.di.unito.it/~tutreeb/ironita-evalita18/index.html) challenge.
We trained our model with the hate IronITA dataset, and we obtained an accuracy of, NUMERO%.
In this way we could tag with [IRONICO] [NON IRONICO] every sentence of the SardiStance dataset, using the model obtained from the hate speech detection task.
At the end, we processed our new dataset (cointaining the new tag for each tweet), and we observed that the mean accuracy over 10 cross folder validation improved from the first simple Bert model, we obtained an mean accuracy of NUMERO%, with a standard deviation of NUMERO%.

### Our choice
We tried to use also multiple tags for each sentence, for example differents combinations of the tags derived from the tasks desribed above.
The results are all stored in the following table.
INSERIRE LA TABELLA
As we can see the most accurate run, is the the one that uses a combination of HATE TAG and SENTIMENT TAG !!!!!!!!!!!!!!!!!!!!! CORRREGGi


### Majority Voting
Ensemble methods are techniques that create multiple models and then combine them to produce improved results. Ensemble methods usually produces more accurate solutions than a single model would. 
Using the majority voting every model makes a prediction (votes) for each test instance and the final output prediction is the one that receives more than half of the votes. If none of the predictions get more than half of the votes, we may say that the ensemble method could not make a stable prediction for this instance. Although this is a widely used technique, you may try the most voted prediction (even if that is less than half of the votes) as the final prediction. In some articles, you may see this method being called “plurality voting”.
Using the majority voting we obtained an accuracy of NUMERO%.





<!-- ROADMAP -->
## Roadmap

The creation of the final model used for the EVALITA competition has seen many changes over time, we would like to explain here every strategies that we used in order to modify the simple Bert model provided by Google, and how we obtained the best classifier for this stance detection task.
We will report also in a table all the measures that we obtained using the various models that we delevoped during tests.

##£ Measures Reports

<img src="https://github.com/March-08/Stance_Detetion/blob/master/Cattura.PNG"/>





### SVM Baseline
A baseline is a method that uses heuristics, simple summary statistics, randomness, or machine learning to create predictions for a dataset. You can use these predictions to measure the baseline's performance (e.g., accuracy)-- this metric will then become what you compare any other machine learning algorithm against.
We used a simply Support Vector Machine as baseline in order to compare our more sophisticated models with this one.
As you can see in the table above we obtained an accuracy of 47.77%




<!-- GETTING STARTED -->
## Getting Started

This is an example of how you may give instructions on setting up your project locally.
To get a local copy up and running follow these simple example steps.

### Prerequisites

This is an example of how to list things you need to use the software and how to install them.
* npm
```sh
npm install npm@latest -g
```

### Installation

1. Get a free API Key at [https://example.com](https://example.com)
2. Clone the repo
```sh
git clone https://github.com/your_username_/Project-Name.git
```
3. Install NPM packages
```sh
npm install
```
4. Enter your API in `config.js`
```JS
const API_KEY = 'ENTER YOUR API';
```



<!-- USAGE EXAMPLES -->
## Usage

Use this space to show useful examples of how a project can be used. Additional screenshots, code examples and demos work well in this space. You may also link to more resources.

_For more examples, please refer to the [Documentation](https://example.com)_




<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request



<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE` for more information.



<!-- CONTACT -->
## Contact

Your Name - [@your_twitter](https://twitter.com/your_username) - email@example.com

Project Link: [https://github.com/your_username/repo_name](https://github.com/your_username/repo_name)



<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements
* [GitHub Emoji Cheat Sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet)
* [Img Shields](https://shields.io)
* [Choose an Open Source License](https://choosealicense.com)
* [GitHub Pages](https://pages.github.com)
* [Animate.css](https://daneden.github.io/animate.css)
* [Loaders.css](https://connoratherton.com/loaders)
* [Slick Carousel](https://kenwheeler.github.io/slick)
* [Smooth Scroll](https://github.com/cferdinandi/smooth-scroll)
* [Sticky Kit](http://leafo.net/sticky-kit)
* [JVectorMap](http://jvectormap.com)
* [Font Awesome](https://fontawesome.com)





<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/othneildrew/Best-README-Template.svg?style=flat-square
[contributors-url]: https://github.com/othneildrew/Best-README-Template/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/othneildrew/Best-README-Template.svg?style=flat-square
[forks-url]: https://github.com/othneildrew/Best-README-Template/network/members
[stars-shield]: https://img.shields.io/github/stars/othneildrew/Best-README-Template.svg?style=flat-square
[stars-url]: https://github.com/othneildrew/Best-README-Template/stargazers
[issues-shield]: https://img.shields.io/github/issues/othneildrew/Best-README-Template.svg?style=flat-square
[issues-url]: https://github.com/othneildrew/Best-README-Template/issues
[license-shield]: https://img.shields.io/github/license/othneildrew/Best-README-Template.svg?style=flat-square
[license-url]: https://github.com/othneildrew/Best-README-Template/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=flat-square&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/othneildrew
[product-screenshot]: images/screenshot.png
