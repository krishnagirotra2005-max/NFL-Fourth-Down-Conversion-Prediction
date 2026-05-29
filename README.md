# NFL Fourth-Down Conversion Prediction

This project builds a machine learning model to predict whether an NFL team will successfully convert a fourth-down attempt. The goal is to use historical NFL play data to estimate conversion probability and support more data-driven football decision-making.

## Project Overview

Fourth-down decisions are one of the most important strategic choices in football. Coaches have to decide whether to attempt a conversion, punt, or kick based on various factors such as field position, yards-to-go, play type, and opponent matchup.

In this project, I trained a classification model to predict whether a fourth-down attempt would be successful using NFL play-by-play data from 2019–2024.

## Dataset

The dataset includes historical fourth-down attempts with the following key variables:

| Variable    | Description                                                                                                                                                                    | Data Type |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------- |
| `converted` | Result of the fourth-down conversion attempt. One of `No` or `Yes`. This is the target variable the model predicts.                                                            | category  |
| `togo`      | Distance in yards from either the first-down marker or the end zone in goal-down situations. This represents the yards needed to successfully convert the fourth-down attempt. | float64   |
| `yardline`  | Distance in yards from the opponent’s end zone. This represents how far the offense is from scoring a touchdown.                                                               | float64   |
| `play_type` | Type of play. One of `Pass` or `Run`. Pass plays include sacks, and run plays include scrambles.                                                                               | category  |
| `posteam`   | Abbreviation for the team with possession of the ball.                                                                                                                         | object    |
| `defteam`   | Abbreviation for the team on defense.                                                                                                                                          | object    |

The data was split using a time-based train/test split:

- **Training data:** 2019–2023 seasons
- **Test data:** 2024 season

This split was chosen because it better reflects real-world deployment, where a model is trained on past games and used to predict future outcomes.

## Methods

The model pipeline included:

- Data preprocessing using `FunctionTransformer`
- Categorical feature handling using `DictVectorizer`
- Classification using `HistGradientBoostingClassifier`
- Model evaluation using accuracy, precision, recall, ROC-AUC, log loss, and a confusion matrix

The final model used the following key features:

- Yards-to-go
- Field position
- Play type
- Offensive team
- Defensive team

## Model Performance

On the held-out 2024 test set, the model achieved:

| Metric | Result |
|---|---:|
| Accuracy | 62.5% |
| ROC-AUC | 0.66 |

The model performed better than random guessing and showed a reasonable ability to distinguish between successful and unsuccessful fourth-down attempts.

## Key Findings

- Fourth-down attempts are most common when teams need only a few yards to convert.
- Field position and yards-to-go are important factors in predicting conversion success.
- The model was better at identifying successful conversions than unsuccessful ones.
- Performance is limited by missing context such as player skill, game situation, injuries, weather, score differential, and coaching tendencies.

## Tools & Technologies

- Python
- Pandas
- Matplotlib
- Scikit-learn
- Jupyter Notebook
- Joblib

## Files

- `NFL Fourth-Down Conversion Prediction.ipynb` - Main notebook containing data loading, preprocessing, model training, evaluation, and discussion.
- `README.md` - Project summary and documentation.

## Conclusion

This project demonstrates how machine learning can be applied to sports analytics and football strategy. While the model should not be used as the only basis for fourth-down decision-making, it provides a useful probability-based perspective that can support deeper analysis.

Future improvements could include adding more game context, such as score, quarter, time remaining, team strength, player-level data, weather, and coaching tendencies.
