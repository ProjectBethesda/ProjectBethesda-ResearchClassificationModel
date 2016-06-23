# Project Bethesda: Research Classification Model

Classifcation model that identifies the research phase of Pubmed articles pertaining to Mendelian Genetics from Medline Metadata. For a walkthrough on how to reproduce the results below using Azure ML [click here](https://github.com/ProjectBethesda/ProjectBethesda-ResearchClassificationModel/blob/master/Methods.md)

**When using this work please cite:**
     *Tracking medical genetic literature through machine learning*, Bornstein, Aaron T. et al.Molecular Genetics and Metabolism

##Contents##
  1. **Classification Methodology**
  2. **Performance Benchmarks**
  3. **Resources to learn more about Azure ML** 

##1. Classification Methodology##
**Project Bethesda Dataset**
   
The DataSet contains Medline Metadata from 2100 Articles categorized  by Dr. Benjamin Solomon head of Genomics at Inova ITMI
   - **Dataset Composition** 
      - Articles correspond to 140 Genes
      - 15 Articles per a Gene 
      - 5 Articles per a research type per a Gene.
      
- **Abstract Normalization**
   - Convert all text to lowercase 
   - Remove Stopwords from NLTK Stopwords Corpus
   - Remove Standalone numbers (1, 2, 3 but not brca1)
   - Remove Number Words (one,two, three)
   - Remove Punctuation (periods, commas, etc)

- **Feature Selection**
  - Prepend the Title, Authors,  Journal Title Abbreviation, Publication Type to the abstract
  - Use the Azure ML feature hashing module with n-grams of 4 and a Hashing Bitsize of 15
  - Convert ResearchPhase into a TwoClassLabel

- **Model Selection and Parameters**
  - Combine a two-class Boosted Decison Tree with a One vs All Classifer
    - Max of 32 Leaves Per a Tree
    - Min of 50 instances per a Leaf
    - Learning Rate of 0.2
    - 300 Trees

##2. Performance Benchmarks##

Using a randomized test/train split of 70-30 here is the average run result:

 - 0 = Basic Science Articles
 - 1 = Clinical Articles 
 - 2 = Managed Articles

![alt tag](/media/ProjectBethesdaML%20Results.png)

##3. Resources to learn more about Azure ML:##

* [MVA Getting Started with Microsoft Azure Machine Learning](https://www.microsoftvirtualacademy.com/en-us/training-courses/getting-started-with-microsoft-azure-machine-learning-8425)
*	[Azure Machine Learning (FAQ) Types](https://azure.microsoft.com/en-us/documentation/articles/machine-learning-faq/)
* [Blog: TechNet Machine Learning Blog](http://blogs.technet.com/b/machinelearning/)
* [Module Descriptions: Machine Learning Module Descriptions] (https://msdn.microsoft.com/en-us/library/azure/dn906013.aspx)

```
**ABOUT THE Author**

Ari Bornstein is a Microsoft Developer Evangelist out of NYC. He works with ISVs to develop Consumer Cloud and Client Solutions. Ari is passionate about many things ranging from computer science to desert archeology. Prior to working at Microsoft, Ari worked with the Inova Hospital System in Fairfax VA to build machine learning classifiers that detect references to new treatments in medical literature. Ari has written a series of blog posts on ML Classification on his blog at pythiccoder.com. 

``` 
