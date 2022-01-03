# NLPproject

# Data

Students write an essay outlining their approach to solving a physics problem. The answer correctness is used as a label 0 (incorrect) and 1 (correct)
Note: hand grading of each essay by domain experts is in progress. Training and testing sets are composed of essays from all of the students in the class (N \approx 1500)
for two consecutive spring semesters. A validation split is taken from the training set as the goal is to produce in-situ predictions

# Data Preparation

Each essay is:

<ul>
  <li> Stripped of unnecessary characters </li> 
      <ul>
        <li> Equations (which are noise) </li>
        <li> Punctuation </li>
        <li> html mark up </li>
      </ul>     
  <li> Stripped of stop words </li>
  <li> Spell corrected with TextBlob </li>
</ul>

# Prediction

For the prediction, the bert model is used as implemented in the simple transfomers library. The simple transformers implementation of bert allows the use of WandB for
parameter tuning.

A split of the training set was used for validation/parameter tuning. Then the trained model was used to predict the entire testing set. Since the goal is to detect 
faultly logic, the relevant metric is recall (provided precision doesn't fall too far out of range). In other words, we are willing to tolerate some reasonable number
of false positive errors (students who would have gotten the problem correct are told to think twice about their approach) to minimize false negative errors
