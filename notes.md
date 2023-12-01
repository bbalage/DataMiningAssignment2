# Steps

## Dataset
- Weather_Data.csv
    - Bangladesh weather history;
    - https://www.kaggle.com/datasets/apurboshahidshawon/weatherdatabangladesh/
    - 3271 sor, 21 sor
    - Adathalmaz dátum szerint rendezve adott

## Cleansing
Needed to remove string typed data.

### Date
- Date in the following format: dd-mm-yy.
- Start date is easily retrievable: 2013.02.01.
- Since the dataset is ordered by dates, and every row is one day, we could drop the dates.
- Quick sanity check before dropping: the difference between first and last date in days should be equal to the number of rows minus one.
- The sanity check is satisfied, so the date is dropped.

### RainToday
- Either Yes or No.
- Should be converted to 1 and 0 respectively.
- According to the website it should be interpreted as "Is today rainy".
- Upon closer observation it does not reflect whether it actually rained that day: the column "Rainfall" tells us how many millimeters of rainfall happened that day, and it does not unambigously correlate to RainToday column.
- New columns is added to remove string: IsTodayRainy; its values are loaded according to Yes and No with ones and zeros.
- RainToday is dropped.

## Wind directions
- Wind directions are in the format of SSE, S; where SSE = South, South-East.
- These strings must be made numerical.
- Each wind direction column (WindGustDir, WindDir9am, WindDir3pm) are separated into 4 distinct columns, with the following logic.
- Each new column represents a direction (north, south, west, east), and contains a value between 0 and 1.
- If the blows into a direction it is set to 1, else zero. If it blows South, South-East, then south is set to 2, and east to 1, then they both get normalized.

## Fitting bell curve to some values
- Bell curve fits well to some values, moderately to others, terribly to some.
- Well: Rainfall; Moderately: MinTemp; Terribly: Cloud3pm, Cloud9am
- Bell curv is not fitted to the generated values; wind directions and yes/no numerization.

## Creating box plot for those values
- It becomes visible that there are lots of outliers.
- For example, rainfall contains the most of them (most days there are no rain at all).
- However, none ofthe outliers seemed unreasonable; there are high temperatures, but within reasonable limits.
- These informations could be useful for rain predictions.

## Correlation
- Creating the correlation heatmap, some observations can be taken.
- There are obvious correlations, like between the temperatures in 9am and 3pm; they are related.
- Also obvious are the inverse correlations, like between cloud and sunshine.
- There are also non-correlating data members, like air pressure and wind directions.