# KD_ArapUbi
A novel approach for the prediction of Arabidopsis thaliana ubiquitination sites based on knowledge distillation and natural language processing

Protein ubiquitination is an important post-translational modification (PTMs), which is involved in diverse biological processes and plays an essential role in the regulation of physiological mechanisms and diseases. Numerous efforts have resulted in the development of various prediction tools for ubiquitination sites across all species. These tools primarily depend on predefined sequence features and machine learning algorithms. However, the variations in ubiquitination patterns among these species remain unclear. In this study, we propose a novel approach for predicting Arabidopsis thaliana ubiquitination sites by building a model based on knowledge distillation in a neural network and natural language protein features. The ‘Teacher-model’ is larger, trained on larger and multi-species; whereas, the ‘Student-model” is smaller, trained on one specific species. As a natural, with its advantage, the ‘Teacher-model’ will be able to simultaneously guide the ‘Student model’ (target model) through pseudo-labels, aiding the proposed model to learn knowledge from teachers - individuals with deep expertise, thereby generating more robust predictions. Evaluation by cross-validation demonstrate that our proposed model obtains the highest performance, reaching the accuracy at 86.3% and AUC value at 0.926. Fortunately, evaluation by independent testing, our proposed model is exhibited that it also achieves the highest performance with accuracy at 86.3% and AUC value of 0.923. In addition, to examine the ability of our proposed model, we have conducted a comparison with several well-known existing predictors for Arabidopsis thaliana ubiquitination. The comparison results also indicate that our proposed model exhibits significantly superior performance in predicting Arabidopsis thaliana ubiquitination compared to other methods. This result suggests that the model that is constructed based on Knowledge distillation and natural language processing would brings high efficiency. Hopefully, these results will be a promising approach and helpful for researchers in their related studies.
Herein, we provide the KD_ArapUbi project to support scientists for their relative works in the identification of protein Arabidopsis thaliana ubiquitination sites.

# Dependencies 
-	Google Colab.
-	Library: Keras, Tensorflow, Sklearn
-	Input: format: .csv ; windowsize: 31
# Prediction: step-by-step as followings:
-**	Step 1: Data collection and pre-processing**
-	**Step 2: Extract fragments using window size of 31**
-	**Step 3: Removing redundant and homologous data using CD-HIT **
-	**Step 4: Word separating using 1-gram …**

def ProSentence(pro, K):
  sentence = ""
  length = len(pro)
  for i in range(length - K + 1):
    sentence += pro[i: i + K] + " "
    #delete extra space
  sentence = sentence[0 : len(sentence) - 1]
  return sentence

#define 1-gram dictionary for protein 1_gram include 20 amino acid ('A', 'C', #'D', 'E', 'F', 'G', 'H', 'I', 'K', 'L', 'M', 'N', 'P', 'Q', 'R', 'S', 'T', 'V', 'W', 'Y'), 'X' representing missing amino #acids.

def twoTupleDic1():
AA_list_sort =['G','A','V','L','I','M','P','F','W','S','T','N','Q','Y','C','K','R','H','D','E','X']

    AA_dict = {}
    numm = 1
    for i in AA_list_sort:
        AA_dict[i] = numm
        numm += 1
    return AA_dict
**Step 5: Traing the model on CSV files**
-	Build teacher model, train teacher model with teacher dataset and save this model: teacher_KD2.h5 
-	Evaluate model using 5-fold cross-validation:
-	Load model teacher_KD2.h5
-	Define Knowledge distillation model
-	Train model Knowledge distillation with 5-fold cross validation
-	Save model the best of Knowledge distillation model: KD2_1gram.h5
