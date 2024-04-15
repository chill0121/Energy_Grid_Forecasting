# TODO List

**General Tasks**
- [] Add data info and processing info to README.
- [] Altair for EDA.
- [X] Find a home for the datasets. (Too large for github)
    - [X] Compressed data.
- [] Set/describe evaluation horizons (short-term, long-term, etc).
- [] Write introduction.
    - [] What is the problem / Why is it important?
    - [] Related work.
    - [] Find or analyze historical power demands.
- [] Connect with PJM api?
- [] Section about data leakage. (Split location, etc)
- [] Address COVID's role in forecasting.
    - [] Be mindful of the test split and COVID dates.
- [] Feature engineering
    - [] Encode Days of Week
    - [] Encode Month
- [] Explore system-wide forecasts vs more granular region forecasts.
    - [] Individual forecasts for zones then add them?
    - [] Shift data for timezone differences?
- [] Create separate a function file for EDA, results, ect.
- [] Rename columns for consistency.
- [] Instead of replacing outliers with median, try without entirely.
- [] Remove any rows with NaNs resulting from lag features?