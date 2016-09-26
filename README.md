# tf-lstm-char-cnn

Tensorflow port of Yoon Kim's [Torch7 code](https://github.com/yoonkim/lstm-char-cnn). See also similar project [here](https://github.com/carpedm20/lstm-char-cnn-tensorflow) that failed to reproduce Kim's results and was apparently abandoned by the author. Many pieces of code are borrowed from it.

## Installation
You need tensorflow version 0.10 and python (obviously).

## Running

```sh
python train.py -h
python evaluate.py -h
```

## Training

```sh
python train.py
```
will train large model from Yoon Kim's paper.

## Evaluate

```sh
python evaluate.py --load_model cv/epoch024_4.4962.model
```
evaluates this model on the test dataset

## Generate

```sh
python generate.py --load_model cv/epoch024_4.4962.model
```
generates random text from the loaded model

## Model

![model](https://cloud.githubusercontent.com/assets/14280777/17991383/13990c56-6b0c-11e6-8a9f-f4de07a6984f.png)

`Model_1` graph is used for inference (computing validation loss and perplexity during training)

`Model` graph is used for training.

## Experiments

### Learning rate 1.0 (default)

![image](https://cloud.githubusercontent.com/assets/14280777/18585742/bd288cd4-7be6-11e6-82fd-d0d4acf727c1.png)

### Learning rate 0.5

![image](https://cloud.githubusercontent.com/assets/14280777/18585850/6d207c6e-7be7-11e6-80a2-b48185d76b2c.png)

### Learning rate 0.25

![image](https://cloud.githubusercontent.com/assets/14280777/18585916/d9520d58-7be7-11e6-80df-3d400ae11325.png)

(training was cancelled after 20 epochs, when learning rate started to collapse)

### Results

| Learning rate  |  Train/Valid/Test loss  |  Train/Valid/Test perplexity  |
|:--------------:|:-----------------------:|:------------------------------|
| 1.0            | 4.036 / 4.496 / 4.459   | 56.58 / 89.68 / 86.37         |
| 0.5            | 4.015 / 4.436 / 4.397   | 55.42 / 84.40 / **81.23**     |
| 0.25           | 4.242 / 4.495 / 4.463   | 69.57 / 89.50 / 86.73         |

Note that model **DOES NOT** reproduce the published result. Original Torch7 code does get to perplexity of 79 with learning rate 1.0.
This code gets to 86 with the same parameters. Tweaking learning rate gets us to perplexity 81. Maybe more parameter search will make furhter improvement?

Reason for the TF failing to reproduce the original result is not clear. The only differences between this model and model of Yoon Kim are:

* TF uses float32, while Torch uses float64
* Parameter initialization is (randomly) different

## Generating random text
```
recorder $ N years ago to meet all kinds of london 's fledgling preclude

machine tool tool exterior buying its debut + but the legitimacy of the company still be complained + but they take advantage of the government banks + since expected to make of the state police gear + the

from the nation 's

from N N N miles of letters of quantum 's resilience in washington

as a new york has been

which had an analyst + by mounting the key + mazda 's

in

every

for the region headed by japanese companies from the hastily would belong to be filled with magna 's definitely identified financing for minnesota 's current expansion + as many of all of

a reduction in a lot of the opposite with a remarkable buy-outs from

air chips maxicare and deprived a head of america for example of

by a third parties notified earlier this year 's

with

+

treatment of the uninsured by

+ but over the diversion to own to test and a

+ mcdonald 's decision to be

and the unique assets will the

for this year forecast predicts to provide a

management and the amount of market stability of soviet consumer metal markets + ralston international financial institutions are

+ that it 's

in private

with the tramp and other

+ in the culmination of newsweek became

in a blueprint and

successful stock bond corp. 's

to solve petroleum co. rebel and confusion program trading for instance of limits on

of N commissioned in the greater than N miles of the national year earlier this picture 
```
