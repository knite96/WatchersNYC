# The Watchers of NYC

## Main

**Welcome to my Project Website!**

### Overview:

The objective of my project was to use data on animal encounters in NYC to create visualizations that may urge site visitors to seek out their local wildlife. Personally, I was curious about the nature of these animals in New York. These silent watchers that have observed and adapted to centuries of human activity. Using some of the most popular python libraries, I have created several visualizations that I hope will impart some glint of knowledge to anyone viewing this site.

### The Libraries I used:
```
#Python Libraries:
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from collections import Counter
import folium
```

With the proper libraries loaded, we can now read the dataset I chose:
```
#read dataset
df = pd.read_csv('Urban_Park_Ranger_Animal_Condition_Response.csv')
```

Now we move onto preprocessing the data:

### Preprocessing the Data:

This dataset I have chosen is a compilation of all requests made to and by Urban Park Rangers of NYC. They are called upon to handle encounters with animals should they be in direct or indirect danger to those around them. This is data compile from 2018-2021 and should be updated semi frequently. This is the only source of data I found related to human/animal interaction and location (as well as time) that is updated within NYC. There are many features in this dataset but I will only use a handfull. 
```
#return dataframe of necessary features
df = df[['Date and Time of initial call', 'Borough', 'Property', 'Species Description', 'Species Status', 'Animal Class', '# of Animals']]
#drop all nans
df.dropna()

#standardize all species descriptions for easier grouping
#small additional edits were made to standardize all non-formal entries/spelling errors
df['Species Description'] = df['Species Description'].str.title()
df['Species Status'] = df['Species Status'].replace(np.nan, 'Other')

#output to new file
df.to_csv('WatchersFin.csv', index=False)
```
With preprocessing done, we can now get to work with the data and create visualizations!

### Visualizations:

First, I'd like to see how this data is spread out amongst the boroughs; see if we get a well-spread-out map of activity:
```
#groupby function to see the animal data by percentage by borough
boro_graph = watcher.groupby(['Borough'])['# of Animals'].sum()
top_of_list = boro_graph.sort_values(ascending=False)
perc = top_of_list/sum(top_of_list) * 100
print(perc)
```
![Image](boro_p.PNG)

So, I'm guessing Central Park has something to do with this...
Let's see what a bar graph will show us...

```
#bar graph to visualize the split amongst the boroughs oF NYC
fig = plt.figure()
ax = fig.add_axes([0,0,1,1])
x_labels = ['Manhatten', 'Brooklyn', 'Queens', 'Staten Island', 'Bronx']
y_labels = [46.411483, 21.818182, 12.057416, 10.430622, 9.282297]
ax.bar(x_labels, y_labels)
plt.show()
```
![Image](bar1.png)

























