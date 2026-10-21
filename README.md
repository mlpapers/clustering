---
title: "Clustering"
aliases: ["Cluster analysis", "Unsupervised classification"]
tags:
  - unsupervised
  - clustering
---
# Clustering

## Overviews

- **[Data Clustering: 50 Years Beyond K-Means](https://doi.org/10.1016/j.patrec.2009.09.011)** — Jain (2010). Survey of clustering objectives, algorithms, representation choices, and validation; similarity and the intended grouping determine which methods are appropriate.
- **[An Impossibility Theorem for Clustering](https://www.cs.cornell.edu/home/kleinber/nips15.pdf)** — Kleinberg (2002). No clustering function satisfies scale invariance, richness, and consistency together under the paper's definitions. The result concerns these axioms, not every clustering formulation.

## Partitions and Prototypes

- **[K-means](https://doi.org/10.1109/TIT.1982.1056489)** — Lloyd (1982). Alternates nearest-centroid assignment and centroid updates to reduce squared Euclidean distortion. Requires a cluster count; initialization affects the local solution. [Implementation](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html).
- **[K-means++](https://research.google/pubs/k-means-the-advantages-of-careful-seeding/)** — Arthur & Vassilvitskii (2007). Seeds centers using squared distance from existing centers; provides an expected approximation bound for the k-means objective, without guaranteeing the global optimum.
- **[Mini-batch k-means](https://www.ccs.neu.edu/home/vip/teach/DMcourse/2_cluster_EM_mixt/notes_slides/sculey_webscale_kmeans_approx.pdf)** — Sculley (2010). Updates centroids from small random batches instead of full passes. Trades optimization accuracy for cheaper updates; supports incremental fitting in [scikit-learn](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.MiniBatchKMeans.html).
- **[K-medoids / FastPAM](https://arxiv.org/abs/1810.05691)** — Schubert & Rousseeuw (2019). Uses observed objects as representatives and minimizes dissimilarity to them. FastPAM accelerates PAM's swap search; unlike k-means, medoids support non-Euclidean dissimilarities.
- **[Spherical k-means](https://doi.org/10.1023/A:1007612920971)** — Dhillon & Modha (2001). Clusters normalized document vectors using unit-length centroids and cosine similarity. Groups vector directions rather than magnitudes.
- **[Fuzzy c-means](https://doi.org/10.1016/0098-3004(84)90020-7)** — Bezdek, Ehrlich & Full (1984). Optimizes weighted distances to centroids with graded memberships controlled by a fuzzifier. These memberships are not posterior probabilities from a fitted mixture model.
- **[Affinity propagation](https://doi.org/10.1126/science.1136800)** — 2007. Exchanges messages between observations to select exemplars from pairwise similarities. Exemplar preferences influence the number of clusters, replacing a fixed cluster-count input.
- **[Bregman clustering](https://jmlr.org/papers/v6/banerjee05b.html)** — 2005. Generalizes hard and soft centroid clustering to Bregman divergences and connects these objectives to exponential-family mixtures; squared Euclidean k-means is one special case.

## Mixture Models

- **[Gaussian mixtures and EM](https://web.mit.edu/6.435/www/Dempster77.pdf)** — Dempster, Laird & Rubin (1977). EM alternates posterior component responsibilities and parameter updates. Gaussian covariance choices control component shapes; fitting can reach local optima. [Implementation](https://scikit-learn.org/stable/modules/mixture.html).
- **[Dirichlet process mixtures](https://www.cs.columbia.edu/~blei/papers/BleiJordan2006.pdf)** — Blei & Jordan (2006). Variational inference for mixtures with an unbounded component model. Practical truncated approximations retain a component cap; priors influence active components. [Implementation](https://scikit-learn.org/stable/modules/generated/sklearn.mixture.BayesianGaussianMixture.html).

## Hierarchical Clustering

- **[Agglomerative linkage](https://docs.scipy.org/doc/scipy/reference/generated/scipy.cluster.hierarchy.linkage.html)** — Single, complete, and average linkage merge clusters using minimum, maximum, or average cross-cluster distances. The linkage defines the dendrogram; cutting it selects a partition.
- **[Ward's method](https://doi.org/10.1080/01621459.1963.10500845)** — Ward (1963). Merges the pair giving the smallest increase in within-cluster sum of squares. Its variance interpretation requires Euclidean geometry. [Implementation notes](https://docs.scipy.org/doc/scipy/reference/generated/scipy.cluster.hierarchy.linkage.html).
- **[BIRCH](https://doi.org/10.1145/233269.233324)** — Zhang, Ramakrishnan & Livny (1996). Compresses observations into a tree of clustering-feature summaries, then clusters the summaries. Threshold and memory choices control compression. [Extended paper](https://research.ibm.com/publications/birch-a-new-data-clustering-algorithm-and-its-applications) (1997).

## Density and Modes

- **[DBSCAN](https://cdn.aaai.org/KDD/1996/KDD96-037.pdf)** — Ester et al. (1996). Groups density-connected regions using a neighborhood radius and minimum neighbor count; leaves other points as noise. A single radius can struggle with unequal cluster densities.
- **[OPTICS](https://doi.org/10.1145/304182.304187)** — Ankerst et al. (1999). Produces an ordering and reachability distances exposing density structure across neighborhood scales. Extracting a partition is a separate step. [Implementation](https://scikit-learn.org/stable/modules/clustering.html#optics).
- **[HDBSCAN](https://doi.org/10.1007/978-3-642-37456-2_14)** — Campello, Moulavi & Sander (2013). Builds a density hierarchy and selects persistent clusters, allowing different densities and noise. Minimum cluster size and density settings still affect the result. [Algorithm](https://hdbscan.readthedocs.io/en/latest/how_hdbscan_works.html).
- **[Mean shift](https://doi.org/10.1109/34.1000236)** — Comaniciu & Meer (2002). Moves candidate centers toward modes of a kernel density estimate. Bandwidth sets the scale of grouping; the number of clusters is not specified directly. [Implementation](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.MeanShift.html).

## Spectral, Subspace, and Graph Methods

- **[Spectral clustering](https://proceedings.neurips.cc/paper_files/paper/2001/hash/801272ee79cfde7fa5960571fee36b9b-Abstract.html)** — Ng, Jordan & Weiss (2001). Clusters an eigenvector representation of an affinity graph. Graph construction determines the geometry; different normalizations lead to different objectives. [Survey](https://arxiv.org/abs/0711.0189) — von Luxburg (2007).
- **[Sparse subspace clustering](https://arxiv.org/abs/1203.1005)** — Elhamifar & Vidal (2013). Represents each point sparsely using other points, builds an affinity from the coefficients, and applies spectral clustering. Targets unions of low-dimensional subspaces.
- **[Louvain](https://arxiv.org/abs/0803.0476)** — Blondel et al. (2008). Alternates local node moves and graph aggregation to optimize modularity. A graph-community heuristic; the result depends on the supplied edges and weights.
- **[Leiden](https://www.nature.com/articles/s41598-019-41695-z)** — Traag, Waltman & van Eck (2019). Adds partition refinement to avoid the disconnected communities Louvain can produce. Supports modularity and other objectives; connectivity guarantees do not imply a global optimum.
- **[Infomap](https://arxiv.org/abs/0707.0609)** — 2007. Finds communities by compressing descriptions of random walks on a network. Flow between modules determines the partition, supporting weighted and directed graphs.

## Categorical Data, Time Series, and Constraints

- **[K-modes / k-prototypes](https://cse.hkust.edu.hk/~qyang/Teaching/537/Papers/huang98extensions.pdf)** — Huang (1998). K-modes uses categorical mismatch counts and modes. K-prototypes combines categorical mismatch with numeric squared distances; their relative weight affects the partition.
- **[k-Shape](https://www.paparrizos.org/papers/PaparrizosSIGMOD15.pdf)** — Paparrizos & Gravano (2015). Uses normalized cross-correlation and shape-based centroids for time-series clustering, aligning sequences through shifts rather than local time warping.
- **[COP-KMeans](https://www.wkiri.com/research/papers/wagstaff-kmeans-01.pdf)** — Wagstaff et al. (2001). Incorporates must-link and cannot-link pairs into k-means assignments. Uses supervision through constraints; assignment can fail when no feasible cluster is available.
- **[Correlation clustering](https://doi.org/10.1023/B:MACH.0000033116.57574.95)** — 2004. Partitions a signed similarity graph to minimize pairwise disagreements or maximize agreements. The number of clusters is an outcome rather than a required input; unlike hard constraints, conflicting pair labels can incur a cost.
- **[Cluster ensembles](https://jmlr.org/papers/v3/strehl02a.html)** — Strehl & Ghosh (2002). Combines multiple partitions into a consensus without requiring the original features. Agreement across input partitions is the objective, not independent evidence of correctness.

## Learned Representations and Semantic Clustering

- **[Deep Embedded Clustering (DEC)](https://proceedings.mlr.press/v48/xieb16.html)** — Xie, Girshick & Farhadi (2016). Initializes an encoder with an autoencoder, then jointly refines its features and cluster centers using a sharpened target distribution and a KL-divergence objective.
- **[DeepCluster](https://arxiv.org/abs/1807.05520)** — Caron et al. (2018). Alternates k-means on image features with network training to predict those assignments. Clustering supplies pseudo-labels for representation learning. [Code](https://github.com/facebookresearch/deepcluster).
- **[SCAN](https://www.ecva.net/papers/eccv_2020/papers_ECCV/html/1057_ECCV_2020_paper.php)** — Van Gansbeke et al. (2020). Separates self-supervised feature learning from semantic image clustering; encourages neighboring representations to share assignments, followed by self-labeling.
- **[Pretrained embeddings](https://arxiv.org/abs/2605.29933)** — CLUBench (2026, preprint) finds conventional clustering on pretrained image/text features competitive in its experiments. Treat encoder, layer, pooling, normalization, and clustering settings as parts of the comparison.
- **[Clustering after UMAP](https://umap-learn.readthedocs.io/en/latest/clustering.html)** — UMAP can support clustering preprocessing, but can distort density and create apparent separations. A two-dimensional display alone is insufficient evidence for distinct groups.

## Choosing and Evaluating a Partition

- **[Gap statistic](https://doi.org/10.1111/1467-9868.00293)** — Tibshirani, Walther & Hastie (2001). Compares within-cluster dispersion with its expectation under a reference null distribution across cluster counts. The reference distribution is part of the method.
- **[Mixture model selection](https://scikit-learn.org/stable/modules/mixture.html)** — BIC compares Gaussian component counts and covariance structures with a complexity penalty. [Mixture components need not correspond one-to-one to clusters](https://pmc.ncbi.nlm.nih.gov/articles/PMC2953822/) (Baudry et al., 2010).
- **[Silhouette](https://doi.org/10.1016/0377-0427(87)90125-7)** — Rousseeuw (1987). Compares a point's mean within-cluster distance with its nearest alternative cluster. Favors compact, separated groups; scores depend on distance and representation. [Metric](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.silhouette_score.html).
- **[Adjusted Rand index](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.adjusted_rand_score.html)** — Measures pairwise agreement between partitions, adjusted for chance and invariant to cluster-label permutations. With reference classes, measures agreement with those classes rather than all possible useful groupings.
- **[Adjusted mutual information](https://jmlr.org/papers/v11/vinh10a.html)** — Vinh, Epps & Bailey (2010). Corrects mutual information between partitions for chance agreement. Unadjusted mutual information can reward extra clusters, especially with small samples.
- **[Resampling stability](https://arxiv.org/abs/1007.1075)** — von Luxburg (2010). Examines whether partitions persist under data perturbations. Stability depends on the algorithm and sampling scheme; high stability alone does not establish the correct cluster count.
- **Noise and coverage** — Report the fraction assigned to clusters and how noise labels enter each metric. [CLUBench](https://arxiv.org/abs/2605.29933) treats DBSCAN noise as one extra cluster; excluding those points evaluates a different population.
- **New observations** — [K-means](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html) assigns points to fitted centroids. [HDBSCAN's approximate prediction](https://hdbscan.readthedocs.io/en/latest/prediction_tutorial.html) holds the existing clustering fixed; it does not discover new clusters by refitting.
- **[CLUBench](https://arxiv.org/abs/2605.29933)** — Xiao et al. (2026, preprint). Compares 24 algorithms on 131 tabular, text, and image datasets. Supplies the true cluster count to methods requiring it; rankings under this protocol do not establish unknown-count discovery performance.

## Software

- **[scikit-learn](https://scikit-learn.org/stable/modules/clustering.html)** — Prototype, hierarchical, density, and spectral methods; [Gaussian mixtures](https://scikit-learn.org/stable/modules/mixture.html) and clustering metrics. [SciPy](https://docs.scipy.org/doc/scipy/reference/cluster.hierarchy.html) provides linkage, dendrograms, and tree cuts.
- **[hdbscan](https://github.com/scikit-learn-contrib/hdbscan)** — Density hierarchies, soft membership, and approximate prediction. [scikit-learn HDBSCAN](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.HDBSCAN.html) counts the point itself in `min_samples`; the contrib package excludes it. Equal settings are not equivalent.
- **[kmedoids](https://github.com/kno10/python-kmedoids)** — PAM and accelerated medoid algorithms. [kmodes](https://github.com/nicodv/kmodes) implements k-modes and k-prototypes for categorical and mixed data.
- **[tslearn](https://tslearn.readthedocs.io/en/stable/user_guide/clustering.html)** — Time-series clustering with Euclidean, dynamic-time-warping, and soft-DTW objectives; also provides [k-Shape](https://tslearn.readthedocs.io/en/stable/gen_modules/clustering/tslearn.clustering.KShape.html).
- **[Faiss](https://github.com/facebookresearch/faiss/wiki/K%E2%80%90means-clustering)** — K-means and spherical clustering using its nearest-neighbor index machinery, with GPU options. [ELKI](https://elki-project.github.io/) provides clustering algorithms and distance functions in Java.
- **[mclust](https://cran.r-project.org/package=mclust)** — Gaussian mixture clustering and model selection in R. [dbscan](https://cran.r-project.org/package=dbscan) provides DBSCAN, HDBSCAN, OPTICS, and related density methods.
- **[leidenalg](https://github.com/vtraag/leidenalg)** — Leiden community detection for igraph graphs, with multiple quality functions and multiplex support.

## Related Topics

- [Feature Extraction](https://mlpapers.org/feature-extraction/)
- [Models](https://mlpapers.org/models/)
