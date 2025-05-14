Mastodon Moderation Analysis
Overview
This project analyzes Mastodon moderation data to explore patterns in moderator activities, focusing on blocking behaviors across instances. It consists of four tasks:

Creating a Similarity Network: Builds a colored, undirected weighted graph to visualize relationships between moderators based on their blocking activities.
Community Detection: Identifies and visualizes communities of moderators with similar moderation patterns using the Louvain algorithm.
Reflection: Discusses challenges and solutions encountered during the analysis.
Repeat Offenses Analysis: Examines users repeatedly blocked by moderators, analyzing blocking reasons and moderator community involvement.

The analysis uses a dataset (mastodon_edgelist_AE2.csv) containing moderation actions, including source (moderator), target (blocked user), blocking reason, and weight.
Project Structure

Data Source:
mastodon_edgelist_AE2.csv: Contains moderation data with columns for source, target, blocking reason, and weight.


Main Script: Analyzing Mastdon Data.ipynb (Jupyter Notebook)
Processes the data, cleans text, computes similarity metrics, detects communities, and analyzes repeat offenders.


Dependencies:
Python 3.x
Libraries: pandas, numpy, matplotlib, nltk, scipy, scikit-learn, networkx


Outputs:
Visualizations:
Moderator similarity network colored by blocking reason (e.g., harassment, spam).
Louvain community detection graph with communities colored by size.
Bar graph of community sizes.
Bar graph of blocking reasons for repeat offenders.


Console outputs:
Cosine similarity matrix snippet.
Community summaries (size, instances, blocking reasons).
Repeat offender details (e.g., number of blocks, moderators involved).





Key Features

Similarity Network (Task 1):

Cleans and tokenizes blocking reasons, removing URLs, special characters, and stopwords.
Creates a sparse matrix from a pivot table of source-target interactions.
Computes cosine similarity between moderators to build an undirected weighted graph.
Colors nodes by blocking reason (e.g., red for harassment, blue for spam) and filters edges to the top 90% by weight.


Community Detection (Task 2):

Applies the Louvain algorithm to identify moderator communities based on similarity.
Filters out communities with fewer than 3 nodes and reassigns community IDs.
Visualizes communities with distinct colors and summarizes community sizes and blocking reasons.
Generates a bar graph of community sizes.


Reflection (Task 3):

Documents challenges, such as handling disconnected graphs, converting node IDs to strings, and setting community size thresholds.
Describes solutions, including edge weight thresholding and dictionary-based community lookups.


Repeat Offenses Analysis (Task 4):

Identifies users blocked multiple times and analyzes their blocking reasons.
Attempts to map moderators to communities to count blocks from different communities.
Visualizes the frequency of blocking reasons (e.g., misinformation, harassment) for repeat offenders.



Setup Instructions

Clone the Repository:
git clone https://github.com/your-username/mastodon-moderation-analysis.git
cd mastodon-moderation-analysis


Install Dependencies:
pip install pandas numpy matplotlib nltk scipy scikit-learn networkx

Ensure NLTK's punkt tokenizer is downloaded:
import nltk
nltk.download('punkt')


Prepare Data:

Place mastodon_edgelist_AE2.csv in the project directory.
Ensure the file includes columns: source, target, blocking_reason, weight.


Run the Analysis:

Open Analyzing Mastdon Data.ipynb in Jupyter Notebook or Google Colab.
Execute the cells sequentially to process the data and generate outputs.
Alternatively, convert the notebook to a Python script:jupyter nbconvert --to script "Analyzing Mastdon Data.ipynb"
python "Analyzing Mastdon Data.py"





Usage

Run the notebook to generate graphs and summaries.
Modify the stop_words list or color_mapping dictionary to customize text cleaning or visualization aesthetics.
Adjust the edge weight threshold (90th percentile) or community size threshold (3 nodes) to explore different graph structures.
Extend the reasons list in Task 1 to include additional blocking reasons.

Results

Task 1: The similarity network shows moderators blocking misinformation and harassment often focus on those categories, while spam blockers tackle a variety of posts.
Task 2: Community detection reveals large communities (e.g., 10 and 8 instances) dominated by harassment and misinformation, with spam rarely being the primary focus.
Task 4: Repeat offenders are most often blocked for misinformation (210 users) compared to harassment (175 users), suggesting stricter moderation for harassment. However, community assignment issues limited the analysis of blocks across communities.

Limitations

The dataset is specific to one Mastodon instance and may not generalize to other platforms.
Inconsistent community assignments for moderators in Task 4 reduced the reliability of community-based block counts.
The analysis assumes clean and consistent blocking reason data, which may vary in practice.
Small community sizes and sparse graphs can affect the robustness of community detection.

Future Improvements

Incorporate data from multiple Mastodon instances for broader insights.
Improve community assignment logic to ensure all moderators are mapped correctly.
Add statistical analysis to compare blocking reason frequencies across communities.
Explore temporal trends in moderation actions to identify changes over time.
Implement advanced text processing (e.g., TF-IDF) for more nuanced similarity calculations.

