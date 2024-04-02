# Validation of eos6oli Model
This repository contains all codes and datasets used for the validation of eos6oli model. Since there are millions of compounds, it would be slow and expensive to experimentally determine the solubility of these compounds.Hence, the need for such models. This model predicts Acqeous Solubility of compounds, an important property for drug discovery using a molecule's SMILES representation as input. The model is based on the Molecule Attention Transformer (MAT) architecture found in literature which applies a self-attention mechanism to the molecules' SMILES represented in a graph but skips the distance matrix calculation step to accelerate predictions.
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
I downloaded,fetched and served the model in [Model_Bias](/notebooks/Model_Bias.ipynb) . To ensure it was working smoothly, I ran predictions for this sample [dataset](/data/input/eml_canonical.csv). I saved the predictions [result](/data/output/eos6oli_output.csv).
### 4
I downloaded molecules used from Harvard Dataverse because I needed a dataset that has actual or experimentally determined solubility values to compare my predictions with.On Harvard Dataverse, I searched for Aqsoldb a manually curated reference dataset of compounds with their acqous solubility values.I downloaded the [dataset](/data/input/curated-solubility-dataset.csv).
#### Exploring the dataset
I explored the dataset, ensured the molecules had valid SMILES representation using rdkit library, and saved random 1000 entries into a csv [file](/data/input/1000molecules.csv) to be used.
### 5
I ran predictions with the model, generated an [output](/data/output/1000predictions.csv) and I tried to match it with the actual solubility values using the SMILES [here](/data/output/predictions.csv). The model predicts the solubility. I made a scatter and residual plots of the actual solubility vs the predicted solubility [plots](/figures/1000molecules) of the predictions. With the scatter plot forming a diagonal line and the residual plot being centred around 0 and the mean absolute error at 0.82, it suggests that the model is not bias.

## Task 2
### 1
I read the [publication](/eos6oli.pdf) and saw a result I could reproduce using the SC2 dataset that was used in the study. 
### 2
From the publication, I was able to find the github repository which has the installation and usage intructions. In Section A of  [Model_Reproducibility](/notebooks/Model_Reproducibility.ipynb), I installed dependencies and the python package of the model. Using the SC2 [dataset](/data/input/llinas2020_raw.csv) that I found in the github repository they provided in the publication. I ensured the SMILES representation was valid using rdkit library. I made predictions with the model, saved the [output](/data/output/SoltranetPredictions.csv). To ascertain reproducibility, I compared the predictions generated the Soltranet model with the actual solubility values using that [dataset](/data/input/merged_predictions.csv) and re-created an [histogram](/figures/Soltranet/Reproducibility_plot.png) I saw on the publication. The result was the same indicating reproducibility. I also went ahead to use a more categorized [datasets](/data/input/SensitivityDatasets) also found on their repository to generate sensitivity [results](/figures/Soltranet/Sensitivity) seen on the publication and the output was also the same.
### 3
Using the same SC2 [dataset](/data/input/llinas2020_raw.csv), in Section B of [Model_Reproducibility](/notebooks/Model_Reproducibility.ipynb), I generated predictions using Ersilia model, saved the [result](/data/output/ErsiliaSoltranet.csv) and compared the results using the [dataset](/data/input/merged_Ersiliapredictions.csv). I recreated an [histogram](/figures/Ersilia/Reproducibility_plotErsilia.png) and sensitivity [results](/figures/Ersilia/Sensitivity) . The results generated using Ersilia and the author's model was exactly the same.

## Week 3
### Task 1
After a short literature review, i found this [publication](/Publication.pdf) that has several datasets on molecules and their experimentally determined solubility. I downloaded one for use as my external [dataset](/data/input/aqua_stand.csv). I also downloaded the training [dataset](/data/input/aqsol.csv) for the soltranet model and compared the smiles with the ones on my external dataset to be sure there is no data leakage. Out of 1310 smiles, I found out 516 were part of the training datasets and had to delete them from my external datasets. I checked and confirmed the smiles were in standard form and generated Inchikeys for the molecules. I saved the processed [dataset](/data/output/noLeaks_data.csv). I made predictions with the eos6oli model and saved the [output](/data/output/ErsiliaValidation.csv). I matched the ouput withe the external dataset to get the experimental values and saved the csv [file](/data/output/merged_ErsiliaValidation.csv). To validate the model, I calculated the R2 score (coefficient of determination) and the score is 0.88 suggesting that the model does well at capturing the patterns and relationships in the dataset with the predictions being very close to the experimental values.

### PCA of Morgan Fingerprints
I made a PCA [plot](/figures/PCA/PCAMorganFingerprints_plot.png) of the training and external validation set using morgan fingerprints and the two sets of data overlap, suggesting that the distribution of the validation set was roughly within the scope of the chemical space of the training set, which indicated that the model could predict the solubility of the validation set.

### Tanimoto Similarity Difference
Because of the overlap seen in the PCA plot, I went ahead to calculate the tanimoto similarity difference between the training and validation dataset. The average Tanimoto similarities between the data in test set and validation set was 0.085. I made [histogram](/figures/TanimotoSimilarity/TanimotoSimilarity_plot.png) and [Kernel density estimate](/figures/TanimotoSimilarity/TanimotoSimilarity2_plot.png) plots of the diffrence and the Tanimoto similarity between the molecules were mostly distributed between 0 and 0.4 which indicated that molecules used in validation were obviously structurally diverse from that of the training set.

# References
* [Soltranet](https://github.com/gnina/SolTranNet)
* [Soltranet Datasets and Figures Generations Repository](https://github.com/francoep/SolTranNet_paper)
* [Ersilia Google Colab Guide](https://github.com/ersilia-os/ersilia/blob/master/notebooks/ersilia-on-colab.ipynb)
* [Harvard Dataverse](https://dataverse.harvard.edu/)
