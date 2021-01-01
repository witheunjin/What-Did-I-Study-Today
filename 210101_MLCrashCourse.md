# ML Crash Course 

provided by Google Developers Page 👉 [Here is the Link](https://developers.google.com/machine-learning/crash-course)

Date : Jan 1st, 2021 (🎉Happy New Year🎉)

### Today's Crashing

1. Introduce to ML

2. Framing

------

## 🌻Framing🌻

### 1. What will be dealt with this course

- How to Frame a task as a ML problem
- Many of the basic vocabulary terms shared across a wide range of ML methods

-----------

### 2. What is (Supervised) ML?

ML systems learn(or create models)

​	how to combine input

​		to produce useful predictions

​			on never-before-seen data

------------

### 3. Terminology

#### 🌴Label🌴

- Label is *the variable we're predicting*
- It represented by the variable `y`
- When training models, the label is provided
- For example, in e-mail, `spam` or not(`not spam`) can be the label 

-------

#### 🌴Features🌴

- Features are *input variables describing the data*

- It represented by the variables `{x1, x2, x3, ... , xn}`

- For example, in e-mail, to/from address or other information of the mail can be the features

  > Features in spam detector example
  >
  > - words in the email text
  > - sender's address
  > - time of day the email was sent
  > - email contains the phrase "one weird trick."

------

#### 🌴Example🌴

- Example is *a particular instance of data, x*

- A piece of data

- One e-mail can be an example

  ##### 🌱 **Labeled Example vs Unlabeled Example**

  [More Specified Description with examples_google developer page](https://developers.google.com/machine-learning/crash-course/framing/ml-terminology#examples)

   1. Labeled Example

      - It has {features, label} = (x,y)

      - It used to train the model
      - For example, e-mail which can be distinguished whether it is a spam mail or not

  2. Unlabeled Example

     - It has {features, ?} = (x, ?)
     - no labels
     - It used for making predictions on new data

-----

#### 🌴Model🌴

- It defines the relationship btw features and label.

- It maps examples to predicted labels : `y'`

- It defined by internal parameters, which are learned.

  ##### 🌱 Training

  - It means *Creating or Learning the model.*

  ##### 🌱 Inference

  - It means *Applying the trained model to unlabeled examples.*

  ##### 🌱 Regression Model vs Classification Model

  1. Regression Model

     - It predicts **continuous** values.

       > Examples
       >
       > - What is the value of a house in Cali?
       > - What is the probability that a user will click on this ad?

  2. Classification Model

     - It predicts **discreate** values.

       >  Examples
       >
       > - Is a given email msg spam or not spam?
       > - It this an Image of a dog, a cat, or a cheetah?


