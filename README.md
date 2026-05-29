# NFL Fourth-Down Conversion Prediction

This project builds a machine learning model to predict whether an NFL team will successfully convert a fourth-down attempt. The model uses features such as yards-to-go, field position, play type, and team matchup data to estimate the probability of a successful conversion.

The goal of this project is to create a supportive analytics tool that can help evaluate whether attempting a fourth-down conversion is likely to be successful.

## Project Overview

Fourth-down decisions are an important part of football strategy. Teams often have to decide whether to attempt a conversion, punt, or kick based on the game situation.

In this project, I used historical NFL fourth-down attempt data to train a classification model that predicts whether a fourth-down attempt will result in a successful conversion.

## Data Dictionary

| Variable    | Description                                                                                                                                                                       | Type     |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| `converted` | Result of the fourth-down conversion attempt. One of `No` or `Yes`. This is the target variable the model predicts.                                                               | category |
| `togo`      | Distance in yards from either the first-down marker or the end zone in goal-down situations. This represents the distance needed to successfully convert the fourth-down attempt. | float64  |
| `yardline`  | Distance in yards from the opponent’s end zone. This represents the distance needed to score a touchdown.                                                                         | float64  |
| `play_type` | Type of play. One of `Pass` or `Run`. Pass plays include sacks, and run plays include scrambles.                                                                                  | category |
| `posteam`   | Abbreviation for the team with possession of the ball.                                                                                                                            | object   |
| `defteam`   | Abbreviation for the team on defense.                                                                                                                                             | object   |

## Train/Test Split

The dataset was split using a time-based split:

* Training data: 2019-2023 seasons
* Test data: 2024 season

A time-based split was used because it better reflects how a model would be used in the real world: trained on past games and evaluated on future games.

The 2025 data was not used because it had fewer observations compared to the other seasons.

## Model

The final model was built using a Scikit-learn pipeline with:

* `FunctionTransformer`
* `DictVectorizer`
* `HistGradientBoostingClassifier`

The model used the following predictor variables:

* `togo`
* `yardline`
* `play_type`
* `posteam`
* `defteam`

## Model Performance

On the held-out 2024 test data, the model achieved:

| Metric    | Result |
| --------- | -----: |
| Accuracy  |  62.5% |
| Precision |  66.7% |
| Recall    |  69.0% |
| ROC-AUC   |   0.66 |
| Log Loss  |  0.646 |

The model performed better than random guessing and showed a reasonable ability to identify successful fourth-down conversions.

## Key Findings

* The training dataset was relatively balanced, with successful conversions making up about 52% of observations and unsuccessful attempts making up about 48%.
* Most fourth-down attempts occurred when teams needed only a few yards to convert.
* The average yards-to-go value was about 4.17 yards, while the median was 2 yards.
* The model was better at identifying successful conversions than unsuccessful ones.
* Performance was limited because the dataset did not include factors such as player skill, score differential, quarter, time remaining, weather, injuries, or coaching tendencies.

## Tools Used

* Python
* Pandas
* Matplotlib
* Scikit-learn
* Joblib
* Jupyter Notebook

## Files

* `NFL Fourth-Down Conversion Prediction.ipynb` - Main notebook containing the data loading, preprocessing, model training, evaluation, and discussion.
* `README.md` - Project overview and documentation.

## Conclusion

The HistGradientBoosting model performed reasonably well in predicting fourth-down conversion outcomes using field position, yards-to-go, play type, and team matchup data.

While the model should not be fully relied on for fourth-down decision-making, it can be used as a supporting tool for analyzing fourth-down situations. With additional game-context and player-level data, the model's predictive performance could be improved further.
