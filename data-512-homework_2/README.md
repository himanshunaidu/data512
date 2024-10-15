# DATA 512 Homework 2: Considering Bias in Wikipedia Politicians Data

## Project Goal

This goal of this project is to explore bias in data using Wikipedia articles about political figures from different countries. The analysis aims to examine the coverage of politicians on Wikipedia and the quality of articles about politicians across nations. 

The code for the project is present in the Jupyter notebook [wikipedia_politician_bias.ipynb](wikipedia_politician_bias.ipynb)

## Data

### Source Data

- WikiPedia Category:Politicians

The Wikipedia [Category:Politicians](https://en.wikipedia.org/wiki/Category:Politicians_by_nationality) by nationality was crawled to generate a list of Wikipedia article pages about politicians from a wide range of countries. This data is in this repository as [politicians_by_country.AUG.2024.csv](./politicians_by_country_AUG.2024.csv).

- Population Reference Bureau

The population data is available in CSV format as [population_by_country_AUG.2024.csv](./population_by_country_AUG.2024.csv) from the repository. This dataset was downloaded from the world population data sheet published by the [World Population Data Sheet](https://www.prb.org/international/indicator/population/table/).

- ORES API

We're using a machine learning system called ORES (Objective Revision Evaluation Service) to estimate the quality of each article. The article quality estimates are, from best to worst:
    - FA - Featured article
    - GA - Good article (also known as A-Class)
    - B - B-Class article
    - C - C-Class article
    - Start - Start-class article
    - Stub - Stub-class article

ORES requires a specific revision ID of an article to be able to make a label prediction. For our analysis, we will use the latest revision of an article. To obtain the latest revision ID for an article, we will use the Article Page Info MediaWiki API.

#### Terms of Use

How the Terms of Use Apply:
- The data created in this project is derived from Wikimedia's raw data and the ORES Machine Learning models. As such, it falls under the [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/deed.en) ("CC BY-SA 4.0")
- Attribution: If you use or share this data, you must provide attribution to the Wikimedia Foundation. The attribution should include a reference to both the original source of the data (the Wikimedia Foundation) and this project.
- Freely Accessible: The data must remain open and freely accessible to others, as per the terms of the Wikimedia Foundation.



### Intermediate Data

1. [wp_politicians_with_page_info.csv](./data/wp_politicians_with_page_info.csv)

This file consists of the dataframe that is the output of the loop in [wikipedia_politician_bias.ipynb](wikipedia_politician_bias.ipynb) that queries the PageInfo API to get the latest revision ids of the Wikipedia articles present in [politicians_by_country.AUG.2024.csv](./politicians_by_country_AUG.2024.csv).

2. [page_info_errors.txt](./data/page_info_errors.txt)

This file consists of the politicians for which the PageInfo API failed to work. 

3. [wp_politicians_with_ores.csv](./data/wp_politicians_with_ores.csv)

This file consists of the dataframe that is the output of the loop in [wikipedia_politician_bias.ipynb](wikipedia_politician_bias.ipynb) that queries the ORES API to get the predicted article quality for the latest revision of the Wikipedia articles present in [politicians_by_country.AUG.2024.csv](./politicians_by_country_AUG.2024.csv).

4. [ores_errors.txt](./data/ores_errors.txt)

This file consists of the politicians for which the ORES API failed to work. 

### Final Data

1. [wp_politicians_by_country.csv](./data/wp_politicians_by_country.csv)

This file consists of the final dataframe created by the Jupyter notebook [wikipedia_politician_bias.ipynb](wikipedia_politician_bias.ipynb). Each row corresponds to a Wikipedia page of a politician, belonging to a specific country (and region), along with the prediction of the article quality by ORES API. 

Below is a description of each column in the dataset:

    - page_id:
    Type: Integer
    The unique identifier for each Wikipedia page.

    - title:
    Type: String
    The title of the Wikipedia page.

    - revision_id:
    Type: Integer
    The unique identifier of the most recent revision made to the Wikipedia page.

    - article_quality_prediction:
    Type: String
    The predicted quality of the Wikipedia article based on the ORES machine learning model. This prediction is based on a set of machine learning models that assess Wikipedia articles, using labels such as Stub, Start, C, B, GA (Good Article), or FA (Featured Article).

    - country:
    Type: String
    The country that the Wikipedia page is associated with (if relevant).

    - population:
    Type: Integer
    The population of the country (if applicable). This data is sourced from publicly available demographic records.

    - region:
    Type: String
    The region or continent where the country is located.



2. [wp_countries-no_match.txt](./data/wp_countries-no_match.txt) 

This file consists of all countries for which there are no matches i.e either the population dataset does not have an entry for the equivalent Wikipedia country, or vice-versa.


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


