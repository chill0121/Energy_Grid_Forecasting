# TODO List

**General Tasks**
- [] Add data info and processing info to README.
- ~~[] Altair for EDA.~~
- [X] Find a home for the datasets. (Too large for github)
    - [X] Compressed data.
- [] Set/describe evaluation horizons (short-term, long-term, etc).
- [] Write introduction.
    - [] What is the problem / Why is it important?
    - [] Related work.
    - [] Find or analyze historical power demands.
- ~~[] Connect with PJM api?~~
- [X] Section about data leakage. (Split location, etc)
- [X] Address COVID's role in forecasting.
    - [X] Be mindful of the test split and COVID dates.
- [X] Feature engineering
- [] Rename columns for consistency.
- [X] Instead of replacing outliers with median, try without entirely.
- [X] Remove any rows with NaNs resulting from lag features.
- [] Model Ablations to test feature importance and cross-validate.
- [X] Remove leap year day? (Just in validation for now)
- [] 1H to 6H
- [] Describe tradeoffs between each model and horizon.