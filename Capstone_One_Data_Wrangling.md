Capstone One Data Wrangling

The Yelp data is in three files: yelp_academic_dataset_business.json, yelp_academic_dataset_user.json, and yelp_academic_dataset_review.json or Business, User, and Review, respectively.  The first hurdle is reading the data into Python and doing so within the constraints of my computer hardware.  Business and User are both small enough to be read in directly using Pandas.  Reviews on the otherhand is huge and needs to be read in line by line to avoid a memory error.  Reading in Business and User was a bit of a trick because they have an additonal line of whitespace at the end of each document and all the data was stored on one line.  Using this:

pd.read_json('yelp_academic_dataset_business.json', lines = True)

worked great and allowed the data to be directly added to a Pandas Dataframe.  Reading in Reviews required more doing and was ultimately much less flexible.  I had to open the Reviews file, read in the file with proper encoding, and then iterate through the file to grab a desired number of reviews.  This required a hard code of the number of reviews to use which could lead to scalability/sampling issues down the road, plus it is compuationally expensive.  The code used is below:

filename = "yelp_academic_dataset_review.json"
infile = open(filename,"r",encoding='utf-8')

df = pd.DataFrame([])
count = 0

##Need to read in JSON objects one at a time, append to dataframe, and avoid killing memory
for row in infile:
    data = json.loads(row)
    df = df.append(pd.DataFrame({'user_id':data["user_id"], 'business_id':data["business_id"], 'stars':data["stars"], 
                                 'date':data["date"]}, index=[0]), ignore_index=True)
    count = count + 1
    if count == 50000:
        break

After the data is each in it's own notebook, Exploratory Data Analysis (EDA) and data wrangling can begin.  One of the first hiccups I found that there were times when a user had left a review before they joined yelp!  This is obviously bizarre/impossible and the cause of this error isn't clear, however it is an extremely small population of the overall data set, less than 0.1%, so I chose to exclude them.  One common characteristic amongst the data points I saw was that they were located in Europe which might warrant further exploration at another time if Yelp is unaware of the situation already.  Continuing the EDA I found that some of the businesses didn't have categories attached, which would pose a problem when attempting to make dummy variables from the contents.  Again this was a very small percentage, roughly 300 out of 140,000, so they were exluded.  In both situations the data was excluded from the Dataframe by masking, using some boolean logic to create a Series of True/False then subsetting the rows of the Dataframe with that Series:

category_df = business_df[pd.notnull(business_df.categories)]

this returns a Dataframe with the rows from business_df that have categories.  With this wrangling done, I was able to move on to creating dummy variables for the category contents.  Fortunately, no further data wrangling was necessary and moving on to building a good predictive model was possible!




