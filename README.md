Gathering, Cleaning, and Analyzing WeRateDogs Twitter Archive
=================================================

**To view the project [click here](https://kennethacurtis.github.io/weratedogs_analysis/)**

**To download the data used in this project [click here](https://drive.google.com/open?id=1hCfzhchyzwMtMQC3Ygv68k0e8giYemht)**

# Introduction

This dataset comes from an archive of tweets from the Twitter user @dog_rates, also known as WeRateDogs. This account rates people's dogs along with a humorous comment about the dog. The dog then gets a rating that almost always has a denominator of 10. The numerators on the other hand, almost always go beyond 10, [because they're good dogs Brent](https://knowyourmeme.com/memes/theyre-good-dogs-brent). The account has over 7 million followers as of 2018. In this notebook, I will wrangle, clean, and analyze the twitter archive and other supporting data.

### The Process

The data for this project requires gathering from a few different sources. The twitter archive, `df_twitter`, comes from a file given to Udacity by WeRateDogs. The other file, `image_predictions` comes from Udacity's servers and will be downloaded by utilizing the `requests` library. All other data will be gathered by accessing the Twitter API and extracting the JSON of each tweet. I will then use the extracted JSON to add extra data to `df_twitter`. I also use the `BeautifulSoup` library to extract users that were tagged in the photos of the tweet. Once I gather all the data I need, I will clean and visualize it.

### Twitter Archive

The archive was downloaded using [this link](https://d17h27t6h515a5.cloudfront.net/topher/2017/August/59a4e958_twitter-archive-enhanced/twitter-archive-enhanced.csv). In the table there are a total of 17 columns. Most of these columns are described on the [twitter developer web page](https://developer.twitter.com/en/docs/tweets/data-dictionary/overview/tweet-object.html) on tweet objects.

### Image Predictions

This file was downloaded using [this link](https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv) and the `requests` library to save the file for analysis. The column descriptions are as follows:

* tweet_id is the last part of the tweet URL after "status/" → https://twitter.com/dog_rates/status/889531135344209921
* p1 is the algorithm's #1 prediction for the image in the tweet → golden retriever
* p1_conf is how confident the algorithm is in its #1 prediction → 95%
* p1_dog is whether or not the #1 prediction is a breed of dog → TRUE
* p2 is the algorithm's second most likely prediction → Labrador retriever
* p2_conf is how confident the algorithm is in its #2 prediction → 1%
* p2_dog is whether or not the #2 prediction is a breed of dog → TRUE
* etc.
