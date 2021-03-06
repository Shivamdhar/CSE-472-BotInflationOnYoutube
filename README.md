*Detecting bot-inflated videos on Youtube*

Youtube has emerged as one of the social media platforms for creators to publish content and monetize it through their increasing audience and viewership. In the race of coming in limelight, few creators try to improve the statistics of published content like number of views, subscribers, likes, etc. through automated scripts or bots. This is a concern for two reasons - a) inflated views lead to disparity among the genuine creators, gaining popularity via organic traffic and others resorting to bot inflation for fame, thus abusing the remuneration mechanism b) ad impressions which work only in case of user interactions like clicks, get wasted due to the activity of view bots, taking a toll on the youtube advertisers. Hence, it is important to solutionize the problem by analyzing the social media interactions and penalize the fake popularity seekers for violating the terms of service. This would also help businesses to get finer insights from their consumer base and not get misled by popularity of certain content.  

The project can be run on any OS environment having python 3.5.+ installed. 
Following libraries need to be installed before hand:

requests==2.18.4

ujson==1.35

ijson==2.3

jsonschema==2.6.0

glob2==0.6

cloudpickle==0.5.3

pickleshare==0.7.4

numpy==1.15.4

scipy==1.1.0

nltk==3.3

pandas==0.23.0

Following is the directory structure:

- dataset: Consists of the following directories

		- comments 
			- processed : contains processsed comments scraped in the form of tab separated files (.tsv files)
		
        - dumped_objects
			
            - history.p and model.p : pickle files generated by our implementation of MaxEnt Classifier during training phase
		
        - statistical_analyzer 
			
            - view_bot.csv : contains statistical properties for the videos in the dataset and forms the input for the statistical analyzer
		
        - tweettube_dataset
			
            - 1.json, 2.json, 3.json, 4.json : contains the raw data scraped form TweetTube

		- dump.sql : contains database screenshot containing videos and related statistics

- code: Consists of the following files 
		
        - API_KEY.txt : contains base64 encoded YouTube API key
		
        - MaxEnt.py : implementation of MaxEnt Classifier
		
        - bot_users.py : contains a list of probable bot users on YouTube based on the comments
		
        - constants.py : contains the constants used across the code base eg: file paths and external APIs
		
        - data_scraper.py : contains modules for scraping video statistics and comments and storing it in MySQL DB and .tsv respectively
		
        - engine.py : wrapper class on MaxEnt Classifier which helps in training the model and classifying the test set
		
        - feature_functions.py : contains all the patterns extracted based on bot behaviour observed while parsing the comments dataset
		
        - pre_processor.py : contains code for reducing noise in the comments dataset by making use of punctuation removal and lemmatization techniques
		
        - statistical_analyzer.py : contains logic for identifying view bot inflation based on correlation between view count and metrics like sum of 								likes and dislikes


How to run and test the model:

	(Use the following steps on the pre-processed data)

	1. Data Scraping : python data_scraper.py

	2. View Bot Identification : python statistical_analyzer.py 

	3. Comment Bot Identification 
		
            - Training Phase : python engine.py train
		
            - Testing Phase : python engine.py test