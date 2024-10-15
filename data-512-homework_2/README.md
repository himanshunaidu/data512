# DATA 512 Homework 2: Considering Bias in Wikipedia Politicians Data

## Project Goal

This goal of this project is to explore bias in data using Wikipedia articles about political figures from different countries. The analysis aims to examine the coverage of politicians on Wikipedia and the quality of articles about politicians across nations. 

The code for the project is present in the Jupyter notebook [wikipedia_politician_bias.ipynb](wikipedia_politician_bias.ipynb)



## How to Run

The entire code of the project resides in the Jupyter notebook [wikipedia_politician_bias.ipynb](wikipedia_politician_bias.ipynb).

In order to run the notebook, start by setting up the Conda environment, using the [data512.yml](data512.yml).


### Python Environment

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


### Get access token

To access ORES Lift Wing, you'll need a Wikimedia account. If you already have a Wikipedia account, it might work. Otherwise, create a new account to get an access token.
Use this [official guide](https://api.wikimedia.org/wiki/Authentication) to create an API key for your account. * Make sure to create a Personal API token instead of Server-side app key* 
On successfully creating the access token, you'll receive a Client ID, Client Secret, and Access Token—save all three. If lost, you'll need to deactivate the token and create a new one.

In the code for data acquisition, make sure to use your username and the Access Token generated.


### Environment File for Credentials

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



## Data

### Source Data

- [politicians_by_country.AUG.2024.csv](./politicians_by_country_AUG.2024.csv)

The Wikipedia [Category:Politicians](https://en.wikipedia.org/wiki/Category:Politicians_by_nationality) by nationality was crawled to generate a list of Wikipedia article pages about politicians from a wide range of countries. This data is in this repository as [politicians_by_country.AUG.2024.csv](./politicians_by_country_AUG.2024.csv).

```Text
name        # name of the politician (article)
url         # url to the Wikipedia article
country     # country to which the politician belongs
```

- [population_by_country_AUG.2024.csv](./population_by_country_AUG.2024.csv)

The population data is available in CSV format as [population_by_country_AUG.2024.csv](./population_by_country_AUG.2024.csv) from the repository. This dataset was downloaded from the world population data sheet published by the [World Population Data Sheet](https://www.prb.org/international/indicator/population/table/).

```Text
Geography        # name of the country/region
Population       # population in millions
```

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

```Text
pageid          # page id of the Wikipedia article
title           # name of the article (politicians name)
revision_id     # latest revision id of the wikipedia article (fetched from PageInfo API)
page_length     # length of the Wikipedia article (not necessaryy)
```

2. [page_info_errors.txt](./data/page_info_errors.txt)

This file consists of the politicians for which the PageInfo API failed to work. 

3. [wp_politicians_with_ores.csv](./data/wp_politicians_with_ores.csv)

This file consists of the dataframe that is the output of the loop in [wikipedia_politician_bias.ipynb](wikipedia_politician_bias.ipynb) that queries the ORES API to get the predicted article quality for the latest revision of the Wikipedia articles present in [politicians_by_country.AUG.2024.csv](./politicians_by_country_AUG.2024.csv).

```Text
pageid                      # page id of the Wikipedia article
title                       # name of the article (politicians name)
revision_id                 # latest revision id of the wikipedia article (fetched from PageInfo API)
page_length                 # length of the Wikipedia article (not necessaryy)
article_quality_prediction  # article rating fetched from the ORES API call      
```

4. [ores_errors.txt](./data/ores_errors.txt)

This file consists of the politicians for which the ORES API failed to work. 

### Final Data

1. [wp_politicians_by_country.csv](./data/wp_politicians_by_country.csv)

This file consists of the final dataframe created by the Jupyter notebook [wikipedia_politician_bias.ipynb](wikipedia_politician_bias.ipynb). Each row corresponds to a Wikipedia page of a politician, belonging to a specific country (and region), along with the prediction of the article quality by ORES API. 

Below is a description of each column in the dataset:

```Text
page_id                         # unique identifier for each Wikipedia page.

title                           # title of the Wikipedia page.

revision_id                     # unique identifier of the most recent revision made to the Wikipedia page.

article_quality_prediction      # predicted quality of the Wikipedia article based on the ORES machine learning model. 

country                         # country that the Wikipedia page is associated with (if relevant).

population                      # population of the country (if applicable). 

region                          # region or continent where the country is located.
```



2. [wp_countries-no_match.txt](./data/wp_countries-no_match.txt) 

This file consists of all countries for which there are no matches i.e either the population dataset does not have an entry for the equivalent Wikipedia country, or vice-versa.

## Analysis

The analysis consists of calculating total-articles-per-capita (a ratio representing the number of articles per person)  and high-quality-articles-per-capita (a ratio representing the number of high quality articles per person) on a country-by-country and regional basis.

We produce tables for the following (the dataframes and output can be found in the notebook):
1. Top 10 countries by coverage: The 10 countries with the highest total articles per capita (in descending order) .
2. Bottom 10 countries by coverage: The 10 countries with the lowest total articles per capita (in ascending order) .
3. Top 10 countries by high quality: The 10 countries with the highest high quality articles per capita (in descending order) .
4. Bottom 10 countries by high quality: The 10 countries with the lowest high quality articles per capita (in ascending order).
5. Geographic regions by total coverage: A rank ordered list of geographic regions (in descending order) by total articles per capita.
6. Geographic regions by high quality coverage: Rank ordered list of geographic regions (in descending order) by high quality articles per capita.


## Known Issues

- Potential Data Inconsistencies with Wikipedia Categories

Wikipedia categories are folksonomic, meaning there is very little control over how they are applied to pages. This means that the set of pages is very likely some kind of subset, and may have pages that are not actually about individual politicians. 

- ORES API Rate Limits

The ORES API has quite strict rate limits, and one must adhere to it. It was found that depending on the throttling logic set for the ORES API requests, varying number of API requests could fail/timeout, and this is not deterministic.

- Incorrect Hierarchical Matching

In this analysis, countries were assigned to the closest (lowest in the hierarchy) region. This is not necessarily valid, as a country could belong to multiple regions. 

- Mismatching Country Names between Wikipedia article data and Population data

There are some countries that are named differently between the [politicians_by_country.AUG.2024.csv](./politicians_by_country_AUG.2024.csv) and [population_by_country_AUG.2024.csv](./population_by_country_AUG.2024.csv) files (Example: "Korea, South" vs Korea (South)). These will need to be manually corrected while performing analyses, in case one needs to consider them. 


## Research Implications

This project explores bias in Wikipedia articles about political figures from different countries. It aims to underscore the importance of recognizing biases in the source data itself, as these could snowball into more serious issues in the models and results. The project shows an example of how much of the information available online inherently contains some level of bias, which may arise from factors such as gender, religion, culture, literacy rates etc.

Further analysis using the tables mentioned in the 'Analysis' section revealed interesting insights. On a high level, we see that most of the countries in the top 10 in regards to total-articles-per-capita (a ratio representing the number of articles per person) and high-quality-articles-per-capita (a ratio representing the number of high quality articles per person) are those belonging to relatively developed regions, such as those in Europe, Oceania and the Americas. On the other hand, the countries that fall in the bottom 10 in regards to these numbers predominantly belong to Asia and Africa. This indicates some clear patterns in how article quality is skewed, thus serving as a warning to exercise caution when using Wikipedia data to perform any kind of analysis.

<!-- One must note however, that there are several potential shortcomings with this very analysis conducted in the project, that should prevent one from making definitive conclusions from the results. Firstly, the per-capita numbers end up potentially adding too strong a penalty to highly populated countries such as India and China. We see that they are at the bottom of the total-articles-per-capita table, and one cannot conclude with certainty whether population is responsible for this. Further analysis into this would be prudent. 
Also, there are various (potentially well-represented) countries missing from the dataset, such as Australia, Canada, New Zealand, etc. 
Lastly, a major part of the analysis relies on the assumption that the ORES API is an accurate predictor of article quality. If this assumption turns out to be incorrect, the entire analysis breaks down.  -->

### What biases did you expect to find in the data (before you started working with it), and why?

Before analyzing the data, I expected that more developed and affluent countries would have a greater number of articles, as well as higher-quality articles, compared to less developed nations. This assumption was based on the belief that internet access, and consequently access to resources such as Wikipedia, would be less prevalent in less developed countries, leading to fewer total articles and lower-quality content. Furthermore, given that the dataset was derived from English Wikipedia, I anticipated a lower representation of articles on politicians from countries where English is not widely spoken. 


### What (potential) sources of bias did you discover in the course of your data processing and analysis?

While analysing the data, there were several potential sources of bias that were revealed. First was the potential sampling bias, for example, some countries with large populations may not have been adequately represented, as evident from the low total-articles-per-capita scores for many of the most populated countries. There are also several countries that are completely missing from the dataset, such as Australia and Canada. Another potential issue is the under-representation of non-English-speaking countries. Finally, significant bias in the article quality could originate from the ORES API itself. As mentioned before, we are making the assumption that the ORES API is an accurate predictor of article quality. This means that we are not accounting for any kind of bias that the ORES ML models could themselves have. 


### What might your results suggest about (English) Wikipedia as a data source?

The results of this project suggest that English Wikipedia may have significant bias. The dataset seems to favor countries from relatively developed regions of the world, that have greater number of English-speaking populations. These biases need to be taken into account before utilizing the dataset for any kinds of analyses or model training, lest researchers end up introducing and aggravating these biases in their own results. 