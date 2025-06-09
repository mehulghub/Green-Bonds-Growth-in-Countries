#  Green Bonds Market Analysis and Event Study Methodology

This repository contains Python code that implements a methodological framework for analyzing the green bonds market and conducting an event study to assess the impact of specific events on related financial assets. The project focuses on demonstrating data handling, market segmentation analysis, and a robust event study methodology using the Market Model.

## Theoretical Framework

The analysis and event study conducted in this project are grounded in established financial and statistical theories:

1.  **Green Bonds Market Analysis:** The initial phase involves descriptive analysis of the green bonds market. This includes:
    *   **Market Segmentation:** Examining issuance activity by entity (issuer) and geographic region (country). This helps to identify key players and centers of activity within the green bond landscape.

2.  **Event Study Methodology:** The event study component follows the standard procedure to determine if an event has a statistically significant impact on a firm's stock returns. The core concepts include:
    *   **Event Definition:** Identifying a specific, discrete event (e.g., a green bond issuance announcement, a policy change) whose impact is to be assessed.
    *   **Event Window:** Defining a period around the event date during which abnormal returns are hypothesized to occur[-5 days,+5 days] of the Green Bond issuance date.
    *   **Estimation Window:** Defining a period prior to the event window, free from the event's influence, used to model the normal relationship between the firm's return and the market return(In my case 45 days before Green Bond issuance date).
    *   **Normal Performance Model (Market Model):** This study utilizes the Market Model, a widely used econometric approach. It assumes a linear relationship between the return of an individual security and the return of a market index. The model is estimated using ordinary least squares (OLS) regression on data from the estimation window:
         R(it) = alpha_i + beta_i* R(mt) + epsilon(it)
        Where:
        *   $R(it)$ is the return of security *i* at time *t*.
        *   $R(mt)$ is the return of the market index at time *t*.
        *   $alpha_i$ and $beta_i$ are the estimated parameters representing the security's intercept and sensitivity to market movements, respectively.
        *   $epsilon(it)$ is the error term, representing the unexplained portion of the security's return.
    *   **Expected Return Calculation:** Using the estimated $alpha_i$ and $beta_i$ from the estimation window, the expected return for the firm during the event window is calculated based on the actual market returns during that period.
    *   **Abnormal Return (AR) Calculation:** The abnormal return for each day in the event window is the difference between the actual return of the firm and its expected return based on the Market Model:
        AR_(it) = R_(it0 - (\hat{\alpha}_i + \hat{\beta}_i R_{mt})
    *   **Cumulative Abnormal Return (CAR):** The CAR is the sum of the abnormal returns over the entire event window. It provides an aggregate measure of the event's impact.
        $$ CAR_i = \sum_{t=T_1}^{T_2} AR_{it} $$
        Where $T_1$ and $T_2$ are the start and end dates of the event window.
    *   **Significance Testing:** Statistical tests are performed on the abnormal returns to determine if they are statistically different from zero. This project includes:
        *   **Normality Test (Shapiro-Wilk):** Assesses whether the abnormal returns are normally distributed, which is an assumption for parametric tests like the t-test.
        *   **Parametric t-test:** Tests the null hypothesis that the mean abnormal return is zero.
        *   **Non-Parametric Chi-Square Test:** Examines the distribution of positive versus non-positive abnormal returns to see if it deviates significantly from a 50/50 split, providing a test of location that does not assume normality.

## Implementation Details

The theoretical concepts described above are implemented in Python using the `GreenBondsAnalyzer` class. Key libraries utilized include:

-   `pandas` for data manipulation and analysis.
-   `openpyxl` for reading Excel files.
-   `matplotlib` and `seaborn` for data visualization.
-   `yfinance` for fetching historical stock and market data.
-   `numpy` for numerical operations.
-   `statsmodels` for statistical modeling, specifically OLS regression.
-   `scipy.stats` for statistical tests (Shapiro-Wilk, t-test, Chi-square).

The code structure within the `GreenBondsAnalyzer` class reflects the workflow from data ingestion and preprocessing to market analysis and the event study execution, including the necessary statistical tests.

## Usage

To utilize the code and replicate the analysis:

1.  Ensure all required Python libraries are installed.
2.  Provide your green bonds data in the specified Excel and CSV formats.
3.  Update the exchange rates dictionary with relevant values.
4.  Define the parameters for the event study (firm ticker, market ticker, event date, and window dates) based on the specific event you wish to analyze.
5.  Run the Python script.

The output will include detailed information at each stage of the analysis, from data cleaning results to regression outputs, calculated abnormal returns, CAR, and the results of the significance tests. Visualizations are generated to illustrate market issuance trends and the distribution of abnormal returns.

## Further Research

This framework can serve as a basis for more advanced research in green finance and event studies, including:

-   Analyzing the impact of different types of green bond issuances (e.g., by use of proceeds, sector).
-   Comparing the market reaction to green bond events versus conventional bond events.
-   Investigating the long-term impact of green bond issuance on firm value and environmental performance.
-   Applying alternative event study models (e.g., Constant Mean Return model, Market Adjusted Return model).
-   Conducting cross-sectional analysis of abnormal returns to identify factors influencing the market reaction.

## Contributing

Contributions to enhance the theoretical depth, add more sophisticated analysis techniques, or improve the code implementation are welcome.
