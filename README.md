# 2025 TLDR Data Repository

The goal of this repository is to ensure that the datasets for the 2025 TLDR papers are open-source, easily accessible, and reproducible. This repository holds submodules for each of the empirical papers at the TLDR conference, and each submodule contains the repository for each paper with the scripts, schemas for the data, and detailed instructions on how to recreate the datasets used in the papers.

Each repository has a README, which includes an overview of the data, the schema of the dataset, and an implementation guideline on how to utilize the scripts. Included below is a sample schema of an example dataset. When possible/relevant, each of the paper's README will include the information below and detailed instructions on how to work the data pipeline included in the respository.

## Data Schema for TLDR 2025 Repository


**name**: The file name, including the extension (.csv, .json). Names should be concise and have words separated by underscores (_) rather than spaces.

**description**: A concise description of the data, including what type of data it is (on-chain data, price data, etc.), how it was sourced, how it's used in the paper, etc.

**file_type**: The data type of the file. Files should ideally be either .csv, .json, or .parquet type - reach out to the data fellow if your data uses a different format.

**size**: The size of the data file in digital storage units (KB, MB, GB, etc.)

**structure**: The row and column length of the data file. For example, [350, 20] would correspond to 350 rows and 20 columns.

**source**: A quick note on where and how the data was obtained. (e.g., specific API, data provider, or extraction method).

**blockchain**: The chain (or chains) the data is sourced from. If the dataset uses non-blockchain data (e.g. CEX price data), can fill this out with NA.

**variables**: This will be a list of the variables present in the dataset, along with their type and a short description. Variable types should fall into one of the MySQL Data Types - if this causes an issue, please reach out to the TLDR data fellow.

**date_range**: (Optional) For time series data, the earliest and latest data points to indicate the coverage of the dataset. Use the standardized format of YYYY-MM-DD (e.g., "2023-01-01 to 2023-12-31")

**other_notes**: (Optional) Other information that would be useful to know about the dataset, including filters, null values, data cleaning (e.g., "Data was filtered to remove blocks with zero transactions").

## Example Data File Schema:

**name**: ethereum__blocks__20056000_to_20056999.csv

**description**: Includes a subset of the on-chain data returned by the eth_getBlockByNumber RPC Method. Used for identifying the market-share of specific block builders.

**file_type**: .csv 

**size**: 187 KB

**structure**: [1000, 8]

**source**: Extracted using JSON-RPC methods for Ethereum using the cryo data tool.

**blockchain**: Ethereum mainnet

**date_range**: 2024-06-09

**other_notes**: The included columns are a subset of the columns returned by the eth_getBlockByNumber RPC Method.

**variables**:
* **block_hash**: STRING. The unique cryptographic identifier of the Ethereum block.
* **author**: STRING. The hex address of the builder that constructs the block.
* **block_number**: INTEGER. The height of the block on Ethereum.
* **gas_used**: INTEGER. The amount of gas consumed in the block.
* **extra_data**: STRING. The graffiti attached to the block to identify the builder.
* **timestamp**: INTEGER. The UNIX timestamp for when the block was collated.
* **base_fee_per_gas**: INTEGER. The amount of fee burned per gas for all transactions in the block.
* **chain_id**: INTEGER. Unused artifact, equal to 1 throughout the dataset for Ethereum.

The implementation guideline for this example project would be located at the bottom of the README, and would detail how to use the repository to create the dataset. The folder in the data repository for this paper will also include the necessary scripts - for this example, it would be a script which utilizes the cryo data tool to pull on-chain data with the set parameters, and pull the necessary columns. Anyone in the public with an RPC endpoint API key will then be able to recreate the data directly.