 <p align="center">
	<h1 align="center"> Understanding the Relation between Noise and Bias <br />
	in Annotated Datasets </h1>
</p>

## Motivation
- **Bias in Annotation**: Annotator differences in <em>subjective tasks</em> introduce <em>bias in their annotations</em>, especially in sensitive domains like hate speech recognition, stemming from diverse backgrounds and perspectives.
- **Misinterpretation of Bias as Noise**: Minority votes are often considered <em>outliers</em> by models. This causes models to perceive them as noise, leading to biased predictions favoring <em>majority vote</em>.
- In this project, we'll explore if <em>perspectivist classification models</em> effectively utilize valuable insights from instances labeled as noisy by noise-detection techniques.


![annotations emoji image](./project_website/Annotations_image_emoji.png)

## Problem Statement
In the evolving landscape of machine learning, the reliability and fairness of models hinge on the quality of annotated data. However, the presence of bias, particularly in subjective tasks, has become a critical concern. This is especially prominent in sensitive domains like hate speech recognition, where annotators, stemming from diverse backgrounds and perspectives, might introduce bias in their annotations.


## Datasets

<table>  
  <tr>
    <td rowspan="2"></td>
    <th colspan="3" scope="colgroup">Toxicity and Hate Speech</th>
  </tr>
  <tr>
    <th scope="col">SBIC [1]</th>
    <th scope="col">Kennedy [2]</th>
    <th scope="col">Agree to Disagree [3]</th>
  </tr>
  <tr>
    <td style="text-align: left"><b># Annotators</b></td>
    <td style="text-align: center">307</td>
    <td style="text-align: center">7,912</td>
    <td style="text-align: center">819</td>
  </tr>
  <tr>
    <td style="text-align: left"><b># Annotations per annotator</b></td>
    <td style="text-align: center">479±829.6</td>
    <td style="text-align: center">17.1±3.8</td>
    <td style="text-align: center">63.7±139</td>
  </tr>
  <tr>
    <td style="text-align: left"><b># Unique texts</b></td>
    <td style="text-align: center">45318</td>
    <td style="text-align: center">39,565</td>
    <td style="text-align: center">10,440</td>
  </tr>
  <tr>
    <td style="text-align: left"><b># Annotations per text</b></td>
    <td style="text-align: center">3.2±1.2</td>
    <td style="text-align: center">2.3±1.0</td>
    <td style="text-align: center">5</td>
  </tr>
  <tr>
    <td style="text-align: left"><b># Labels</b></td>
    <td style="text-align: center">2</td>
    <td style="text-align: center">3</td>
    <td style="text-align: center">2</td>
  </tr>
</table>



## Methodology

### Two Regimes of Classification

<img src="./project_website/model 1.png" alt="model 1" height="500px" width="450px">&emsp;&emsp;<img src="./project_website/model 2.png" alt="model 1" height="500px" width="450px">

### MODEL AND PERFORMANCE

> **Model**

Trained 2 models for each dataset

<table>  
  <tr>
    <td style="text-align: left"><b>Majority Label Model</b></td>
    <td style="text-align: left"><b>Multi Annotator Model</b></td>
  </tr>
  <tr>
    <td style="text-align: left"> <b>Model</b> - Roberta-Base [6] <br /> <b>Epochs</b> - 5 <br /> <b>Learning Rate</b> - 5e-5 <br /> <b>Batch Size</b> - 32 </td>
    <td style="text-align: left"> <b>Model</b> - DISCO [7] <br /> <b>Epochs</b> - 5 <br /> <b>Learning Rate</b> - 2e-3 <br /> <b>Batch Size</b> - 200 </td>
  </tr>
</table>

> **Performance**

<table>  
  <tr>
    <td style="text-align: left"><b>Dataset</b></td>
    <td style="text-align: left"><b>F1 Score (majority)</b></td>
    <td style="text-align: left"><b>F1 Score (multi-annotator)</b></td>
  </tr>
  <tr>
    <td style="text-align: left">Agree to Disagree</td>
    <td style="text-align: center">0.78</td>
    <td style="text-align: center">0.78</td>
  </tr>
  <tr>
    <td style="text-align: left">Kennedy</td>
    <td style="text-align: center">0.68</td>
    <td style="text-align: center">0.75</td>
  </tr>
  <tr>
    <td style="text-align: left">SBIC</td>
    <td style="text-align: center">0.80</td>
    <td style="text-align: center">0.78</td>
  </tr>
</table>

### Uncertainty in Machine Learning Predictions

<ul>
	<li> <b>Data Cartography</b> summarizes training dynamics for all samples as: </li>
		<ul>
  			<li> <b>Confidence</b>: Mean of probabilities for gold label across epochs.</li>
  			<li> <b>Variability</b>: Standard Deviation of probabilities for gold label across epochs.</li>
		</ul>
</ul>

## Results

### DATASET CARTOGRAPHY

> **AGREE TO DISAGREE**

<img src="./project_website/plots_agree_to_disagree/conf_vs_var_color_correctness.png" alt="agree to disagree" height="350px" width="450px"> 

> **KENNEDY**

<img src="./project_website/plots_kennedy/conf_vs_var_color_correctness.png" alt="kennedy" height="350px" width="450px">

> **SBIC**

<img src="./project_website/plots_sbic/conf_vs_var_color_correctness.png" alt="sbic" height="350px" width="450px">

### SINGLE GROUND TRUTH MODEL

> **AGREE TO DISAGREE**

<img src="./project_website/plots_agree_to_disagree/agr_factor_vs_conf_hue.png" alt="agr factor vs conf" height="350px" width="500px">

> **KENNEDY**

<img src="plots_kennedy/agr_factor_vs_conf_hue.png" alt="agr factor vs conf" height="350px" width="500px">

> **SBIC**

<img src="./project_website/plots_sbic/agr_factor_vs_conf_hue.png" alt="agr factor vs conf" height="350px" width="500px">

### MULTI ANNOTATOR MODEL

> **AGREE TO DISAGREE**

<img src="./project_website/plots_agree_to_disagree/low_conf_mjr_disagree_vs_conf.png" alt="low conf mjr disagree vs conf" height="300px" width="400px">&emsp;&emsp;&emsp;&emsp;<img src="./project_website/plots_agree_to_disagree/group_count.png" alt="group count]" height="300px" width="400px">

<!--
<img src="plots_agree_to_disagree/disagree_vs_conf.png" alt="disagree vs conf" height="350px" width="350px">
<br>&nbsp;&nbsp;&nbsp;<img src="plots_agree_to_disagree/low_conf_mjr_disagree_vs_conf.png" alt="low conf mjr disagree vs conf" height="350px" width="350px">
<br>&nbsp;&nbsp;&nbsp;<img src="plots_agree_to_disagree/group_count.png" alt="group count]" height="350px" width="400px">-->

> **SBIC**

<img src="./project_website/plots_sbic/low_conf_mjr_disagree_vs_conf.png" alt="low conf mjr disagree vs conf" height="300px" width="400px">&emsp;&emsp;&emsp;&emsp;<img src="./project_website/plots_sbic/group_count.png" alt="group count" height="300px" width="400px">


> **KENNEDY**

<img src="./project_website/plots_kennedy/low_conf_mjr_disagree_vs_conf.png" alt="low conf mjr disagree vs conf" height="300px" width="400px">&emsp;&emsp;&emsp;&emsp;<img src="./project_website/plots_kennedy/group_count.png" alt="group count" height="300px" width="400 px">

<!--### KENNEDY
> **MAJORITY VOTE LABEL**

<img src="plots_kennedy/agr_factor_vs_conf_hue.png" alt="agr factor vs conf" height="350px" width="500px">
 
> **MULTI ANNOTATOR**

<img src="plots_kennedy/disagree_vs_conf.png" alt="disagree vs conf" height="350px" width="350px">
<br>&nbsp;&nbsp;&nbsp;<img src="plots_kennedy/low_conf_mjr_disagree_vs_conf.png" alt="low conf mjr disagree vs conf" height="350px" width="350px">
<br>&nbsp;&nbsp;&nbsp;<img src="plots_kennedy/group_count.png" alt="group count" height="350px" width="400 px">


### SBIC
> **MAJORITY VOTE LABEL**

<img src="plots_sbic/agr_factor_vs_conf_hue.png" alt="agr factor vs conf" height="350px" width="500px">

> **MULTI ANNOTATOR**

<img src="plots_sbic/disagree_vs_conf.png" alt="disagree vs conf" height="350px" width="350px">
<br>&nbsp;&nbsp;&nbsp;<img src="plots_sbic/low_conf_mjr_disagree_vs_conf.png" alt="low conf mjr disagree vs conf" height="350px" width="350px">
<br>&nbsp;&nbsp;&nbsp;<img src="plots_sbic/group_count.png" alt="group count" height="350px" width="400px">-->


## Analysis

<b>High Confidence in Majority model and Low Confidence in Multi-Annotator model</b>

> **Mislabeled annotations:**
<table>  
  <tr>
    <td style="text-align: left"><b>Text</b></td>
    <td style="text-align: left"><b>Annotation</b></td>
  </tr>
  <tr>
    <td style="text-align: left">I thought you were going to win this in a landslide</td>
    <td style="text-align: left">Offensive</td>
  </tr>
  <tr>
    <td style="text-align: left">crossing my fingers for you from Germany. Even though I am not an American.</td>
    <td style="text-align: left">Offensive</td>
  </tr>
  <tr>
    <td style="text-align: left">boy F**K you</td>
    <td style="text-align: left">Not Offensive</td>
  </tr>
  <tr>
    <td style="text-align: left">Fragility at its finest</td>
    <td style="text-align: left">Offensive</td>
  </tr>
</table>


## Findings

> **Single Ground Truth Model**

- There is <b>correlation between human disagreement on instances and model’s uncertainty/confidence</b> for classifying that instance.
- For instances that there is <b>more disagreement among human labelers there is also low confidence</b> from the single-GT model.

> **Multi-Annotator Model**

- Like single gold label model, we see <b>significant correlation between agreement between annotators and model confidence</b> in all the datasets, with the <b>confidence decreasing with more disagreement</b> between the annotators.
- For <b>low confidence samples in single ground truth model</b>, we observe multi-annotator model having <b>high confidence for labels which disagree with majority</b>, hence learning valuable information from samples that majority vote aggregation discards.
- We see <b>high number of annotations per annotator is necessary</b> to model different perspectives effectively.



## References

[1] [Social Bias Frames: Reasoning about Social and Power Implications of Language](https://aclanthology.org/2020.acl-main.486) (Sap et al., ACL 2020)

[2] [Constructing interval variables via faceted Rasch measurement and multitask deep learning: a hate speech application](https://arxiv.org/abs/2009.10277) (Kennedy et al., 2020)

[3] [Agreeing to Disagree: Annotating Offensive Language Datasets with Annotators’ Disagreement](https://aclanthology.org/2021.emnlp-main.822) (Leonardelli et al., EMNLP 2021)

[4] [SemEval-2018 Task 1: Affect in Tweets](https://aclanthology.org/S18-1001) (Mohammad et al., SemEval 2018)

[5] [Dataset Cartography: Mapping and Diagnosing Datasets with Training Dynamics](https://aclanthology.org/2020.emnlp-main.746) (Swayamdipta et al., EMNLP 2020)

[6] [RoBERTa: A Robustly Optimized BERT Pretraining Approach](https://arxiv.org/pdf/1907.11692.pdf) (Yinhan Liu et al., 2019)

[7] [Disagreement Matters: Preserving Label Diversity by Jointly Modeling Item and Annotator Label Distributions with DisCo](https://aclanthology.org/2023.findings-acl.287) (Weerasooriya et al., Findings 2023)

[8] [Annotators with Attitudes: How Annotator Beliefs And Identities Bias Toxic Language Detection](https://aclanthology.org/2022.naacl-main.431) (Sap et al., NAACL 2022)

[9] [Dealing with Disagreements: Looking Beyond the Majority Vote in Subjective Annotations](https://aclanthology.org/2022.tacl-1.6) (Mostafazadeh Davani et al., TACL 2022)


## About the Team

<table>
<tr align="center">
	
<td>
	
Abhishek Anand

<p align="center">
<img src = "./project_website/team/abhishek.jpeg"  height="120" alt="Abhishek Anand">
</p>
<p align="center"> MS in Computer Science </p>
</td>

<td>
	
Anweasha Saha

<p align="center">
<img src = "./project_website/team/anweasha.jpeg"  height="120" alt="Anweasha Saha">
</p>
<p align="center"> MS in Computer Science </p>
</td>

<td>
	
Prathyusha Naresh Kumar

<p align="center">
<img src = "./project_website/team/prathyusha.jpeg"  height="120" alt="Prathyusha Naresh Kumar">
</p>
<p align="center"> MS in Computer Science </p>
</td>

<td>
	
Negar Mokhberian
	
<p align="center">
<img src = "./project_website/team/negar.png"  height="120" alt="Negar Mokhberian">
</p>
<p align="center"> PhD in Computer Science </p>
</td>

<td>
	
Ashwin Rao

<p align="center">
<img src = "./project_website/team/ashwin.png"  height="120" alt="Ashwin Rao">
</p>
<p align="center"> PhD in Computer Science </p>
</td>

<td>
	
Zihao He

<p align="center">
<img src = "./project_website/team/zihao.png"  height="120" alt="Zihao He">
</p>
<p align="center"> PhD in Computer Science </p>
</td>

</tr>
  </table>
