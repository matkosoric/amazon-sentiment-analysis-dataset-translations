# Amazon sentiment analysis dataset translations

This repository contains translations of a 150 000 randomly selected entries from Amazon dataset originally created by Julian McAuley and Jianmo Ni, containing over 20GB of data.
The goal is to create smaller datasets for sentiment analysis on languages other than English, for which there are many publicly available datasets already.
Original text values have been sanitized from double quotes characters.
English original with 150k entries is in **aws_sentiment_input.zip**.
Column **sentiment_score** indicates review attitude for particular item on a scale from negative (1) to positive (5).
Two columns that can be used for model training are **summary** and **reviewtext**.
Original column **overall** is renamed to **sentiment_score**.
In order to join translations with original, you can use **original_id** column in translation dataset.
Data is probably skewed in terms of Amazon's shopping category, for which there is no indicator, but it is not skewed regarding sentiment score distribution.
Each sentiment category on a scale from one to five contains slightly more than 30k entries.
Translation is performed with Microsoft Azure's [Translator](https://azure.microsoft.com/en-us/services/cognitive-services/translator/) cloud service.


The easiest way of transforming parquet files to csv in Python is probably with Pandas:

```
import pandas as pd
df = pd.read_parquet('aws_spanish.parquet')
df.to_csv('aws_spanish.csv')
```


Sentiment score distribution view from PowerBI:
![AWS Spanish Translation](https://raw.githubusercontent.com/matkosoric/amazon-sentiment-analysis-dataset-translations/master/sentiment_distribution.PNG?raw=true "")


Review date from PowerBI:
![AWS Spanish Translation](https://raw.githubusercontent.com/matkosoric/amazon-sentiment-analysis-dataset-translations/master/date_distribution.PNG?raw=true "")


In case you want to import data to Postgres, here is DDL:

```
CREATE TABLE "amazon-sentiment".aws_spanish (
    id int8 NULL,
    summary varchar NULL,
    sentiment_score int4 NULL,
    reviewtext varchar NULL,
    id_original int8 NULL,
    reviewername varchar NULL,
    reviewerid varchar NULL,
    asin varchar NULL,
    helpful varchar NULL,
    unixreviewtime int4 NULL,
    reviewtime date NULL
);
```

View in DBeaver:

![AWS Spanish Translation](https://raw.githubusercontent.com/matkosoric/amazon-sentiment-analysis-dataset-translations/master/aws_spanish.PNG?raw=true "")


Original source of data:

[Amazon product data - 2014 version](https://jmcauley.ucsd.edu/data/amazon/)

[Amazon Review Data - 2018 version](https://nijianmo.github.io/amazon/index.html)

