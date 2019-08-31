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
This post is a summary of TCLUST algorithm by Fritz et al., and García-Escudero et al. The detailed listings of references are listed at the end of this post. All of the contents or ideas in this post are from these references. It is done as a Robust Statistics course project. This is a link for <a href="http://drive.google.com/uc?export=view&id=1a5COCf9MJIeG1u9mzsSqtsXkOHki9aNB" target="_blank">full report including examples and simulation studies</a>.
</p>

<hr>
<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-04.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-05.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-06.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-07.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-08.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-09.jpg" width="1000px">
</p>


<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-11.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-12.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-13.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-14.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-15.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-16.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-17.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-18.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-19.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-20.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-21.jpg" width="1000px">
</p>







<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-24.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-25.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-26.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-27.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-28.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-29.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-30.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-31.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-32.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-33.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-34.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-35.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-36.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-37.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-38.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-39.jpg" width="1000px">
</p>

<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-40.jpg" width="1000px">
</p>


<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-51.jpg" width="1000px">
</p>


<br>
<p align="middle">
<img src="/assets/img/slides/TCLUST/TCLUST_slides-52.jpg" width="1000px">
</p>
