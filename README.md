# university-public-library-dataset
Documentation, example scripts, and reproducibility materials accompanying an anonymized university and public library dataset for research on recommender systems, data sparsity, and cold-start recommendation.
# University and Public Library Recommendation Dataset for Sparse and Cold-Start Research

## Overview

This repository provides the documentation, example code, and reproducibility materials accompanying the dataset:

**University and Public Library Recommendation Dataset for Sparse and Cold-Start Research**

The dataset contains anonymized user borrowing transactions and associated metadata collected from university and public library environments in Indonesia. It is intended to support research in recommender systems, data sparsity, cold-start recommendation, digital libraries, user behaviour analysis, information retrieval, and machine learning.

The authoritative dataset is publicly deposited in Mendeley Data, Version 1:

-   Dataset:https://data.mendeley.com/datasets/6rd45bvxjy/1
-   DOI: https://doi.org/10.17632/6rd45bvxjy.1
-   License: CC BY 4.0
-   Published: 8 July 2026

The GitHub repository is intended to provide documentation and code associated with the dataset. The dataset itself should be accessed from Mendeley Data.

------------------------------------------------------------------------

## Dataset Summary

  ------------------------------------------------------------------------
  Dataset |               Users  |      Library Items  |  Borrowing Interactions  |  Initial Sparsity
                                             
  ------------        ------------- --------------   ----------------------    ----------------
  University Library |   14,148  |       8,369  |        52,394    |               99.97%
                                                   

 Public Library   |   53,008   |      54,563  |       406,170    |              99.98%
                                                    

The datasets exhibit characteristics commonly observed in real-world library recommendation environments, including:

-   Extreme user--item interaction sparsity
-   Cold-start users and items
-   Heterogeneous user and item metadata
-   Long-tail borrowing behaviour
-   Borrowing-based rather than explicit-rating interactions

------------------------------------------------------------------------

## Dataset Structure

Each library dataset contains three interconnected data domains:

1.  User Data
2.  Borrowing Transactions
3.  Item Data / Bibliographic Metadata

The three components are linked through anonymized user and item identifiers.

``` text
USER DATA
   |
   | UserId
   v
BORROWING TRANSACTIONS
   |
   | BookId
   v
ITEM DATA / BIBLIOGRAPHIC METADATA
```

### User Data

User data contain anonymized user attributes that can be used as auxiliary information for recommendation modelling. Depending on the library environment, the data include demographic and academic characteristics.

### Borrowing Transactions

Borrowing data represent historical user--item interactions. Each transaction connects an anonymized user identifier with an anonymized library-item identifier and includes transaction-related information such as borrowing and return dates.

### Item Data

Item data contain bibliographic and collection metadata describing library resources. These attributes can support content-based
recommendation, metadata-enhanced recommendation, and cold-start research.

------------------------------------------------------------------------

## Relationships Among Dataset Files

The data components are related through common identifiers:

-   `UserId` links borrowing transactions to the corresponding user record.
-   `BookId` links borrowing transactions to the corresponding item record.
-   Borrowing transactions therefore form the interaction layer between users and library items.

Conceptually:

``` text
+------------------+
|    USER DATA     |
|------------------|
| PK: UserId       |
| User attributes  |
+--------+---------+
         |
         | UserId
         v
+------------------+
|    BORROWING     |
|------------------|
| FK: UserId       |
| FK: BookId       |
| Borrowing Date   |
| Return Date      |
| Borrow Duration  |
+--------+---------+
         |
         | BookId
         v
+------------------+
|    ITEM DATA     |
|------------------|
| PK: BookId       |
| BIBID            |
| ISBN             |
| Book Title       |
| Author           |
| Publisher        |
| Published Year   |
| DDC Number       |
| Location Code    |
+------------------+
```

`UserId` and `BookId` in the released data are anonymized identifiers and should not be interpreted as the original institutional identifiers.

------------------------------------------------------------------------

## Variable Definitions

### User Data

The University Library user data include the following variables:

  ---------------------------------------------------------------------------
  Variable                    Data Type               Description
  --------------------------- ----------------------- -----------------------
  `UserId`                    String                  Anonymous unique
                                                      identifier for a
                                                      library user

  `Membership Type`           Categorical             Type of library
                                                      membership

  `Gender`                    Categorical             Gender category

  `Place of Birth`            String                  User's place of birth

  `Date of Birth`             Date                    User's date of birth

  `Join Year`                 Integer                 Year the user became a
                                                      library member

  `Academic Year`             Integer                 Academic year
                                                      associated with the
                                                      user

  `Program Code`              Categorical/String      Code representing the
                                                      academic program

  `Department Code`           Categorical/String      Code representing the
                                                      academic department

  `Cumulative GPA`            Float                   Cumulative grade point
                                                      average

  `Total Credit Cumulative`   Integer                 Cumulative academic
                                                      credits
  

The exact variables available may differ between the University Library and Public Library datasets. Researchers should inspect the downloaded files before analysis.

### Borrowing Transactions

The borrowing data include transaction-level variables such as:

  --------------------------------------------------------------------------
  Variable                   Data Type               Description
  -------------------------- ----------------------- -----------------------
  `UserId`                   String                  Anonymous identifier
                                                     linking the transaction
                                                     to a user

  `BookId`                   String                  Anonymous identifier
                                                     linking the transaction
                                                     to an item

  `Borrowing Date`           Date                    Date on which the item
                                                     was borrowed

  `Return Date`              Date                    Date on which the item
                                                     was returned

  `Borrow Duration (days)`   Integer                 Duration of the
                                                     borrowing period in
                                                     days

  `Trx at the year of`       Integer                 Year/study-year information associated with the transaction

### Item Data

The item metadata include bibliographic and collection attributes such as:

  -----------------------------------------------------------------------
  Variable                Data Type               Description
  ----------------------- ----------------------- -----------------------
  `BookId`                String                  Anonymous unique
                                                  identifier for a
                                                  library item

  `BIBID`                 String                  Bibliographic record
                                                  identifier

  `ISBN`                  String                  International Standard
                                                  Book Number, where
                                                  available

  `Book Title`            String                  Title of the library
                                                  item

  `Author`                String                  Author information

  `DDC Number`            String                  Dewey Decimal
                                                  Classification number

  `Published Year`        Integer                 Publication year

  `Publisher Name`        String                  Publisher information

  `Location Code`         Categorical/String      Library collection or
                                                  location code

Identifiers such as `UserId`, `BookId`, `BIBID`, `ISBN`, and classification codes should be treated as identifiers or categorical values rather than continuous numerical variables.

------------------------------------------------------------------------

## Data Collection and Preparation

The datasets were extracted from the management systems of the participating university and public libraries.

Data inclusion and exclusion were determined during data collection based on domain-expert assessment of the relevance of available attributes and records to the research objectives. Relevant borrowing transactions, user information, and bibliographic metadata were included, while irrelevant attributes and records that did not meet the defined data requirements were excluded.

The preparation process included:

1.  **Domain-expert feature selection**\
    Available attributes were reviewed by domain experts, and features relevant to library users, borrowing transactions, and bibliographic information were selected.

2.  **Data cleansing**\
    Duplicate, incomplete, invalid, or inconsistent records were identified and removed or handled as appropriate.

3.  **Feature transformation**\
    Categorical variables were transformed into numerical representations when required for machine-learning applications. One-Hot Encoding was used for categorical feature transformation.

4.  **Metadata integration and validation**\
    User data, borrowing transactions, and item metadata were integrated using unique user and item identifiers and subsequently validated.

------------------------------------------------------------------------

## Anonymization and Privacy Protection

All personally identifiable information was removed or anonymized before public release. Original user identifiers were replaced with anonymous identifiers. Personal information that could directly identify individual users was excluded from the released dataset. Item and location identifiers were also anonymized where necessary.

The anonymization process preserves the relationships among users, transactions, and library items while preventing direct identification of individual users.

The datasets are provided exclusively for research and educational purposes and should be used in accordance with applicable ethical, privacy, and data-protection requirements.

------------------------------------------------------------------------

## Interaction Matrix

Borrowing transactions can be transformed into a user--item interaction matrix.

For a binary interaction representation:

``` text
R(u,i) = 1  if user u borrowed item i
R(u,i) = 0  otherwise
```

where:

-   `u` represents a unique user;
-   `i` represents a unique library item; and
-   `R` represents the user--item interaction matrix.

The resulting initial interaction matrix is referred to as **R0** in the accompanying research work.

The original matrices are extremely sparse:

-   University Library: **99.97%**
-   Public Library: **99.98%**

The borrowing data can therefore be used to investigate recommendation under sparse and cold-start conditions.

------------------------------------------------------------------------

## Recommended Research Tasks

The dataset can support research involving:

### Recommender Systems

-   Collaborative filtering
-   Content-based recommendation
-   Hybrid recommendation
-   Metadata-enhanced recommendation
-   Deep learning-based recommendation

### Sparse and Cold-Start Recommendation

-   Recommendation under extreme interaction sparsity
-   New-user recommendation
-   New-item recommendation
-   User--item interaction reconstruction
-   Evaluation of sparsity-reduction techniques

### User and Collection Analysis

-   User borrowing behaviour analysis
-   Collection usage analysis
-   User--item interaction analysis
-   Bibliographic similarity analysis
-   Library analytics

### Benchmarking

The datasets can be used to compare recommendation approaches using standard ranking metrics such as:

-   Precision@K
-   Recall@K
-   F1-score@K
-   MAP
-   NDCG

Researchers may also compare performance across university and public library environments.

------------------------------------------------------------------------

## Example Usage with Python

The following example illustrates the general workflow for loading and connecting the three data components.

``` python
import pandas as pd

# Replace the filenames below with the actual filenames
# downloaded from Mendeley Data.

# Replace with the actual downloaded dataset filename
df = pd.read_csv("YOUR_DATA_FILE.csv")

print("Dataset shape:", df.shape)
print(df.head())
```

### Constructing a Binary User--Item Matrix

``` python
interaction_matrix = pd.crosstab(
    borrowing["UserId"],
    borrowing["BookId"]
)

interaction_matrix = (interaction_matrix > 0).astype(int)

print("Users:", interaction_matrix.shape[0])
print("Items:", interaction_matrix.shape[1])
```

Researchers should adjust the filenames and column names if the downloaded files use different names or formats.

------------------------------------------------------------------------

## Reproducibility

The GitHub repository is intended to provide supporting scripts and examples for reproducible use of the dataset.

The repository organization:

``` text
.
├── README.md
├── scripts/
│   ├── 01_UnivLib_DIB.py
│   ├── 02_PublicLib_DIB.py

```

The actual scripts included in the repository may vary according to the analyses provided by the authors.

The complete dataset remains available from Mendeley Data rather than being duplicated in this GitHub repository.

------------------------------------------------------------------------

## Important Considerations and Limitations

Researchers should consider the following limitations when using the dataset:

1.  The datasets originate from two library environments and may not represent all library contexts or geographic regions.
2.  The interaction matrices exhibit extreme sparsity.
3.  The datasets represent observed borrowing behaviour rather than explicit user ratings.
4.  The absence of a borrowing interaction should not automatically be interpreted as an explicit negative preference.
5.  Personally identifiable information has been removed or anonymized.
6.  Additional behavioural information, such as search logs, browsing histories, reservation records, or recommendation feedback, is not included in the released datasets.
7.  Some attributes may contain missing values because the datasets reflect records from operational library management systems.

------------------------------------------------------------------------

## Dataset License

The dataset is distributed under the **Creative Commons Attribution 4.0
International (CC BY 4.0)** license.

Users may reuse the dataset in accordance with the terms of the license
and should provide appropriate attribution.

------------------------------------------------------------------------

## Citation

Please cite the dataset as:

> Ibrahim, I., Heryadi, Y., Qomariyah, N., & Budiharto, W. (2026).
> *University and Public Library Recommendation Dataset for Sparse and
> Cold-Start Research* (Version 1) \[Data set\]. Mendeley Data.
> https://doi.org/10.17632/6rd45bvxjy.1

### BibTeX

``` bibtex
@misc{Ibrahim2026LibraryDataset,
  author       = {Irma Irawati Ibrahim and Yaya Heryadi and
                  Nunung Qomariyah and Widodo Budiharto},
  title        = {University and Public Library Recommendation Dataset
                  for Sparse and Cold-Start Research},
  year         = {2026},
  publisher    = {Mendeley Data},
  version      = {1},
  doi          = {10.17632/6rd45bvxjy.1},
  url          = {https://doi.org/10.17632/6rd45bvxjy.1},
  note         = {Data set}
}
```

------------------------------------------------------------------------

## Data Availability

The dataset is publicly available from Mendeley Data:

**Mendeley Data:**\
https://data.mendeley.com/datasets/6rd45bvxjy/1

**DOI:**\
https://doi.org/10.17632/6rd45bvxjy.1

**Version:** 1

**License:** CC BY 4.0

------------------------------------------------------------------------

For questions concerning the dataset or associated materials, please refer to the corresponding author information provided in the associated Data in Brief article and the Mendeley Data record.
