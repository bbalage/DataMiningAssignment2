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