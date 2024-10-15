# DATA 512 Homework 2: Considering Bias in Wikipedia Politicians Data

## Project Goal

This goal of this project is to explore bias in data using Wikipedia articles about political figures from different countries. The analysis aims to examine the coverage of politicians on Wikipedia and the quality of articles about politicians across nations. 

The code for the project is present in the Jupyter notebook [wikipedia_politician_bias.ipynb](wikipedia_politician_bias.ipynb)


## License

### Source Data

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


