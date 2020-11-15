# SCDetector: Software Functional Clone Detection Based on Semantic Tokens Analysis

SCDetector is a combination of token-based and graph-based approach. Given a method source
code, we first generate the CFG and then apply centrality analysis to
transform the graph into certain semantic tokens (i.e., tokens with
graph details). Finally, these semantic tokens are fed into a Siamese
network to train a model and use it to detect code clone pairs.

SCDetector consists of three main phases:
Static Analysis, Centrality Analysis, and Clone Detection.

1. Static Analysis: This phase aims to extract the CFG of a
method based on static analysis, where each node is a basic
block. The input in this phase is a method while the output
is the CFG of the method.

2. Centrality Analysis: In this phase, we first dig out the
centrality of each basic block of the CFG obtained from
static analysis. Then we assign the centrality to each token
in a basic block and sum the centrality of the same token
in different basic blocks. The outputs are tokens with graph
details (i.e., centrality), called semantic tokens.

3. Clone Detection: Given a pair of code methods, the corresponding
semantic tokens are fed into a Siamese network.
The output is the probability that these two methods are a
clone pair. If the probability is large than 0.5, we identify that
they are a pair of clones. The Siamese network is trained
first by using labeled code pairs.

# Dataset #

We conduct our evaluations on two datasets: Google Code Jam
(<https://github.com/parasol-aser/deepsim/tree/master/dataset>) and BigCloneBench (<https://github.com/jeffsvajlenko/BigCloneEval>). 

Programs in Google Code Jam are
collected from an online programming competition held by Google.
In our experiment, we use the same dataset collected by DeepSim (<https://github.com/parasol-aser/deepsim>), which
consists of 1,669 projects from 12 different competition problems.
As discussed in DeepSim, projects for solving the same problem are
functionally similar while those for different problems are dissimilar.
Moreover, very few projects within a competition problem are
syntactically similar. Therefore, we can assume that code clone
pairs in the same problem are most likely to be semantic clones (i.e.,
Type-4 clones). The total number of similar and dissimilar method
pairs are 275,570 and 1,116,376, respectively.

The second dataset used in our experiment is BigCloneBench (<https://github.com/jeffsvajlenko/BigCloneEval>) dataset, which composes of over 6,000,000 tagged clone pairs
from 25,000 systems. The code granularity of clone pairs in
BigCloneBench is function-level, and each clone pair is
manually assigned a corresponding clone type. Because of the
ambiguous boundary between Type-3 and Type-4, these two clone
types are further divided into three subcategories by a similarity
score measured by line-level and token-level after Type-1 and
Type-2 normalizations, as follows: i) Strongly Type-3 (ST3) with
a similarity between [0.7, 1.0), ii) Moderately Type-3 (MT3) with a
similarity between [0.5, 0.7), and iii)Weakly Type-3/Type-4 (WT3/T4)
with a similarity between [0.0, 0.5).

# Publication #
Yueming Wu, Deqing Zou, Shihan Dou, Siru Yang, Wei Yang, Feng Cheng,
Hong Liang, and Hai Jin. 2020. SCDetector: Software Functional Clone
Detection Based on Semantic Tokens Analysis. In 35th IEEE/ACM International
Conference on Automated Software Engineering (ASE'20), September
21–25, 2020, Virtual Event, Australia. ACM, New York, NY, USA, 13 pages.
https://doi.org/10.1145/3324884.3416562
