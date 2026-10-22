---
title: "Clustering"
aliases: ["Cluster analysis", "Unsupervised classification"]
tags:
  - unsupervised
  - clustering
---
# Clustering

🔒 Full text at this link requires payment or institutional access. Unmarked links may be unchecked.

## Overviews

- **Data Clustering: 50 Years Beyond K-Means** - Survey of clustering objectives, algorithms, representation choices, and validation; similarity and the intended grouping determine which methods are appropriate. [Jain 2010](<https://www.cse.msu.edu/~cse802/Papers/DataClustering50yearsBeyondKmeans.pdf> "Data clustering: 50 years beyond K-means; Pattern Recognit. Lett.").
- **An Impossibility Theorem for Clustering** - No clustering function satisfies scale invariance, richness, and consistency together under the paper's definitions. The result concerns these axioms, not every clustering formulation. [Kleinberg 2002](<https://www.cs.cornell.edu/home/kleinber/nips15.pdf> "An Impossibility Theorem for Clustering; NeurIPS").

## Partitions and Prototypes

- **K-means** - Alternates nearest-centroid assignment and centroid updates to reduce squared Euclidean distortion. Requires a cluster count; initialization affects the local solution. [Lloyd 1982](<https://doi.org/10.1109/TIT.1982.1056489> "Least squares quantization in PCM; IEEE Trans. Inform. Theory"); [docs](<https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html>).
- **K-means++** - Seeds centers using squared distance from existing centers; provides an expected approximation bound for the k-means objective, without guaranteeing the global optimum. [Arthur and Vassilvitskii 2007](<https://research.google/pubs/k-means-the-advantages-of-careful-seeding/> "k-means++: the advantages of careful seeding; SODA").
- **Mini-batch k-means** - Updates centroids from small random batches instead of full passes. Trades optimization accuracy for cheaper updates; supports incremental fitting in scikit-learn. [Sculley 2010](<https://www.ccs.neu.edu/home/vip/teach/DMcourse/2_cluster_EM_mixt/notes_slides/sculey_webscale_kmeans_approx.pdf> "Web-Scale K-Means Clustering; WWW"); [docs](<https://scikit-learn.org/stable/modules/generated/sklearn.cluster.MiniBatchKMeans.html>).
- **K-medoids / FastPAM** - Uses observed objects as representatives and minimizes dissimilarity to them. FastPAM accelerates PAM's swap search; unlike k-means, medoids support non-Euclidean dissimilarities. [Schubert and Rousseeuw 2019](<https://arxiv.org/abs/1810.05691> "Faster k-Medoids Clustering: Improving the PAM, CLARA, and CLARANS Algorithms; LNCS").
- **Spherical k-means** - Clusters normalized document vectors using unit-length centroids and cosine similarity. Groups vector directions rather than magnitudes. [Dhillon and Modha 2001](<https://doi.org/10.1023/A:1007612920971> "Concept Decompositions for Large Sparse Text Data Using Clustering; Mach. Learn.").
- **Fuzzy c-means** - Optimizes weighted distances to centroids with graded memberships controlled by a fuzzifier. These memberships are not posterior probabilities from a fitted mixture model. [Bezdek et al. 1984](<https://doi.org/10.1016/0098-3004(84)90020-7> "FCM: The fuzzy c-means clustering algorithm; Comput. Geosci.").
- **Affinity propagation** - Exchanges messages between observations to select exemplars from pairwise similarities. Exemplar preferences influence the number of clusters, replacing a fixed cluster-count input. [Frey and Dueck 2007](<https://doi.org/10.1126/science.1136800> "Clustering by Passing Messages Between Data Points; Science").
- **Bregman clustering** - Generalizes hard and soft centroid clustering to Bregman divergences and connects these objectives to exponential-family mixtures; squared Euclidean k-means is one special case. [Banerjee et al. 2005](<https://jmlr.org/papers/v6/banerjee05b.html> "Clustering with Bregman Divergences; JMLR").

## Mixture Models

- **Gaussian mixtures and EM** - EM alternates posterior component responsibilities and parameter updates. Gaussian covariance choices control component shapes; fitting can reach local optima. [Dempster et al. 1977](<https://web.mit.edu/6.435/www/Dempster77.pdf> "Maximum Likelihood from Incomplete Data Via the EM Algorithm; JRSS B"); [docs](<https://scikit-learn.org/stable/modules/mixture.html>).
- **Dirichlet process mixtures** - Variational inference for mixtures with an unbounded component model. Practical truncated approximations retain a component cap; priors influence active components. [Blei and Jordan 2006](<https://www.cs.columbia.edu/~blei/papers/BleiJordan2006.pdf> "Variational inference for Dirichlet process mixtures; Bayesian Anal."); [docs](<https://scikit-learn.org/stable/modules/generated/sklearn.mixture.BayesianGaussianMixture.html>).

## Hierarchical Clustering

- **Agglomerative linkage** - Single, complete, and average linkage merge clusters using minimum, maximum, or average cross-cluster distances. The linkage defines the dendrogram; cutting it selects a partition. [docs](<https://docs.scipy.org/doc/scipy/reference/generated/scipy.cluster.hierarchy.linkage.html>).
- **Ward's method** - Merges the pair giving the smallest increase in within-cluster sum of squares. Its variance interpretation requires Euclidean geometry. [Ward 1963](<https://doi.org/10.1080/01621459.1963.10500845> "Hierarchical Grouping to Optimize an Objective Function; JASA"); [docs](<https://docs.scipy.org/doc/scipy/reference/generated/scipy.cluster.hierarchy.linkage.html>).
- **BIRCH** - Compresses observations into a tree of clustering-feature summaries, then clusters the summaries. Threshold and memory choices control compression. [Zhang et al. 1996](<https://doi.org/10.1145/233269.233324> "BIRCH: an efficient data clustering method for very large databases; SIGMOD"), [Zhang et al. 1997](<https://research.ibm.com/publications/birch-a-new-data-clustering-algorithm-and-its-applications> "BIRCH: A new data clustering algorithm and its applications; Data Mining and Knowledge Discovery").

## Density and Modes

- **DBSCAN** - Groups density-connected regions using a neighborhood radius and minimum neighbor count; leaves other points as noise. A single radius can struggle with unequal cluster densities. [Ester et al. 1996](<https://cdn.aaai.org/KDD/1996/KDD96-037.pdf> "A Density-Based Algorithm for Discovering Clusters in Large Spatial Databases with Noise; KDD").
- **OPTICS** - Produces an ordering and reachability distances exposing density structure across neighborhood scales. Extracting a partition is a separate step. [Ankerst et al. 1999](<https://doi.org/10.1145/304182.304187> "OPTICS: ordering points to identify the clustering structure; SIGMOD"); [docs](<https://scikit-learn.org/stable/modules/clustering.html#optics>).
- **HDBSCAN** - Builds a density hierarchy and selects persistent clusters, allowing different densities and noise. Minimum cluster size and density settings still affect the result. [Campello et al. 2013 🔒](<https://doi.org/10.1007/978-3-642-37456-2_14> "Density-Based Clustering Based on Hierarchical Density Estimates; LNCS"); [docs](<https://hdbscan.readthedocs.io/en/latest/how_hdbscan_works.html>).
- **Mean shift** - Moves candidate centers toward modes of a kernel density estimate. Bandwidth sets the scale of grouping; the number of clusters is not specified directly. [Comaniciu and Meer 2002](<https://doi.org/10.1109/34.1000236> "Mean shift: a robust approach toward feature space analysis; TPAMI"); [docs](<https://scikit-learn.org/stable/modules/generated/sklearn.cluster.MeanShift.html>).

## Spectral, Subspace, and Graph Methods

- **Spectral clustering** - Clusters an eigenvector representation of an affinity graph. Graph construction determines the geometry; different normalizations lead to different objectives. [Ng et al. 2001](<https://proceedings.neurips.cc/paper_files/paper/2001/hash/801272ee79cfde7fa5960571fee36b9b-Abstract.html> "On Spectral Clustering: Analysis and an algorithm; NeurIPS"), [von Luxburg 2007](<https://arxiv.org/abs/0711.0189> "A Tutorial on Spectral Clustering; arXiv").
- **Sparse subspace clustering** - Represents each point sparsely using other points, builds an affinity from the coefficients, and applies spectral clustering. Targets unions of low-dimensional subspaces. [Elhamifar and Vidal 2012](<https://arxiv.org/abs/1203.1005> "Sparse Subspace Clustering: Algorithm, Theory, and Applications; arXiv").
- **Louvain** - Alternates local node moves and graph aggregation to optimize modularity. A graph-community heuristic; the result depends on the supplied edges and weights. [Blondel et al. 2008](<https://arxiv.org/abs/0803.0476> "Fast unfolding of communities in large networks; J. Stat. Mech.").
- **Leiden** - Adds partition refinement to avoid the disconnected communities Louvain can produce. Supports modularity and other objectives; connectivity guarantees do not imply a global optimum. [Traag et al. 2019](<https://www.nature.com/articles/s41598-019-41695-z> "From Louvain to Leiden: guaranteeing well-connected communities; Scientific Reports").
- **Infomap** - Finds communities by compressing descriptions of random walks on a network. Flow between modules determines the partition, supporting weighted and directed graphs. [Rosvall and Bergstrom 2008](<https://arxiv.org/abs/0707.0609> "Maps of random walks on complex networks reveal community structure; PNAS").

## Categorical Data, Time Series, and Constraints

- **K-modes / k-prototypes** - K-modes uses categorical mismatch counts and modes. K-prototypes combines categorical mismatch with numeric squared distances; their relative weight affects the partition. [Huang 1998](<https://cse.hkust.edu.hk/~qyang/Teaching/537/Papers/huang98extensions.pdf> "Extensions to the k-Means Algorithm for Clustering Large Data Sets with Categorical Values; Data Min. Knowl. Discov.").
- **k-Shape** - Uses normalized cross-correlation and shape-based centroids for time-series clustering, aligning sequences through shifts rather than local time warping. [Paparrizos and Gravano 2015](<https://www.paparrizos.org/papers/PaparrizosSIGMOD15.pdf> "k-Shape; SIGMOD").
- **COP-KMeans** - Incorporates must-link and cannot-link pairs into k-means assignments. Uses supervision through constraints; assignment can fail when no feasible cluster is available. [Wagstaff et al. 2001](<https://www.wkiri.com/research/papers/wagstaff-kmeans-01.pdf> "Constrained K-means Clustering with Background Knowledge; ICML").
- **Correlation clustering** - Partitions a signed similarity graph to minimize pairwise disagreements or maximize agreements. The number of clusters is an outcome rather than a required input; unlike hard constraints, conflicting pair labels can incur a cost. [Bansal et al. 2004](<https://doi.org/10.1023/B:MACH.0000033116.57574.95> "Correlation Clustering; Mach. Learn.").
- **Cluster ensembles** - Combines multiple partitions into a consensus without requiring the original features. Agreement across input partitions is the objective, not independent evidence of correctness. [Strehl and Ghosh 2002](<https://jmlr.org/papers/v3/strehl02a.html> "Cluster Ensembles --- A Knowledge Reuse Framework for Combining Multiple Partitions; JMLR").

## Learned Representations and Semantic Clustering

- **Deep Embedded Clustering (DEC)** - Initializes an encoder with an autoencoder, then jointly refines its features and cluster centers using a sharpened target distribution and a KL-divergence objective. [Xie et al. 2016](<https://proceedings.mlr.press/v48/xieb16.html> "Unsupervised Deep Embedding for Clustering Analysis; ICML").
- **DeepCluster** - Alternates k-means on image features with network training to predict those assignments. Clustering supplies pseudo-labels for representation learning. [Caron et al. 2018](<https://arxiv.org/abs/1807.05520> "Deep Clustering for Unsupervised Learning of Visual Features; ECCV"); [code](<https://github.com/facebookresearch/deepcluster>).
- **SCAN** - Separates self-supervised feature learning from semantic image clustering; encourages neighboring representations to share assignments, followed by self-labeling. [Van Gansbeke et al. 2020](<https://www.ecva.net/papers/eccv_2020/papers_ECCV/html/1057_ECCV_2020_paper.php> "SCAN: Learning to Classify Images without Labels; ECCV").
- **Pretrained embeddings** - CLUBench (2026, preprint) finds conventional clustering on pretrained image/text features competitive in its experiments. Treat encoder, layer, pooling, normalization, and clustering settings as parts of the comparison. [Xiao et al. 2026](<https://arxiv.org/abs/2605.29933> "CLUBench: A Clustering Benchmark; arXiv").
- **Clustering after UMAP** - UMAP can support clustering preprocessing, but can distort density and create apparent separations. A two-dimensional display alone is insufficient evidence for distinct groups. [docs](<https://umap-learn.readthedocs.io/en/latest/clustering.html>).

## Choosing and Evaluating a Partition

- **Gap statistic** - Compares within-cluster dispersion with its expectation under a reference null distribution across cluster counts. The reference distribution is part of the method. [Tibshirani et al. 2001](<https://doi.org/10.1111/1467-9868.00293> "Estimating the Number of Clusters in a Data Set Via the Gap Statistic; JRSS B").
- **Mixture model selection** - BIC compares Gaussian component counts and covariance structures with a complexity penalty. [Baudry et al. 2010](<https://pmc.ncbi.nlm.nih.gov/articles/PMC2953822/> "Combining Mixture Components for Clustering; Journal of computational and graphical statistics : a joint publication of American Statistical Association, Institute of Mathematical Statistics, Interface Foundation of North America"); [docs](<https://scikit-learn.org/stable/modules/mixture.html>).
- **Silhouette** - Compares a point's mean within-cluster distance with its nearest alternative cluster. Favors compact, separated groups; scores depend on distance and representation. [Rousseeuw 1987](<https://doi.org/10.1016/0377-0427(87)90125-7> "Silhouettes: A graphical aid to the interpretation and validation of cluster analysis; JCAM"); [docs](<https://scikit-learn.org/stable/modules/generated/sklearn.metrics.silhouette_score.html>).
- **Adjusted Rand index** - Measures pairwise agreement between partitions, adjusted for chance and invariant to cluster-label permutations. With reference classes, measures agreement with those classes rather than all possible useful groupings. [Hubert and Arabie 1985 🔒](<https://doi.org/10.1007/BF01908075> "Comparing partitions; Journal of Classification"); [docs](<https://scikit-learn.org/stable/modules/generated/sklearn.metrics.adjusted_rand_score.html>).
- **Adjusted mutual information** - Corrects mutual information between partitions for chance agreement. Unadjusted mutual information can reward extra clusters, especially with small samples. [Vinh et al. 2010](<https://jmlr.org/papers/v11/vinh10a.html> "Information Theoretic Measures for Clusterings Comparison: Variants, Properties, Normalization and Correction for Chance; JMLR").
- **Resampling stability** - Examines whether partitions persist under data perturbations. Stability depends on the algorithm and sampling scheme; high stability alone does not establish the correct cluster count. [von Luxburg 2010](<https://arxiv.org/abs/1007.1075> "Clustering Stability: An Overview; Found. Trends ML").
- **Noise and coverage** - Report the fraction assigned to clusters and how noise labels enter each metric. CLUBench treats DBSCAN noise as one extra cluster; excluding those points evaluates a different population. [Xiao et al. 2026](<https://arxiv.org/abs/2605.29933> "CLUBench: A Clustering Benchmark; arXiv").
- **New observations** - K-means assigns points to fitted centroids. HDBSCAN's approximate prediction holds the existing clustering fixed; it does not discover new clusters by refitting. [docs](<https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html>), [docs](<https://hdbscan.readthedocs.io/en/latest/prediction_tutorial.html>).
- **CLUBench** - Compares 24 algorithms on 131 tabular, text, and image datasets. Supplies the true cluster count to methods requiring it; rankings under this protocol do not establish unknown-count discovery performance. [Xiao et al. 2026](<https://arxiv.org/abs/2605.29933> "CLUBench: A Clustering Benchmark; arXiv").

## Software

- **scikit-learn** - Prototype, hierarchical, density, and spectral methods; Gaussian mixtures and clustering metrics. SciPy provides linkage, dendrograms, and tree cuts. [docs](<https://scikit-learn.org/stable/modules/mixture.html>), [docs](<https://docs.scipy.org/doc/scipy/reference/cluster.hierarchy.html>), [docs](<https://scikit-learn.org/stable/modules/clustering.html>).
- **hdbscan** - Density hierarchies, soft membership, and approximate prediction. scikit-learn HDBSCAN counts the point itself in `min_samples`; the contrib package excludes it. Equal settings are not equivalent. [docs](<https://scikit-learn.org/stable/modules/generated/sklearn.cluster.HDBSCAN.html>), [code](<https://github.com/scikit-learn-contrib/hdbscan>).
- **kmedoids** - PAM and accelerated medoid algorithms. kmodes implements k-modes and k-prototypes for categorical and mixed data. [code](<https://github.com/nicodv/kmodes>), [code](<https://github.com/kno10/python-kmedoids>).
- **tslearn** - Time-series clustering with Euclidean, dynamic-time-warping, and soft-DTW objectives; also provides k-Shape. [docs](<https://tslearn.readthedocs.io/en/stable/gen_modules/clustering/tslearn.clustering.KShape.html>), [docs](<https://tslearn.readthedocs.io/en/stable/user_guide/clustering.html>).
- **Faiss** - K-means and spherical clustering using its nearest-neighbor index machinery, with GPU options. ELKI provides clustering algorithms and distance functions in Java. [docs](<https://elki-project.github.io/>), [code](<https://github.com/facebookresearch/faiss/wiki/K%E2%80%90means-clustering>).
- **mclust** - Gaussian mixture clustering and model selection in R. dbscan provides DBSCAN, HDBSCAN, OPTICS, and related density methods. [code](<https://cran.r-project.org/package=dbscan>), [code](<https://cran.r-project.org/package=mclust>).
- **leidenalg** - Leiden community detection for igraph graphs, with multiple quality functions and multiplex support. [code](<https://github.com/vtraag/leidenalg>).

## Related topics

- [Feature Extraction](https://mlpapers.org/feature-extraction/)
- [Models](https://mlpapers.org/models/)
