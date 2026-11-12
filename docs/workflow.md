## Welcome! :) Follow the instructions below to reproduce the paper's results.
# Getting started
To run the code in this repository you must first install the required packages. This can be found in `requirements.txt` file and can be installed using the command `pip install -r requirements.txt`

# Downloading the data
You will need to download the data from its original source as it is about 2GB and too big to include in this repo. Go to rrr link and follow the instructions there.

# Running the preprocessing pipeline
After having the dataset downloaded and accessible to your work environment, you are ready to preprocess the pipeline. As mentioned in the paper, the data is extremely inhomogeneous both geographically and temporally, so extensive data preprocessing is necessary to attempt to mitigate bias.

In the notebook called `Preprocessing.ipynb` you can find in each cell a step of the preprocessing pipeline. This includes separating the dataset into two ~20 year datasets, finding a threshold over data density bins and subsampling randomly points up to the threshold. More detail about the method can be found within the notebook and on the main article.

Alternatively, if you do not care about the process and wish only to reproduce the results you can use the function from `funcs.py` called `method34`. It was the 34th attempt at a preprocessing method hence the name. This function accepts as imput a pandas dataframe, for more information refer to the functions documentation.

# Selecting the number of clusters
Using the Bayesian Information Criterion (BIC) score (refer to main article), we can find the optimal number of clusters for this classification problem. morrre

# Running the GMM ensemble
Now that the preprocessing and the cluster number choice are out of the way, all that is left to do is running the 100 GMM ensemble for the optimal number of clusters. Note that we chose to do 100 GMMs but this is an arbitrary choice, mainly restricted by computational power. The ensemble is trained in batches, maximising the ability to parallely compute GMMs since they are independent. If GPUs are available the function that runs the ensemble should be able to detects this. Once calculated, the way we chose to save the clustering results was by duplicating the original data csv and adding a column per ensemble member of hard classification, 6 columns per ensemble member of cluster membership probabilities, 6 columns per ensemble member of cluster membership variance and a precomputed mean ensemble column for both hard and soft clustering. 

Note that there is no consensus between ensemble members on the cluster numbers. To deal with this we refer you to the method created in Poropat et al. 2024, where a similar issue was found and solved. This is implemented in our code.

# Plotting the results
To plot your recently found results, use the Plots.ipynb notebook. These are the exact plots used in the article plus a few plots that ended up not being used in the paper but still have some informative value. These include data dsitribution plots as well before and after preprocessing and the pipeline flow chart.