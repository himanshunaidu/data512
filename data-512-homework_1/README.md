# DATA 512 Homework 1: Wikipedia Rare Disease Article Traffic Analysis

## Project Goal

The goal of this project is to collect, analyze, and publish monthly article traffic data for a set of Wikipedia pages related to rare diseases. The data spans from July 2015 to September 2024, and is gathered from the Wikimedia Analytics Pageviews API. The dataset allows for an analysis of trends in desktop and mobile traffic across various articles over time.

The purpose of this project is also to follow best practices for open scientific research, ensuring reproducibility through transparent documentation, data accessibility, and adherence to licensing standards.

The code for the project is present in the Jupyter notebook [wp_rare_disease_article_views.ipynb](wp_rare_disease_article_views.ipynb)


## License

### Source Data

The source data used in this project is obtained from the Wikimedia Foundation via the [Pageviews API](https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/reference/page-views.html). According to the [Wikimedia Foundation Terms of Use](https://foundation.wikimedia.org/wiki/Policy:Terms_of_Use), the data can be reused, modified, and distributed as long as proper attribution is provided, and the data remains freely accessible.

How the Terms of Use Apply:
- The dataset created in this project is derived from Wikimedia's raw data. As such, it falls under the [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/deed.en) ("CC BY-SA 4.0")
- Attribution: If you use or share this dataset, you must provide attribution to the Wikimedia Foundation. The attribution should include a reference to both the original source of the data (the Wikimedia Foundation) and this project.
- Freely Accessible: The data must remain open and freely accessible to others, as per the terms of the Wikimedia Foundation.

### Access Page View Data

To code for accessing the page view data in [wp_rare_disease_article_views.ipynb](wp_rare_disease_article_views.ipynb) was developed by Dr. David W. McDonald for use in DATA 512, a course in the UW MS Data Science degree program. This code is provided under the [Creative Commons](https://creativecommons.org) [CC-BY license](https://creativecommons.org/licenses/by/4.0/). 

Modifications to this code were made by Himanshu Naidu on October 5, 2024.

## How to Run

The entire code of the project resides in the Jupyter notebook [wp_rare_disease_article_views.ipynb](wp_rare_disease_article_views.ipynb).

In order to run the notebook, start by setting up the Conda environment, using the [data512.yml](data512.yml)

### Environment Setup

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


### Running the Notebook

The notebook does not need any additional configuration. Thus, you can run the code using the 'Run All' option.

The entire code takes ~30 minutes to run on the system used to develop this project, with the main bottleneck being the 'Data Acquisition' step that involves using the pageviews API (that has rate limits).

Note: The system used to develop this project is equipped with a 12th Gen Intel® Core™ i7-12700H processor (2.30 GHz)



## API Documentation

The data is acquired using the [Wikimedia Analytics Pageviews API](https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/reference/page-views.html). The API documentation provides details on how to make requests for pageview data and includes parameters for specifying the time range, article titles, and access type (e.g., mobile, desktop).

## Generated Files

The code generates several data files during its execution.

### Data Files

The data files represent the monthly page traffic for Wikipedia articles related to rare diseases and are stored in JSON format:

1. Monthly Mobile Access:

Filename: [rare-disease_monthly_mobile_201501-202409.json](data/rare-disease_monthly_mobile_201501-202409.json)

Description: This file contains the sum of mobile web and mobile app traffic for each article for each month in the specified date range.

Data Schema:

```
{
  "article_title": [
    {
      "timestamp": "YYYYMMDDHH",
      "project": "string",
      "article": "string",
      "granularity": "string",
      "agent": "string",
      "views": integer
    }
  ]
}
```

2. Monthly Desktop Access:

Filename: [rare-disease_monthly_desktop_201501-202409.json](data/rare-disease_monthly_desktop_201501-202409.json)

Description: This file contains the desktop traffic for each article for each month in the specified date range.

Data Schema: 

```
{
  "article_title": [
    {
      "timestamp": "YYYYMMDDHH",
      "project": "string",
      "article": "string",
      "granularity": "string",
      "agent": "string",
      "views": integer
    }
  ]
}
```

3. Monthly Cumulative Access:

Filename: [rare-disease_monthly_cumulative_201501-202409.json](data/rare-disease_monthly_cumulative_201501-202409.json)

Description: This file contains the sum of all mobile and desktop traffic for each article for each month in the specified date range.

Data Schema: 

```
{
  "article_title": [
    {
      "timestamp": "YYYYMMDDHH",
      "project": "string",
      "article": "string",
      "granularity": "string",
      "agent": "string",
      "views": integer
    }
  ]
}
```


### Plot Files

The plot files are all the plots generated by the [Jupyter notebook](wp_rare_disease_article_views.ipynb)

1. Maximum Average and Minimum Average

Filename: [maximum_average_and_minimum_average.png](plots/maximum_average_and_minimum_average.png)

Description: This plot contains time series for the articles that have the highest average page requests and the lowest average page requests for desktop access and mobile access over the entire time series.

2. Top 10 Peak Page Views

Filename: [top_10_peak_page_views.png](plots/top_10_peak_page_views.png)

Description: This plot contains time series for the top 10 article pages by largest (peak) page views over the entire time series by access type.

3. Fewest Months of Data

Filename: [fewest_months_of_data.png](plots/fewest_months_of_data.png)

Description: This plot contains pages that have the fewest months of available data.


## Known Issues

The code for accessing the page views data, as developed by Dr. David W. McDonald failed to work for certain diseases, due to failure in encoding the '/' character in the disease names (such as 'Trimethoprim/sulfamethoxazole'). Thus the encoding had to be done in safe mode. 

Original Code:
```
urllib.parse.quote(request_template['article'].replace(' ','_'))
```

Modified Code (by Himanshu Naidu):
```
urllib.parse.quote(request_template['article'].replace(' ','_'), safe='')
```


## Special Considerations

- API: The pageviews API may undergo changes, which could affect the data consistency for the given time period. 

- Data Completeness: Some articles may have incomplete data for certain months, particularly articles created after July 2015 or deleted before September 2024.

- Access Type Considerations: The Wikimedia Pageviews API separates mobile web and mobile app access, and these are combined into a single mobile category in this project.