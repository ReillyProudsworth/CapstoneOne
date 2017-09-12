Capstone 1 Project proposal

What is the problem you want to solve?

Who is your client and why do they care about this problem? In other words, what will your client DO or DECIDE based on your analysis that they wouldn’t have otherwise?

What data are you going to use for this? How will you acquire this data?
In brief, outline your approach to solving this problem (knowing that this might change later).

What are your deliverables? Typically, this would include code, along with a paper and/or a slide deck.

The problem I'd like to solve is predicting how much a consumer will like a business based on their past experiences.  Businesses across all industries would find it valuable to understand the features which correlate to a good or bad customer experience.

My client is Yelp and they care about making a prediction like this as a tool for recommending businesses to their users.  By prediciting a likely review rating for a business, users could be directed to businesses that partner with Yelp and will most likely give the user a good customer experience.  This would be a marketable feature to grow Yelp's business.

Yelp provided the dataset for this through their website.  The data includes information about businesses, users, and individual reviews, all stored in JSON files. My approach to solving this problem will be to wrangle each data file individually, add features, merge the data into one dataframe, then select and tune a machine learning algorithm using the features created.  This will probaby be done with some from of regression, considering I'm dealing with continuous values and not looking to classify anything.  

Currently I'm aiming to deliver the Python code for my program, a paper explaining my procedure, and a slide deck which will be used to present my findings.   