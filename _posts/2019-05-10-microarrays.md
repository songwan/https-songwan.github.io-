---
title: Microarrays
layout: post
summary: Gene Expression Microarrays
categories:
    - Biostat
thumbnail: posts/microarray2.png
author: Songwan
---
<hr>
#### 알림
이 포스팅은 2019년 <a href="https://canvas.harvard.edu/courses/49497/pages/course-schedule" target="_blank"> Harvard STAT115강의</a>를 요약한 것임을 알려드립니다.

<hr>
#### Affymetrix GeneChip Arrays
1995년경 Stanford 대학에서 발명한 Gene expression을 측정하는 도구로, 현재 Affymetrix라는 회사서 판매하고 있다. 아래 그림은 microarray의 구성을 나타내고 있다. 각 프로브(칸) 마다 여러 개의 미리 세팅된 염기서열이 있다. 이에 대응되는 (예를 들면 A-T, C-G) 우리가 분석하고자 하는 DNA의 염기서열이 달라붙음으므로 염기서열을 알아낼 수 있다.
<p align="center">
<img src="/assets/img/posts/GeneChip.jpg"  width="10%"> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img src="/assets/img/posts/microarray2.png"  width="40%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img src="/assets/img/posts/microarray3.jpg"  width="40%">
</p>

Microarray방법은 실험 오차를 줄이기 위하여 최소 3개의 replicates를 두는 것이 좋다. 그러나, 현재, 기술의 발전으로 **genome-wide expression array**는 잘 쓰이지 않는다. 왜냐하면 대안인 RNA-seq의 비용이 크지 않고, 더 정확한 (실험 오류가 적은)분석을 할 수 있고, 이미 공공데이터가 많이 개방되어있으며, RNA-seq로 여러 data analysis를 할 수 있다는 장점이 있기 때문이다.

> - Microarray로 이제 새로운 데이터를 생성하지는 않지만, NCBI에는 GEO (Gene expression omnibus)라고 불리는 여러 microarray로부터 측정된 gene expression level 데이터가 존재한다.

<hr>
#### Affymetrix Microarray Data
Microarray로 측정된 데이터는 **cell file**에 저장된다. **cell file**의, raw data는 다음과 같이 생겼다.  

> | X | Y | MEAN | STDV | NPIXELS |
|----------|----------|----------|----------|
| 701 | 523 | 311.0 | 76.5 | 16 |
| 702 | 523 | 48.0 | 10.5 | 16 |  

> - (X, Y) : 프로브 위치, 하나의 프로브에는 여러개의 PIXEL이 존재
> - MEAN : 평균 gene expression level
> - NPIXELS : 각 프로브 마다 가장 중간의 NPIXELS개의 픽샐만을 선택해 expression level을 산출. (경계는 오염될 수 있기 때문.)

Microarray 디자인에 대한 정보는 **cdf file**에 저장된다.

> - (X, Y)에 해당하는 프로브가 어떤 sequence에 해당되고 어떤 transcript를 타겟팅하는지에 대한 정보
> - MM (MisMatch) probes는 거의 항상 PM (Perfect Match) probe 바로 옆에 있다.


**Perfect Match (PM)** and **MisMatch (MM)** : control for cross hybridization
> - 프로브를 생산 (hybridization) 하는 과정에서 RNA를 cDNA로 복제하는데, 이 과정에서 cDNA가 원 RNA와 염기서열이 동일하다면 PM, 동일하지 않다면 MM이라고 한다.
> - MM은 분석에서 background noise를 측정하는 데에 사옹된다. PM과 MM의 expression level의 차이를 비교해보 real signal이 무엇이고 noise가 무엇인지 식별하는 데 도움이 된다.
> - 나중에는 PM만을 사용하게 됨 (후에 설명함).

<p align="center"> <img src="/assets/img/posts/MMPM.jpg"  width="50%"></p>


Probe Definition file (cdf file)
> - 하나의 gene이더라도 여러 요인에 의해 다른 RNA나 transcript가 생성되기 때문에 데이터는 모두 다르고, cdf file 또한 여러 버전으로 나누어져 있다. (cdf for genes, cdf for transcripts, ...)
> - 분석의 목적에 따라 cdf 파일을 알맞게 선택해야 한다. 만약 reference gene detection (transcript만 알고 싶어하는 경우)이 목적이라면 그에 해당하는 cdf파일을 선택해야 한다 (refseqmRNA).
> - 가장 최신의 cdf annotation 사용하는 것이 좋다. (과거의 annotation과 30%가 다를 수 있음, bioConductor를 최신버전으로 사용)

<hr>
#### Microarray Normalization
sdfsd
