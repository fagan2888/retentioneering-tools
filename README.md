<div align="left">

[![Rete logo](https://github.com/retentioneering/pics/blob/master/pics/logo_long_black.png)](https://github.com/retentioneering/retentioneering-tools)

[![Pipi version](https://img.shields.io/pypi/v/retentioneering)](https://pypi.org/project/retentioneering/)
[![Telegram](https://img.shields.io/badge/channel-on%20telegram-blue)](https://t.me/retentioneering_meetups)
[![Python version](https://img.shields.io/pypi/pyversions/retentioneering)](https://pypi.org/project/retentioneering/)
[![License](https://img.shields.io/pypi/l/retentioneering)](https://www.mozilla.org/en-US/MPL/)
[![Travis Build Status](https://travis-ci.com/retentioneering/retentioneering-tools.svg?branch=unit_tests)](https://travis-ci.com/github/retentioneering/retentioneering-tools)
[![Downloads](https://pepy.tech/badge/retentioneering)](https://pepy.tech/project/retentioneering)


## What is Retentioneering?


Retentioneering is a Python framework to process and analyze clickstreams, event streams, trajectories, and event logs. You can segment users, clients (agents), build ML pipelines to predict agent category or probability of target event based on historical data.

Retentioneering extends Pandas, NetworkX, Scikit-learn for in-depth processing of event sequences data, specifically Retentioneering provides a powerful environment to perform an in-depth analysis of customer journey maps, bringing behavior-driven segmentation of users and machine learning pipelines to product analytics. Retentioneering is also developing customer journey map simulation engines that allow the data scientists to explore the business impact of CJM mutations and optimize product and online marketing.

Product analysts can apply Retentioneering Tools as a Python framework to explore, grow, and optimize the product based on deep analysis of user trajectories. Using Retentioneering you can vectorize clickstream logs and cluster user trajectories to automatically identify common successful or churn patterns. You can explore those patterns using our tools such as graph visualizer, step matrix, multiple clustering, and segmentation engines, and many others.

This repository contains both python library with easy to use utils, but also we provide several demos Python Notebooks and datasets to illustrate how to automate product analytics routines.

## Installation

- You can install our package using pip:

```bash
pip3 install retentioneering
```


## Getting started

If you use Pandas dataframes to work with user behaviour data you can try Retentioneering with just a few lines of code!

```python
import retentioneering

# load sample data
from retentioneering import datasets
data = datasets.load_simple_shop()

retentioneering.config.update({
    'event_col':'event',
    'event_time_col':'timestamp',
    'index_col': 'client_id'
})
```

Above we imported sample dataset, which is regular pandas dataframe containing raw user
behavior data from hypothetical web-site or app in form of sequence {'client_id', 'event', 'timestamp'},
and pass those column names to retentioneering.config. Now, let's plot the graph to visualize 
user behaviour from the dataset (read more about graphs here):

<div align="left">

 ```python
data.rete.plot_graph(norm_type='node',
                      weight_col='client_id',
                      thresh=0.2,
                      targets = {'payment_done':'green',
                                 'lost':'red'})
```

[![intro 1](https://github.com/retentioneering/pics/blob/master/pics/rete20/graph_0.png)](https://github.com/retentioneering/retentioneering-tools)

Here we obtain the high-level graph of user activity where 
edge A --> B weight shows percent of users transitioning to event B from 
all users reached event A (note, edges with small weighs are 
thresholded to avoid visual clutter, read more in the documentation)

To automatically find distinct behavioral patterns we can cluster users from the
dataset based on their behavior:

<div align="left">

```pyhton
data.rete.get_clusters(method='kmeans',
                       n_clusters=8,
                       ngram_range=(1,2),
                       plot_type='cluster_bar',
                       targets=['payment_done','cart']);
```

[![intro 1](https://github.com/retentioneering/pics/blob/master/pics/rete20/clustering_2.svg)](https://github.com/retentioneering/retentioneering-tools)

<div align="left">

Users with similar behavior grouped in the same clluster. Clusters with low convertion rate
can represent systematic problem in the product: specific behavior pattern which systematically 
does not lead to product goals. Obtained user segments can be explored deeper to understand 
problematic behavior pattern. In the example above cluster 4 has low convertion rate to purchase 
but high convertion rate to cart visit.

```python
clus_4 = data.rete.filter_cluster(4)
clus_4.rete.plot_graph(thresh=0.1,
                        weight_col='client_id',
                        targets = {'lost':'red',
                                   'payment_done':'green'})
```
<div align="left">

[![intro 1](https://github.com/retentioneering/pics/blob/master/pics/rete20/graph_1.png)](https://github.com/retentioneering/retentioneering-tools)


To explore more features please see the [documentation](https://retentioneering.github.io/retentioneering-tools/)

## Documentation

#### Explore [these step-by-step tutorials](https://github.com/retentioneering/retentioneering-tools/tree/master/examples) to learn more:

- [Plot graph](https://retentioneering.github.io/retentioneering-tools/_build/html/early_steps.html#first-steps) 
- [Step Matrix](https://retentioneering.github.io/retentioneering-tools/_build/html/early_steps.html#temporal-funnel)
- [Users behavioral clustering](https://retentioneering.github.io/retentioneering-tools/_build/html/early_steps.html#supervised-classifier) 
- [Compare user segments](https://retentioneering.github.io/retentioneering-tools/_build/html/mobile-app-case.html#analysis)


## Contributing

This is community-driven open source project in active development. Any contributions, new ideas, bug reports, bug fixes, documentation improvements are very welcome.

Feel free to reach out to us: retentioneering[at]gmail.com

Retentioneering now provides several opensource solutions for data-driven product analytics and web analytics. Please checkout this repository for JS library to track the mutations of the website elements: https://github.com/retentioneering/retentioneering-dom-observer

Apps better with math!:)
Retentioneering is a research laboratory, analytics methodology and opensource tools founded by [Maxim Godzi](https://www.linkedin.com/in/godsie/) and [Anatoly Zaytsev](https://www.linkedin.com/in/anatoly-zaytsev/) in 2015. Please feel free to contact us at retentioneeringATgmail.com if you have any questions regarding this rep, or to obtain more tools that we are not able to provide though the public rep.
