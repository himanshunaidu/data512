# DATA 512 Homework 2: Considering Bias in Wikipedia Politicians Data

## Project Goal

This goal of this project is to explore bias in data using Wikipedia articles about political figures from different countries. The analysis aims to examine the coverage of politicians on Wikipedia and the quality of articles about politicians across nations. 

The code for the project is present in the Jupyter notebook [wikipedia_politician_bias.ipynb](wikipedia_politician_bias.ipynb)


## License

### Source Data

The Wikipedia Category:Politicians by nationality was crawled to generate a list of Wikipedia article pages about politicians from a wide range of countries. This data is in this repository as politicians_by_country.AUG.2024.csv.
The population data is available in CSV format as population_by_country_AUG.2024.csv from the repository. This dataset was downloaded from the world population data sheet published by the Population Reference Bureau.
The article quality is extracted using the ORES API. ORES (Objective Revision Evaluation Service) is a web service and API that provides machine learning as a service for Wikimedia projects. The different quality levels that ORES assignes to an article (from best to worst) are as follows:
FA - Featured article
GA - Good article (also known as A-Class)
B - B-Class article
C - C-Class article
Start - Start-class article
Stub - Stub-class article
ORES requires a specific revision ID of an article to be able to make a label prediction. For our analysis, we will use the latest revision of an article. To obtain the latest revision ID for an article, we will use the Article Page Info MediaWiki API.
The resulting dataset consisting of country, region, population, article_title (politician name), revision_id and article_quality is stored in wp_politicians_by_country.csv which can be found on the repository.
wp_countries-no_match.txt consists of all countries for which there are no matches i.e either the population dataset does not have an entry for the equivalent Wikipedia country, or vice-versa.
articles_without_scores.txt consists of all the politicians for whom we were unable to extract the latest revision ID for their corresponding articles through the page info API. This seems to be because these articles are not in English.
All the data collected in this analysis through the APIs are subject to the terms and conditions of the Wikimedia Foundation terms of use which states that users can freely access and reuse the content on Wikimedia platforms, including articles and datasets, under free and open licenses. Any contributions made to Wikimedia platforms must be licensed under a free and open license, allowing the content to be freely shared and reused by others. Users are responsible for their edits and contributions and must adhere to laws, avoid copyright infringement, and respect the platform's policies.

How the Terms of Use Apply:
- The dataset created in this project is derived from Wikimedia's raw data. As such, it falls under the [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/deed.en) ("CC BY-SA 4.0")
- Attribution: If you use or share this dataset, you must provide attribution to the Wikimedia Foundation. The attribution should include a reference to both the original source of the data (the Wikimedia Foundation) and this project.
- Freely Accessible: The data must remain open and freely accessible to others, as per the terms of the Wikimedia Foundation.

## How to Run

The entire code of the project resides in the Jupyter notebook [wikipedia_politician_bias.ipynb](wikipedia_politician_bias.ipynb).

In order to run the notebook, start by setting up the Conda environment, using the [data512.yml](data512.yml).

### Environment Setup

#### Python Environment

To set up the Conda environment for the project, using the [data512.yml](data512.yml) file, follow these steps:

1. Open a terminal or command prompt.
2. Navigate to the directory where the data512.yml file is located. For this project, it would be the data-512-homework_1 folder.

    Note: Switch to the main branch.

3. Run the following command to create the Conda environment:

    ```
    conda env create -f data512.yml
    ```

    This command will read the data512.yml file and create a new Conda environment with the specified dependencies.

4. Once the environment is created, activate it by running the following command:

    ```
    conda activate data512
    ```
    (If the name in data512.yml has been changed, update the above environment name accordingly)

5. You can now proceed with running your notebooks or any other tasks within the activated Conda environment.

Remember to deactivate the environment when you're done by running `conda deactivate`.

#### Environment File for Credentials

The project uses the dotenv package to load credentials (mainly ORES API, further instructions in the notebook) from a file called '.env' in the same directory as this notebook. The file should look like this:

```
    WIKIMEDIA_USERNAME="<your_wikimedia_username>"
    WIKIMEDIA_CLIENT_ID="<your_wikimedia_client_id>"
    WIKIMEDIA_CLIENT_SECRET="<your_wikimedia_client_secret>"
    WIKIMEDIA_ACCESS_TOKEN="<your_wikimedia_provided_access_token_its_a_really_long_string>"
```

The repository has a file called '.env.example' that you can copy to '.env' and fill in the values with your own credentials. 


### Running the Notebook

The notebook does not need any additional configuration. Thus, you can run the code using the 'Run All' option.

The entire code takes ~2 hours 30 minutes to run on the system used to develop this project, with the main bottleneck being the 'Getting Article Quality Predictions' step that involves using the ORES API (that has rate limits).

Note: The system used to develop this project is equipped with a 12th Gen Intel® Core™ i7-12700H processor (2.30 GHz)


## Analysis



## Research Implications


