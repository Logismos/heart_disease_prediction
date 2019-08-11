# Introduction
* This is my final project for our class, Intro to data science algorithms. 
* And we are tasked with selecting a multivariate analysis problem, applying various data science algorithms and tools, to
include those learned in this class, and performing regression and/or classification.
* In light of this, I chose a heart disease classification problem.
* This notebook contains, in sequential order, a walk through of my project.
* I will be giving a summary of it through this video.
* I will try to keep it at a high level, and will gloss over some of the tedious steps

# Heart Disease
* Why did I choose to predict heart disease?
* Heart disease is the number one killer in the world. 
* I also have a personal interest in biomedical applications of machine learning. My professional goal is to work in the
  intersection of the two fields.
# Data Source
* The dataset I used, which was obtained from Kaggle, and it appears to have been orginally hosted on the UCF machine
  learning repository, is a conglomeration of 4 different heart disease datasets.
* Each dataset has information on patients, which appear to have been admitted to a hospital due to chest pain.
* These patients conducted clinically induced exercise, and were subsequently subjected to a medical imaging technique
  called angiography. 
* Angiography is an xray imaging technique which looks at the heart's blood vessels. 
* They also conducted several more measurements, such as an electrocardiogram, and each patient is labeled as having
  heart disease or not
* This is a video of angiography

# Goals
* I have little knowledge in these variables, so I will not hypothesize on anything. 
* What I will do though is conduct a little background investigation on each variable, as well as performing statistical
  tests on each variable
* I will also try to develop a model which is superior to those from other kaggle kernels. 

# EDA
* This section is on EDA
## Quick look
* First we load the data and give a quick look at its contents
* We see that there are 1025 patients, and 14 variables, to include the target variable
* And looking at the number of unique values for each variable, we see that most of them are categorical
## Preprocessing
* The categorical variables are transformed into several dummy variables, taking the values of 0 or 1
* Then renaming the variables to something more descriptive
## Variable Exploration
* Now to explore each variable
* Starting with a cross-correlation map to give us a high level look of how each variable is related to each other
* This contains a lot of information, and we can look at just how each variable compares to heart disease
* Now we see that there are some variables, like Thalasemmia Fixed Defect that have a high correlation, and some that
  have a low correlation, like fasting blood sugar levels
* Now a Pairplot of continuous variables, we see that there appears to be a degree of separation between the two
  classes, heart disease present and not present, in even as low as two dimensions
### Sex
* Now to look at each variable type individually
* Looking at sex, it appears that females are more likely to have heart disease, which is strange, as it does not agree
  with statistics concerning the total population
### Age
* A similar conflicting finding also appears with age, which shows that younger people are more likely to have heart
  disease.
* This is a plot from heart.org showing how it conflicts with the findings concerning age and sex.
### Resting blood pressure
* Resting blood pressure seems to be about the same within the two classes
### Cholesterol
* Same with cholesterol, except for some high outliers in the heart disease class
### Fasting Blood Sugar
* Blood sugar does not seem to correlate with heart disease
### Maximum Heart Rate Achieved during exercise
* For maximum heart rate achieved during exercise, it appears that those with heart disease were likely to have a higher
  value
### Exercise Induced Angina
* Angina is a type of chest pain caused by reduced blood flow to the heart
* It appears that those that did not experience exercise induced angina were more likely to have heart disease, which
  seems somewhat counterintuitive
### ST Depression
* ST Depression is the depression of the ST segment in an ECG signal
* Those with heart disease were not likely to have exercise induced ST depression
### Number of major blood vessels
* Angiography reveals the blood vessels that do not have restricted blood flow
* Those with less major blood vessels had a higher chance of having heart disease, which seems intuitive
### Chest Pain
* The chest pain variable is categorical, and it can be eithertypical angina, which appears to be what's called stable
  angina, and occurs as the result of hard exercise or stress, then atypical angina, which occurs while resting, and is
  not good, non-anginal is any chest pain that is not anginal, and there is asymptomatic, which is chest pain without
  symptoms.
* Those with typical anginal chest pain were less likely to have heart disease, and the other types were more likely to
  occur in those with heart disease
### Resting Electrocardiogram
* Electrocardiogram, or ECG for short, is a measurement of the electrical activity of the heart, and a single heart beat
  can be segmented into different intervals
* This variable concerns an ECG taken at rest, and can be either a normal ECG, ST-T wave abnormality, which is an
  abnormality in the ST and T portions, and Left Ventricular hypertrophy, which is an increase in the QRS complex (which
  is the peak of the signal)
* People without heart disease were slightly more likely to have a normal ECG, and people with heart disease were
  slightly more likely to have an ST-T wave abnormality
* Left ventricular hypertrophy does not seem to play a part
### Slope of the ST segment during peak exercise
* This variable concerns the slope of the ST segment of the ECG signal
* Can be up-sloping, down-sloping, or flat (horizontal)
* Down-sloping appears to be correlated with heart disease, and flat slope appears to be correlated with not having
  heart disease. Up-sloping appears to be slightly correlated with not having heart disease.
### Thalasemmia
* Thalasemmia is a blood disorder which affects hemoglobin
* This variable can be Normal, a fixed defect, which appears to be a irreversable defect, and a reversable defect
* Those with a Reversable Defect appear to not have heart disease, and those with a fixed defect appear to have a higher
  likelihood of having heart disease
* Those that don't have Thalasemmia were less likely to have heart disease

# Classification
* The next sections concerns classification of heart disease
* Besides creating and evaluating several classifiers, it also delves into feature importance and hyperparameter
  optimization
## Load data
* Create our feature matrix and target vector
* I opted to remove age and sex from the set of features. I wanted to remove any doubts caused by the datasets difference from total population trends
## Preprocessing
* Split into train and test sets, and perform normalization. 
* Because many variables are bernoulli, or taking on the values of 0 or 1, we set the maximum value to 1 and the minimum
  to 0 for all variables

## Exercise in Building Classifieres
* For this project, I opted to write the code for the various classifiers instead of using sklearn. 
* I used ..
* I took the sklearn template, and wrote them based on information from the ESL and the various lectures

## Evaluation
* I also used kFold Cross-Validation as the evaluation method
* Seeing how each model performs with kFold CV on the entire dataset, later I will keep the train and test sets separate
* We see that the kNN and weighting neighbors by distance is the best model by far

## Feature Importance
* For feature importance I used two methods
* I used the step forward algorithm as mentioned in class, and I used a random forest method
### Step forward
* For the step forward method, I used NB as the classifier because it was the best model that doesn't have
  hyperparameters 
* I compared it with how large each variable is correlated with heart disease
* It seems that Thalasemmia Fixed Defect is the most important feature here, followed by ST depression and number of
  major blood vessels
### Random Forest Method
* The sklearn RF model stores the feature importances after fitting on the training set
* ...
### Hyperparameter
