twitter_search: 
	search reference and referrers’ information of YouTube videos on Twitter;
	search information of YouTube channel publishers on Twitter;
	process raw data


process:
	read_data(): 
		Read channel and video data from JSON files
	clean_data(V): 
		Clean video data (10 videos without stat and snippet are discarded)
	video_sum(V): 
		Get info of videos, Get mapping from channel to video
	channel_sum(Cdata, VC_dict): 
		get info of sampled channels
	Clustering(C, K): 
		Apply KMeans clustering on channel data and return statistics of clustering result, K is number of clusters
	PCA(C_stat, C): 
		Get the PCA representation of quantitation of channel popularity
	Cgen(C, C_stat, C_des, C_title, C_pubtime, V_stat, V_comm, VC_dict):
		Generate part of channel features including (as matrix mat):
			Duration, video publishing frequency
			Ratio of subscriber/view, comment/view
			Sentiment anaylysis result: positive/negative/neutral/compound sentiment scores
		Generate response vector y according to clustering result:
			cluster1: [0, 850000000], cluster2:[850000000, 3700000000], cluster3[3700000000, infinity]
	Vgen(V_stat, VC_dict):
		Aggregate the video statistics for each channel including:
			Ratio of like/dislike, comment/view, favorite/view
	cat_dummy(VC_dict, V_catId, V_stat):
		Process and aggregate the category info of videos of a channel as dummy variable (44 categorys, 43 dummy variables)
	ref_scores():
		Compute the referrer scores for each channel: sum(sum of each video's referrer's followers/1000.0)
	socialmedia(C):
		Identify if channel has twitter, facebook, instagram google+
	C_names(VC_dict, V_des, V_title):
		Named Entity Recognition: average occurrence of named entities in description and titles for each video of each channel
	Agg1(mat, V_agg, C_name, Ref_scores, cat_id_dummy, social, y, C):
		Aggregate all the features: 
			C_name is score of named entity recognition
			cat_id_dummy are ecoded dummy features of video categories
			Ref_scores are aggregated referrer scores
			Social media scores
	PROCESSER():
		Aggregate all the processors

		
NE: named entity recognition
