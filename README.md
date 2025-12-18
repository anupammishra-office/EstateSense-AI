**code**

1. `image_getter.py` - class for easily getting an image url for a Zillow listing
2. `learn_preferences.py` - the guts of the recommender system 
3. `load_transform.py` - class for loading data from MongoDB and transforming it for processing
4. `pre_processing.py` - class to transform, normalize, and prep data for the recommender
5. **pipeline**
  1. `get_schools.py` - a class to scrape school data for a given listing and transform it to a Pandas df
  2. `walkscore_api.py` - a class to query WalkScore for walkability and public transit data, and update MongoDB
  3. `web_scraping.py` - a class that streamlines scraping Zillow search results to obtain addresses of listings
  4. `zillow_api.ipynb` - an iPython notebook that I use for querying the Zillow API, need to convert to a script 

**data**

1. `san_fran.csv` - a csv of zillow listings that I scraped
2. `seattle_schools.txt` - a list of all Seattle area schools and their scores from 1-10
3. **seattle**
  1. `seattle.csv` - a csv of aggregated zillow listings that I queried through the API
  2. `bellevue-WA.csv` - a csv of address and home ids that I scraped from Zillow search results
  3. `wallingford-seattle-WA.csv` - a csv of address and home ids that I scraped
  4. etc, other csv files for each of the major neighborhoods and surrounding towns
 
### Overview

This recommender system is -- at the core -- a content based information retrieval system. Recommendations are made based on the notion of computing a measure of similarity between different listings. A content based recommender is different from a collaborative based recommender because the latter relies on the ratings of other users to make recommendations to a new user. 


## How the recommender works 
![alt text](https://github.com/anupammishra-office/EstateSense-AI/blob/master/data/algorithm.png)

Recommendations are shown two at a time and the user is able to pick the one they like best. The user's choice is recorded and then used to update a probabilistic "guess" of what measure of similarity is providing the best recommendations for that user. I am intent on the idea of only showing listings two at a time for one particular reason -- humans are notoriously bad at making value judgements from multiple choices when the number of choices exceeds four to five. We are, however, exceptionally good at making pairwise value comparisons. In general, people can quickly take a look at two things and tell you which is better or more preferable. The downside to this approach is that the user may have to choose listings over a large number of iterations of the algorithm before a high degree of confidence is obtained for the best distance metric.
