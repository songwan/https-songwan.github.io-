---
title: Introducing TCLUST algorithm
layout: post
summary: Robust clustering algorithm by trimming approach
categories:
    - statistics
thumbnail: posts/tclust.png
author: Songwan
---
<script src='https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.4/MathJax.js?config=default'></script>


<hr>
### Note
<p align="justify" style='line-height:200%; font-size:120%'>
This post is a summary of TCLUST algorithm by Fritz et al., and García-Escudero et al. The detailed listings of references are listed at the end of this post. All of the contents or ideas in this post are from these references. It is done as a Robust Statistics course project. This is a link for <a href="http://drive.google.com/uc?export=view&id=1a5COCf9MJIeG1u9mzsSqtsXkOHki9aNB" target="_blank">full report including examples and simulation studies</a> and <a href="http://drive.google.com/uc?export=view&id=1a5COCf9MJIeG1u9mzsSqtsXkOHki9aNB" target="_blank"> R source code</a>.
</p>
<hr>
### 1. Introduction  
<p align="justify" style='line-height:200%; font-size:120%'>
 K-means is an unsupervised learning algorithm widely used in cluster analysis. However, K-means relies heavily on four major assumptions. 1) Number of clusters, k, 2) SSE is the right objective to minimize, 3) every cluster has the same shape, and 4) every observation is equally important for each cluster. We will discuss the sensible choice of k in section 4.4. Minimizing SSE may not be the right objective, as clusters often have different variances.

&nbsp;&nbsp;&nbsp;&nbsp;Assuming that SSE is minimized for any cluster leads to clusters having the same shape (e.g. scatter matrices are equal). This assumption does not hold when spurious observations or groups are introduced, which is the essence of the robustness of an estimator. We will illustrate the results of K-means with a simulation performed in this post. Similar to the classical means, trimming the data is one of the remedies we should always be looking to perform. Background noise and outlying groups could unnecessarily give too much information, leading to not being able to analyze what we are actually interested in.<br><br>

&nbsp;&nbsp;&nbsp;&nbsp;However, trimming approach on K-means also holds the same assumptions as classical K-means. Even after discarding the spurious observations, limitation of having equally spherical shapes and weights on clusters would still prevent us from obtaining the optimal clustering results. TCLUST allows us to flexibly modify these assumptions, as we are able to put various types of constraints on the scatter matrices and control how strong the constraint is.<br>
</p>
<hr>
### 2. TCLUST on eigenvalue ratio constraints  
<p align="justify" style='line-height:200%; font-size:120%'>
In this post, we will illustrate mathematical framework for robust clustering by eigenvalue ratio constraints. The concepts and descriptions used in section 2 and section 3 are mainly from the work done by Fritz et al. (2013). Suppose we were given the sample observations \({x_1,x_2, …, x_n}\) in \(R^p\), and the probability distribution function ϕ(·;μ,Σ) of p-variate normal distribution with mean μ and covariance matrix 𝜮. Assume the number of clusters to be k and the trimming level to be α. Trimming level decides how much proportion of the data we want to treat as an outlier. For example, we should trim [nα] observations for trimming level α.
<br><br>

&nbsp;&nbsp;&nbsp;&nbsp;Let \(R_0,R_1,…, R_k\) be a partition of the indices of n observations. For example, in the partition \(R_1\), the observation \({x_2,x_3}\) can be included. Especially, \(R_0\) is the partition for outlying observations. The TCLUST algorithm optimizes the set of parameters \(R_0,R_1,…, R_k\), the centers \(m_1,…, m_k\), p by p symmetric and positive semidefinite scatter matrices \(S_1, …, S_k\) and weights \(p_1,…, p_k\) such that it maximizes the objective function $$\sum_{j=1}^k \sum_{i \in R_j} log(p_j\phi(x_i;μ_j,S_j))$$ Here, the weights should satisfy the condition \(p_i \in [0,1]\) and \(\sum_{j=1}^k p_j=1\). This objective function can be interpreted as the sum of weighted log normal probability density function for each observation, giving the same weights if cluster is same. <br><br>

&nbsp;&nbsp;&nbsp;&nbsp;Before we take a look at the eigenvalue constraints, let’s think about the case where there are no restrictions on our objective function. Then, this gives a problem to clustering algorithm because maximization of objective function \(\sum_{j=1}^k \sum_{i \in R_j} log(p_j\phi(x_i;μ_j,S_j))\) without any constraint on scatter matrices(\(S_j\)) is not a well-defined problem. For example, if \(μ_j=x_i\) and \(det(S_j)\rightarrow 0\), then $$ϕ(x_i;μ_j,S_j)=\frac{exp{(-\frac{1}{2}}(x_i-μ_j)'S_j^{-1}(x_i-μ_j))}{\sqrt{2\pi}^pdet(S_j)^{1/2}}$$ goes infinite giving \(ϕ(x_i;μ_j,S_j)\) undefined. Therefore, imposing restriction is essential to make clustering problem solvable. <br><br>

&nbsp;&nbsp;&nbsp;&nbsp; To make our maximization of objective function well defined problem, we can introduce eigenvalue ratio restrictions on the cluster scatter matrices \(S_1, …, S_k\). Let’s denote \(λ_l(S_j)\) be a set of eigenvalues across all clusters scatter matrices \(j=1,…,k\) and data dimension \(l=1,…,p\). Then we can define the maximum of \(λ_l(S_j)\) as \(\max_{j, l}⁡λ_l(S_j)\) and the minimum of \(λ_l(S_j)\) as \(\min_{j, l}⁡λ_l(S_j)\). Eigenvalue ratio restriction is then defined as the ratio of maximum and minimum eigenvalue such that  $$\max_{j, l}⁡λ_l(S_j)/\min_{j, l}⁡λ_l(S_j)≤c$$ for some constant \(c≥1\). Here, c decides the strength of the constraint. If c is big, there is a weak constraint, and if c is small, there is a strong constraint. For example, If we set c=1, this implies \(\max_{j, l}⁡λ_l(S_j) = \min_{j, l}⁡λ_l(S_j)≤c\). Therefore, all clusters should have same axis length. <br>
</p>
<hr>

### 3. TCLUST algorithm  
<p align="justify" style='line-height:200%; font-size:120%'>
TCLUST algorithm gives robust clustering methods by trimming and cluster matrices constraints. There are various types of constraints that can be applied on cluster scatter matrices such as cluster covariance determinant, eigenvalues or both. Here, we only described the TCLUST algorithm having eigenvalue ratio restriction. In other words, the algorithm approximately maximizes the objective function $$\sum_{j=1}^k \sum_{i \in R_j} log(p_j\phi(x_i;μ_j,S_j))$$ under eigenvalue ratio constraint $$\max_{j, l}⁡λ_l(S_j)/\min_{j, l}⁡λ_l(S_j)≤c$$

&nbsp;&nbsp;&nbsp;&nbsp;The whole algorithm can be seen as a classification EM algorithm with concentration step. For each iteration we assign data points to the cluster (expectation step), trim the outlying observations (concentration step), and optimize parameters p, μ, S (maximization) according to the assignment result given on the concentration step. Our detailed examples for understanding TCLUST algorithm can be found on the supplementary documents section 1. <br>
</p>
<br>
### 3.1. Initialization step
<p align="justify" style='line-height:200%; font-size:120%'>
As EM algorithm repeatedly optimizes the objective function and update parameters, we need to set the initial parameter values. We first randomly choose (p+1) points for each cluster, therefore having select k×(p+1) observations. We choose (p+1) points in each cluster to avoid singularity of covariance matrices. For each cluster, by using those selected data points, we can calculate cluster centers m_j^0 and cluster scatter matrices \(S_j^0\) for \(j=1,…,k\).<br><br>

&nbsp;&nbsp;&nbsp;&nbsp;Here, when we calculate cluster scatter matrices, we should apply the eigenvalue ratio constraints. For the \(j^{th}\) cluster weights \(p_j^0\), at first, it is chosen at random. This initialization procedure is repeated several times to find the best clustering results through TCLUST algorithm. From the expectation step (section 3.2) to maximization step (section 3.4), those steps are executed until convergence. (i.e., \(θ^{l+1}=θ^l\)) or a maximum number of iterations is reached.<br>
</p>
<br>
### 3.2. Expectation step
<p align="justify" style='line-height:200%; font-size:120%'>
In the expectation step, the goal is to calculate posterior probabilities for each observation \(x_i\) and assign observations to a cluster which provides maximum posterior probability. Let the distance metric from an observation x_i to the center of cluster j (\(μ _j^l)\) at l^th iteration be \(D_j\) (\(x_i;θ^l)=p_j^l ϕ(x_i;μ_j^l,S_j^l)\). If \(D_j (x_i;θ^l)\) small, the distance of the \(x_i\) to \(μ_j^l\) is large. The posterior probabilities are defined as \(\frac{D_j(x_i;θ^l)}{\sum{j=1}^K{D_j(x_i;θ^l)}}\) where \(θ^l\) is the set of cluster parameters in the iteration l.
</p>
<br>

### 3.3.	Concentration step
<p align="justify" style='line-height:200%; font-size:120%'>
After we calculate posterior probabilities for each observation, we can trim [nα] observations. Let \(D(x_i;θ^l)\) be the maximum of \(D_j(x_i;θ^l)\) across all clusters for observation \(x_i\). Then, \(D(x_i;θ^l)\) is defined as $$D(x_i;θ^l )=max{D_1 (x_i;θ^l), …,D_k(x_i;θ^l)}$$ We can calculate \(D(x_i;θ^l)\) for all of the observations and sort it from smallest to largest. Then we trim the smallest [nα] observations as possible outliers. For the non-outlying observations, we can assign them to the clusters which provides the largest posterior probabilities (i.e. assign \(x_i\) to cluster j if \(D_j(x_i;θ^l)=D(x_i;θ^l)\)). As a result, we will now have the partition \(R_0,R_1,…, R_k\) for every observation. Here, \(R_0\) is the partition for outlying observations with smallest [nα] \(D(x_i;θ^l)’s\).
</p>

<p align="justify"> </p>
<br>

### 3.4. Maximization step
<p align="justify" style='line-height:200%; font-size:120%'>
In the maximizations step, the parameters \(θ^l=(p_1^l,…, p_k^l,μ_1^l,…, μ_k^l,S_1^l, …, S_k^l )\) are updated, based on non-discarded observations and their cluster assignments. Let \(n_j=\#R_j\) be the number of observations in cluster j. Then the weights are updated by \(p_j^{l+1}=n_j/[n(1-α)]\). In other words, we update weights proportional to the number of observations in cluster j. Also, the centers are updated by the sample means \(m_j^{l+1}=1/n_j \sum_{i∈R_j} x_i \). <br><br>

&nbsp;&nbsp;&nbsp;&nbsp;However, scatter matrices are not updated by sample covariance matrices because it may not satisfy eigenvalue ratio constraint. Instead, we use scatter matrices that are updated by truncated eigenvalues and spectral decomposition. First, we apply spectral decomposition of sample covariance matrix \(T_j=U_j' D_j U_j\) where \(U_j\) being an orthogonal matrix and \(D_j=diag(d_{j1},d_{j2},…, d_{jp})\) a diagonal matrix consist of eigenvalues. If we consider truncated eigenvalues such that <br> </p>
<p align="middle">
<img src="/assets/img/posts/math01.png" width="250px">
</p>
<p align="justify" style='line-height:200%; font-size:120%'>
with m as some threshold value, the scatter matrices are updated as \(S_j^{l+1}=U_j'D_j^* U_j\) with $$D_j*=diag(d_{j1}^{m_{opt}} ,d_{j2}^{m_{opt}},…,d_{jp}^{m_{opt}})$$  and  \(m_{opt}\)  minimizing $$m \longmapsto \sum_{j=1}^k n_j \sum{l=1}^p (log(d_jl^m+\frac{d_{jl}}{d_{jl}^m}))$$
These truncated eigenvalues with optimized m enable our updated scatter matrices meet the eigenvalue ratio restriction.
</p>
<br>

### 3.5 Evaluation
<p align="justify" style='line-height:200%; font-size:120%'>
	When the algorithm converges, we can calculate $$\sum_{j=1}^k \sum_{i \in R_j} log(p_j\phi(x_i;μ_j,S_j))$$ with parameters updated from the iterative expectation and maximization step.
</p>
<hr>

### 4. Conclusion
<p align="justify" style='line-height:200%; font-size:120%'>
Giving constraints on scatter matrices improves robustness on clustering and avoid unwell defined problem. Through the simulation study, we could conclude that TCLUST algorithm outperforms non robust k-means algorithm when there are some outliers or overlapping points in the bridge region. However, the problem where the algorithm would find the local maxima in the objective function still persists, similar to classical K-means. In which case, we would need to perform the TCLUST algorithm several times to ensure reasonable results. If time permits, we should also look into modifying the algorithm and propose a remedy to the problem such as better starting point in the initial steps, or using the robust covariance matrices for the clusters instead of the truncated covariance matrices.</p>
<hr>

### References  
<p align="justify" style='line-height:200%; font-size:120%'>
- Fritz, H., Garcıa-Escudero, L. A., & Mayo-Iscar, A. (2012). tclust: An R package for a trimming approach to cluster analysis. Journal of Statistical Software, 47(12), 1-26.  <br>

- Fritz, H., GarcíA-Escudero, L. A., & Mayo-Iscar, A. (2013). A fast algorithm for robust constrained clustering. Computational Statistics & Data Analysis, 61, 124-136.  <br>

- García-Escudero, L. A., Gordaliza, A., Matrán, C., & Mayo-Iscar, A. (2008). A general trimming approach to robust cluster analysis. The Annals of Statistics, 36(3), 1324-1345. <br>

</p>
<hr>
