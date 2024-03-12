# Validation of eos6oli Model
This repository contains all codes and datasets used for the validation of my model of choice. This model predicts Acqeous Solubility of compounds, an important property for drug discovery.
## Characteristics
* Input: Compound
* Input shape: Single
* Task: Regression
* Output: Experimental value
* Output shape: Single (Predicted log of solubility of the compound)

## Repository Ogranization
* '/notebooks' contains all colab notebooks used
* '/data' contains all the datasets
* '/data/input' contains all inputs
* '/data/output' contains all outputs generated
* '/figues' contains all figues generated
* '/requirements.txt' contains all requirements

## Task 1
### 1
Going through the models provided, I choose the eos6oli because I was able to understand the aim and the methodology of the publication more.
### 2
I created this repository for all files
### 3
I downloaded,fetched and served the model in this [notebook](/notebooks/Ersilia_Week2_Task1_3to4.ipynb) . To ensure it was working smoothly, I ran pedictions for this sample [dataset](/data/input/eml_canonical.csv) and saved the [result](/data/output/eos6oli_output.csv).
### 4
I downloaded molecules used from Chembl. From the homepage, I navigated to compounds, filtered to small molecules that have been approved and downloaded 3592 of them in tsv as seen [here](/data/input/Chembl.tsv).
#### Exploring the dataset
I explored the dataset, ensured the molecules had SMILE representation, found out some entries had missing values,cleaned it up and saved the first 1000 entries into a csv [file](/data/input/1000molecules.csv) to be used.
### 5
I ran predictions with the model, generated an [output](/data/output/1000predictions.csv) and i tried to match it with the drug names [here](/data/output/predictions.csv). The model predicts the solubility. I made a scatter, histogram, violin and box [plots](/figures/1000molecules) of the predictions. The ouput shows that the solubility of most of these molecules were between -9 and +2, with  majority at around -3.

## Task 2
### 1
I read the [publication](/eos6oli.pdf) and saw a result I could reproduce using the SC2 dataset that was used in the study. 
### 2
From the publication, I was able to find the github repository which has the installation and usage intructions. In this [notebook](/notebooks/Ersilia_Week2_Task2_2.ipynb), I installed dependencies and the python package of the model. Using the SC2 [dataset](/data/input/llinas2020_raw.csv) that i found in the github repository they provided in the publication, I made predictions with the model, saved the [output](/data/output/SoltranetPredictions.csv). To ascertain reproducibility, I compared the predictions generated the Soltranet model with the actual solubility values using that [dataset](/data/input/merged_predictions.csv) and re-created an [histogram](/figures/Soltranet/Reproducibility_plot.png) I saw on the publication. The result was the same indicating reproducibility. I also went ahead to use a more categorized [datasets](/data/input/SensitivityDatasets) also found on their repository to generate sensitivity [results](/figures/Soltranet/Sensitivity) seen on the publication and the output was also the same.
### 3
Using the same SC2 [dataset](/data/input/llinas2020_raw.csv), in this [notebook](/notebooks/Ersilia_Week2_Task2_3.ipynb), I generated predictions using Ersilia model, saved the [result](/data/output/ErsiliaSoltranet.csv) and compared the results using the [dataset](/data/input/merged_Ersiliapredictions.csv). I recreated an [histogram](/figures/Ersilia/Reproducibility_plotErsilia.png) and sensitivity [results](/figures/Ersilia/Sensitivity) . The results generated using Ersilia and the author's model was exactly the same.

# References
* [Soltranet](https://github.com/gnina/SolTranNet)
* [Soltranet Datasets and Figures Generations Repository](https://github.com/francoep/SolTranNet_paper)
* [Ersilia Google Colab Guide](https://github.com/ersilia-os/ersilia/blob/master/notebooks/ersilia-on-colab.ipynb)
