---
title: Introducing Biostatistics
layout: post
summary: History of Biostatistics
categories:
    - Biostat
thumbnail: posts/biostatintro.png
author: Songwan
---
<hr>
#### 알림
이 포스팅은 2019년 <a href="https://canvas.harvard.edu/courses/49497/pages/course-schedule" target="_blank"> Harvard STAT115강의</a>를 요약한 것임을 알려드립니다.

<hr>
#### Protein Sequencing
초기 Bioinformatics 연구는 **Protein Sequencing**에 집중되었다. 다음은 protein sequencing의 역사에 대해 간략히 보여준다.

> - Sanger Sequencing (1955)
> - Smith-Waterman algorithm (fast sequence alignment algorithm, 1970)
> - PDB (Protein structure Database, 1973)
> - BLAST algorithm (fast search to find similar sequence from DB, 1990)
> -BLOCKS database (functional sequence, 1994)
> - CASP competition (developing algorithm for prediction of structure from a partial sequence, 1994)
> - Proteomics (전체(total) 단백질 연구, 1997)
> - Proteomics in genomics (protein level을 추정하기 위해 genomics를 활용하기 시작, 2017 - )

최근 (Dec 03, 2018) 구글 딥마인드 랩에서는 **AlphaFold**라는 것을 제작하였다고 한다. 이전동안 protein structure prediction은 생명과학분야에서만 다루었다. 하지만 이번 구글의 딥러닝 기술을 활용한 AlphaFold가 기존의 CASP13 protein-folding competition에서 우승을 하면서 크게 주목받게 되었다.

> - <a href="http://dongascience.donga.com/news/view/30213" target="_blank"> 관련기사 ([Science토크]‘알파폴드’ 쇼크로 치열해지는 단백질 구조 분석 경쟁, 동아사이언스 </a>
> - <a href="https://deepmind.com/blog/article/alphafold" target="_blank"> AlphaFold: Using AI for scientific discovery </a>
> - <a href="https://kstatic.googleusercontent.com/files/b4d715e8f8b6514cbfdc28a9ad83e14b6a8f86c34ea3b3cc844af8e76767d21ac3df5b0a9177d5e3f6a40b74caf7281a386af0fab8ca62f687599abaf8c8810f" target="_blank"> 관련 논문 (De novo structure prediction with deep-learning based scoring) </a>

<hr>
#### Microarray
<p align="center">
<img src="/assets/img/posts/microarray.png"  width="20%">
</p>
1995년에 스탠포드 대학에서 Microarray를 발명하였다. 마이크로어레이는 동시에 여러개의 gene expression level을 검사할 수 있다. 마이크로어레이의 probe에 있는 색상이 gene expression level의 정도를 나타낸다. 오늘날 microarray기술은 한 번에 1000 probe까지 분석 할 수 있다. 또한 전체 gene expression level이 아니라 일부분의 gene expression level을 가지고도 이미 나와있는(이전에 분석하여 공공으로 개방된) 데이터와 결합하여 어떤 cell인지 유추할 수 있다.

> - **<a href="https://clue.io/cmap" target="_blank">Connectivity Map (CMAP)</a>** : 이러한 일부분의 gene expression level데이터를 가지고 전체를 유추하는 프로젝트
<hr>

#### DNA Sequencing Wave
그 이후로는 DNA의 구조에 관한 연구가 활발히 진행되었다.
> - DNA structure (1953)
> - Recombinant DNA (재조합 DNA, DNA를 효소를 이용해 자르고 재조합하기 등. 1972)
> - Sanger sequencing (DNA를 sequencing함, 1977)
> - PCR (DNA sequence를 분석하기 전 amplify하는 방법 개발, 1985)
> - NCBI (National Center for Biotechnology and Information, PubMed가 NCBI산하 프로젝트임, 1988)
> - BLAST (Fast sequencing algorithm, 1990)

현재 DNA sequencing 기술이 발전하여 비용과 가격이 많이 줄어들으며, 개인의 DNA sequence를 분석하여 personalized disease susceptibility test를 하기도 한다.
> - **High-throughput sequencing (HTS)** : **next generation sequencing (NGS)**라고도 불린다. 이전에 쓰이던 Sanger sequencing을 대신한 빠른 속도의 sequencing 방법을 의미한다. <a href="https://www.youtube.com/watch?v=womKfikWlxM" target="_blank"> 소개 영상 </a>

<hr>
#### Bioinformatics와 Computational Biology의 차이점
> - Computational Biology : 컴퓨터를 이용해 biology를 연구하며, living system에 관한 연구를 진행, 과학.
> - Bioinformatics : 문제를 해결하기 위해 알고리즘이나 데이터베이스를 생성하는 것, 엔지리어닝.
> - 두 용어는 같은 의미로 사용되기도 한다.

<hr>
#### 토픽
Transcriptome (전사체, 어떤 종류의 세포, 또는 조직에서 어느 순간에 발현중인 RNA의 총합)
> - Microarray
> - RNA-seq
> - Single cell RNA-seq

Gene regulation
> - Motif finding
> - ChIP-seq
> - Epigenetics
> - GWAS interpretation

Cancel genomics
> - TCGA
> - CRISPR screens
> - cancer immunology
