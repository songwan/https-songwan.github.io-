---
title: Introduction to Nonparametric Statistics
layout: post
summary: Nonparametric Statistics
categories:
    - NonparametricStatistics
thumbnail: posts/npintro.png
author: Songwan
---
<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<hr>
#### 참고문헌
1. R과 함께 비모수 통계학, 김홍기, 자유아카데미
2. Myles Hollander, Douglas A. Wolfe and Eric Chicken. Nonparametric statistical methods. 3rd edition. Wiley, 2014.
<hr>
#### 1장. 서론
<hr>
#### 1.1 비모수적 방법  
**통계학**의 분류
> - **기술통계학 (descriptive statistics)** : 데이터를 기록, 정리하고 데이터가 갖고 있는 특징을 요약
> - **추측통계학 (inferential statistics)** : 데이터가 갖고 있는 정보를 기초로 하여 불확실한 사실에 대한 추측을 하거나 의사결정
>> - 추정 (estimation)
>> - 가설검정
>> - 위치문제 location
>>> - 정규분포 가정 하에서는 **표본평균** (불편추정량, 중김극한정리 성립, 모평균에 대한 최소분산 불편추정량, 최량추정량)을 많이 사용함. 그러나, 표본통계량의 분포가 정규분포에 수렴하는 속도가 아주 느리거나, 이상점을 포함한 데이터의 경우, 표본평균에 기초한 추정이나 검정의 효율이 급격히 떨어짐. 이럴 때에는 비모수적 방법을 사용하는 것이 좋음.
>> - 척도문제 scale
>> - 일원/이원배치법
>> - 회귀모형
>> - 독립성 문제
<hr>
**통계적 추론 (statistical inference)**의 분류
> - 모수적 방법
> - **비모수적 방법** : 일반적으로 순수 비모수적 방법과 분포무관 방법을 구별하지 않고 씀
>> - **순수 비모수적 방법 (truly nonparametric)**
>>> - 모집단의 모수 자체에 관심을 두지 않는 통계적 밥법
>> - **분포무관 방법 (distribution free)**
>>> - 귀무가설 하에서 검정통계량의 분포가 모집단 분포와 무관한 검정법
> - 베이즈적 방법
>> - 분포무관 신뢰구간
>>> - 신뢰구간이 모집단의 분포함수에 영향을 받지 않는 구간추정법
<hr>
장점
> - 데이터가 구간척도 (interval sacle)이나 비율척도 (ratio scale) 등으로 주어지지 않고, **순위척도 (ordinal scale)**로 주어져서, 상대적인 크기로 데이터가 주어질 경우에 유용한 분석 방법.

단점
> - 복잡한 분포, 이론전개가 어려움. 소표본 (small sample) 분포를 이용할 수 없으며, 점근분포의 성질에 의존하는 경우가 많음

<hr>
