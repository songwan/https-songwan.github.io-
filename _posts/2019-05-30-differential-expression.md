---
title: Differential expression analysis
layout: post
summary: Differential expression, Multiple testing adjustment, FWER, FDR
categories:
    - Biostat
thumbnail: posts/DEanalysis.png
author: Songwan
---
<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

<hr>s
#### 알림
이 포스팅은 2019년 <a href="https://canvas.harvard.edu/courses/49497/pages/course-schedule" target="_blank"> Harvard STAT115강의</a>를 요약한 것임을 알려드립니다.
<hr>
#### 다룰 토픽  
- Differential expression : Fold change, T* test on normally distributed data, empirical Bayes method
- Multiple test adjustment : FWER, FDR
<hr>

#### Heatmap : Expression level visualization
다음 그림은 암의 종류 (ALL, AMLL)에 따른 gene expression level을 그림으로 나타낸 것이다. 각 행은 gene을, 열은 sample을 의미하며, 빨간색으로 갈 수록 expression level이 높고, 파란색으로 갈 수록 expression level이 낮다고 볼 수 있다. 주의해야 할 점은 row의 ordering이 매우 중요하다는 것이다. 어떻게 ordering을 하느냐에 따라 visualization이 매우 달라질 수 있다.
<p align="center"> <img src="/assets/img/posts/DEanalysis2.png"  width="30%"></p>

<hr>
#### 어떻게 우리는 Differential expression의 정도를 계산할까?  
1) **Fold change (Avg(X) / Avg(Y))**를 사용하는 것 (Naive method)
> - MAS4, MAS5, dChip
>> - Natural scale을 사용하므로 바로 fold change 계산
> - RMA를 사용하는 방법 (microarray 포스팅 참고)
>> -  RMA는 log scale을 사용하기 때문에 샘플 X와 sample Y의 평균 expression level을 빼면 log(Avg(X)) - log(Avg(Y)) = log(Avg(X)/Avg(Y))이다. 따라서 fold change (Avg(X) / Avg(Y))를 계산하려면 두 로그값의 차이에 **exponential**을 취해주어야 한다. 그렇지 않으면 geometric mean을 게산한 것이 된다.  

> - 예시 : 다음과 같이 Gene 1, 2와 Gene 3에 대한 3개의 Treatment sample (T1, T2, T3), 3개의 Control sample (C1, C2, C3)와 Fold change 값 (FC)가 있다고 하자.  
<p align="center"> <img src="/assets/img/posts/deexample.png"  width="65%"></p>  
> - FC = 36.67은 Treatment group에서 크게 overexpressed된 것을 알 수 있고, FC = 1.875은 Treatment group에서 약간 overexpressed된 것을 알 수 있다.    
> - 다른 예시를 보자.  
<p align="center"> <img src="/assets/img/posts/deexample2.png"  width="50%"></p>  
> - Gene 4를 보면 Control보다 Treatment에서 더 높은 값을 가짐을 알 수 있다. 반면 Gene 5에서는 Control과 Treatment에 따른 차이가 크지 않다. 하지만 FC값은 2.213으로 동일하다. **여기서 Fold change사용의 문제점이 드러난다.**  따라서, differential expression level의 confidence를 줄 수 있는 다른 통계량이 필요하다.
<hr>
2) **T-test** (데이터가 정규분포를 따르는 경우)
> - T-test는 데이터가 Normal을 따른다는 가정이 필요하다.
> - 우선, 데이터가 Normality assumption을 만족하는지 알아보기 위해 QQ Plot을 그린다.
<p align="center"> <img src="/assets/img/posts/qqplot.png"  width="50%"></p>  
<hr>
3) **Wilcoxon Rank Sum Test** (데이터가 정규분포를 따르지 않는 경우)
- 행에 있는 모든 데이터에 순위를 매긴후, Treatment와 Control그룹의 랭크의 합을 각각 $$T_T$$ 와 $$T_C$$라 하자.
- 예) 10개의 normal sample (control) 과 10개의 cancer sample (treatment)이 있다고 하면, min(T) = 55 ( = 1 + 2 + ... + 10)이고 max(T) = 155 ( = 11 + 12 + ... + 20)이다.
- Significance rule은 permutation에 의해 결정되는데, 예를 들어 위의 예시의 경우, 랜덤으로 많은 수의 조합 (permutation)을 simulation해서 분포를 그려보면 다음과 같다.
<p align="center"> <img src="/assets/img/posts/permutation.png"  width="50%"></p>  
- 이 경우, T = 150 이상일 경우에 Significant하다고 할 수 있다. 여기서 150이라는 숫자는 U table (transformation of T)에서 도출할 수 있다.
- 하지만 이 방법은 nonparametric한 방법이므로, 샘플의 수가 적을 땨에는 power이 작다는 단점이 있다.
<hr>
#### Linear Model for Differential Expression
> - Linear model : $$Y_{ijk} = \mu_{j} + \alpha_{ij} + error_{ijk}$$ 은 **각 gene j마다의 seperate한 linear model**로써,
>> - $$k$$ : 특정 sample
>> - $$Y_{ijk}$$ : RMA analysis를 통한 expression index
>> - $$\mu_{j}$$ : gene j의 전체 experiment (RMA expression index)에 대한 평균 expression level
>> - $$\alpha_{ij}$$ : i-th condition의 overall mean ($$\sum_{i}\alpha_{ij}=0$$)으로부터의 편차(deviation)
> - 이 모델에서, 3개의 treatment (mutant)와 3개의 control (wildtype)에 대해, 귀무가설 $$H_0$$ : $$\alpha_{mu}$$ - $$\alpha_{widetype}$$ $$= 0$$에대해 검정한다.

<hr>
