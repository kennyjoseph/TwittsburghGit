This code is for the website located at http://tinyurl.com/mapTwittsburgh.  Development is in the initial stages.

The social media dataset that we use is from Twitter.  We obtain approximately 120,000 geo-tagged tweets from Pittsburgh and the surrounding areas using TweetTracker (Kumar et al., 2011), a tool that allows one to easily set up a bounding box to capture tweets in a specific area. 

Given a set of tweets, our visualization required that we present a) interesting keywords of tweets occurring in b) different neighborhoods, c) differentiating between tweets of “residents” and “non-residents”.  

In order to parse out keywords from tweets, we use a tokenizer developed specifically for tweets by Gimpel et al. (2011).  The next step was to determine the neighborhood in which the tweet occurred.  In order to do so, we use the R package maptools (Bivand and Lewin-Koh, 2013) to perform a spatial join on the location of each tweet and the neighborhood data obtained from Pittsburgh SNAP, described below.  Having determined the neighborhood that each tweet was from, we could now determine the “home” neighborhood of each user in our dataset.  

We first remove all users having less than 5 tweets, as we suspected that any fewer would result in a highly biased view of a user’s home, while any higher of a threshold removed too much of the data.  Following in the line of previous work (e.g. Cho et al., 2011), the neighborhood in which a user had the most geo-tagged tweets was considered her “home neighborhood”.  Though this definition of home is libel to produce some noise, the heuristic has been shown to be reasonably reliable, and thus seemed like a good step for this project.

As a result of these steps, we now have a set of keywords for each neighborhood, where this set of keywords is split by tweets made by “residents” of that neighborhood and those made by residents of other neighborhoods (“non-residents”).  In order to determine the terms most relevant to a given subset (i.e. resident or non-resident) of a given neighborhood, we treat the set of associated keywords as a document in the form of a bag of words.  We have 2N documents, where N is the number of neighborhoods.  Using this collection of documents, we apply tf-idf weighting to all terms in the corpora, and select the top five terms in each subset of each neighborhood for visualization.


The data used can be found in penn3.js - it is a combination of popular (using tf-idf weighting) unigrams from Twitter data collected from the Gardenhose from early 2013 within Pittsburgh and the surrounding areas, and demographic/neighborhood data from <a href="http://www.pittsburghpa.gov/dcp/snap/">Pittsburgh SNAP</a>. 

brandon_re.tff is a custom font built by Robyn Hammond.  

We also use local copies of leaflet.css and leaflet.js  -these local copies should be removed in future work.

Kumar, Ravi, Mohammad Mahdian, and Mary McGlohon. 2010. “Dynamics of Conversations.” In Proceedings of the 16th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, 553–562. KDD  ’10. New York, NY, USA: ACM. doi:10.1145/1835804.1835875. http://doi.acm.org/10.1145/1835804.1835875.
Cho, Eunjoon, Seth A. Myers, and Jure Leskovec. 2011. “Friendship and Mobility: User Movement in Location-based Social Networks.” In Proceedings of the 17th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, 1082–1090. KDD  ’11. New York, NY, USA: ACM. doi:10.1145/2020408.2020579. http://doi.acm.org/10.1145/2020408.2020579.
Gimpel, Kevin, Nathan Schneider, Brendan O’Connor, Dipanjan Das, Daniel Mills, Jacob Eisenstein, Michael Heilman, Dani Yogatama, Jeffrey Flanigan, and Noah A. Smith. 2011. “Part-of-speech Tagging for Twitter: Annotation, Features, and Experiments.” In Proceedings of the 49th Annual Meeting of the Association for Computational Linguistics: Human Language Technologies: Short Papers - Volume 2, 42–47. HLT  ’11. Stroudsburg, PA, USA: Association for Computational Linguistics. http://dl.acm.org/citation.cfm?id=2002736.2002747.
Bivand, Roger, and Nicholas Lewin-Koh. 2013. Maptools: Tools for Reading and Handling Spatial Objects. http://CRAN.R-project.org/package=maptools.
