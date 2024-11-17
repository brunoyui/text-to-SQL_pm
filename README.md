# Applying Text-to-SQL in Process Mining: Leveraging Natural Language for Data Insights

This repository includes the resources referenced in the paper, as well as complementary content. Bellow the details of each resource:

- dataset: 
    - text2sql4pm.tsv: contains all data in tsv format file
    - gold_en.txt: contains the standard SQL statements for English language
    - gold_en.txt: contains the standard SQL statements for Portuguese language 

- results: evaluations of SQL statements generated by the models using OpenAI and Code representations with 0-shot and 1-shot prompt strategies. The results for both languages, English and Portuguese are available in their respective folders. Each strategy used are identified by the folder name and contains the same structure.
    - questions.json: contains the prompts to ask models to generate SQL statements
    - RESULTS_MODEL-gemini-1.0-pro.txt: SQL statements generated by Gemini-1.0 Pro model
    - RESULTS_MODEL-gpg-3.5-turbo.txt: SQL statements generated by GPT-3.5 Turbo model
    - RESULTS_MODEL-Meta-Llama-3-8B-Instruct.txt: SQL statements generated by Llama3-8B Instruct
    - evaluations:
        - scores_cr_gemini10_EM: evaluation results on Exact Match Accuracy metric of SQL statements generated by Gemini-1.0 Pro 
        - scores_cr_gemini10_EX: evaluation results on Execution Accuracy metric of SQL statements generated by Gemini-1.0 Pro 
        - scores_cr_gpt35_EM: evaluation results on Exact Match Accuracy metric of SQL statements generated by GPT-3.5 Turbo 
        - scores_cr_gpt35_EX: evaluation results on Execution Accuracy metric of SQL statements generated by GPT-3.5 Turbo 
        - scores_cr_llama3_EM: evaluation results on Exact Match Accuracy metric of SQL statements generated by Llama3-8B Instruct
        - scores_cr_llama3_EX: evaluation results on Execution Accuracy metric of SQL statements generated by Llama3-8B Instruct

- graphs_results: contains the graphs images for all SQL complexity results for each metric on both languages, Portuguese and English

- scripts:
    - main.py: the entry point for executing the results analysis based on the parameters provided
    - execute_analysis.py: the common pre-steps for executing results analysis for each SQL complexity
    - execution.py: steps and configurations necessary to process the results and generates the graphs for each SQL complexity
    - graphs_plot.py: function to generate the graphs for the paper and complementary content
    - loader_results.py: contains the class used to support the load of files results for each prompt strategy (0-shot and 1-shot) and prompt representation
    - sql_pattern.py: contains filters for SQL patterns template founded in each SQL complexity 
    - utils.py: auxiliary function to calculate results percentage
    - run.sh: shell script to process all results

## Complementary content

This section contains details of each SQL pattern template founded and the complete results of models evaluations using Exact Match Accuracy (EM) and Execution Accuracy (EX) metrics for both languages, English and Portuguese.

### SQL patterns templates and results

#### Easy
|  Symbol   |                                           SQL Pattern                                                       |
|-----------|-------------------------------------------------------------------------------------------------------------|
| Sc        | SELECT *concept* FROM event\_log (ORDER BY *concept*<sup>+</sup>)<sup>*</sup>                              |
| ScFc      | SELECT *concept* FROM event\_log WHERE (FILTER *concept*) (ORDER BY *concept*<sup>+</sup>)<sup>*</sup>      | 
| ScGcFc<sup>+</sup>| SELECT *concept* FROM event\_log GROUP BY *concept* HAVING (FILTER *concept*)<sup>+</sup>              |
| Ac        | SELECT AGG(*concept*) FROM event\_log                                                                       |           
| AcFc      | SELECT AGG(*concept*) FROM event\_log (FILTER *concept*)                                                    |

**Exact Match Accuracy**

*English*
![My Image](graphs_results/results_easy_EM.png)

*Portuguese*
![My Image](graphs_results/results_easy_EM_pt.png)

**Execution Accuracy**

*English*
![My Image](graphs_results/results_easy_EX.png)

*Portuguese*
![My Image](graphs_results/results_easy_EX_pt.png)

#### Medium
|  Symbol   |                                           SQL Pattern                                                       |
|-----------|-------------------------------------------------------------------------------------------------------------|
| Sc<sup>+</sup> | SELECT (*concept*<sup>+</sup>) from event\_log (ORDER BY *concept*)<sup>*</sup> |
| ScGc  | SELECT *concept* FROM event\_log GROUP BY *concept* ORDER BY *concept* |
| Sc<sup>+</sup>Fc<sup>+</sup>   | SELECT (*concept*<sup>+</sup>) FROM event\_log WHERE (FILTER *concept*)<sup>+</sup> (ORDER BY *concept*)<sup>*</sup> |
| Sc<sup>+</sup>GcFc<sup>+</sup> |  SELECT (*concept*<sup>+</sup>) FROM event\_log GROUP BY (*concept*<sup>+</sup>) HAVING (FILTER *concept*) |
| Acc<sup>+</sup>Gc | SELECT AGG(*concept*), (*concept*<sup>+</sup>) FROM event\_log GROUP BY *concept* |
| Ac(c<sup>+</sup>)<sup>*</sup>Fc<sup>+</sup>(Gc)<sup>*</sup> | SELECT AGG(*concept*), (*concept*<sup>+</sup>)<sup>*</sup> FROM event\_log WHERE (FILTER *concept*)<sup>+</sup>(GROUP BY *concept*)<sup>*</sup> |
| (Ac)<sup>+</sup>c(Fc)<sup>*</sup>GcFc | SELECT AGG(*concept*<sup>+</sup>), *concept* FROM event\_log (WHERE FILTER *concept*)<sup>*</sup> GROUP BY *concept* HAVING (FILTER *concept*) |

**Exact Match Accuracy**

*English*
![My Image](graphs_results/results_medium_EM.png)

*Portuguese*
![My Image](graphs_results/results_medium_EM_pt.png)

**Execution Accuracy**

*English*
![My Image](graphs_results/results_medium_EX.png)

*Portuguese*
![My Image](graphs_results/results_medium_EX_pt.png)

#### Hard

#### Extra

#### No hardness






