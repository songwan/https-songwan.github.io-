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
#### Chapter 1. Introduction

복습 : 2 sample t-test  
목표 : Parametric한 가정 없이 어떻게 t-test와 같은 검정을 시행할 수 있을까?

<hr>

#### 1. Measurement Scale
Nominal scale : 대상을 categorizing / classifying하는데 사용되는 category / class
- 크기나 우열을 가릴 수 없음
- 예) 빨강, 하양, 파랑
- 예) 짝수, 홀수
- 예) 남자, 여자

Ordinal scale : 대상을 큼, 작음, 같음과 같은 상대적인 순서에 따라 raning을 매김.
- 예) 중년, 청년, 노인

Interval scale : 대상간 **상대적인** 순서가 있거나, 크기의 차이가 있다. 또한, 0점이 존재하고, 단위거리 (unit distance) 가 존재한다.
- 예) 개인의 나이
- <p align="middle"><img src="/assets/img/posts/npintro.png"  width="60%"></p>

Ratio scale : **Natural** 0 point를 가지는 특별한 경우의 Interval scale
- 예) 나이, 몸무게
- 예) 온도는 Ratio scale이 아님
- Interval scale과 Ratio scale은 명확히 구분이 안됨. 동시에 해당되는 경우도 있음.

<hr>
#### 2. 비모수 (혹은 distribution free) methods의 정의
- 측정당시에 **nominal**, 혹은 **ordinal** scale 인 데이터를 사용한 방법론.
- 측정당시에 **Interval** 혹은 **ratio** scale인 데이터를 데이터의 분포가 정해졌거나 정해지지 않았을때 사용되는 방법론. (단, 무한개의 파라미터를 가진 경우는 제외한다.)

<hr>

#### 3. 가설 검정
Goal : Type 1 에러를 컨트롤 하면서 Type 2 에러를 최소화 하는 것
- 죄수의 예시로 왜 $$\alpha$$가 중요한 지 생각해보기

<p align="middle"><img src="/assets/img/posts/nphypotest.png"  width="40%"></p>

Type 1 error rate
- = $$\alpha$$
- significance levels
- = P(reject H0 | H0 True)

Type 2 error rate
- = $$\beta$$
- = P(Accept H0 | H0 False)

Power
- = $$1-\beta$$
- = P(Reject H0 | H0 False)
- = P(Reject H0 | H1 True)

**Unbiasedness**
- 만약 $$\alpha \leq Power = 1 - \beta$$ 이면 test가 unbiased라고 한다.

**Consistency**
- 어떤 가설검정이 H1클래스 내에서의 모든 다른 alternatives에 대해 consistent하다는 것은 $$ n \rightarrow \infty $$함에 따라 $$Power \rightarrow 1$$인 경우를 말한다.
- 예시 : 전체 출생 인구 중 남아의 수
> - H0 : $$p = 1/2$$ vs H1 : $$p = p_1 \neq 1/2 $$
> - 노트 참고

<hr>
#### 4. Relative efficiency of tests
- 주어진 $$H_0, H_1, \alpha$$에 대해, $$Power_1(n)$$을 $$T_1$$의 Power이라 하고 $$Power_2(n)$$을 $$T_2$$의 Power라고 하자.
- $$1-\beta$$를 고정된 power 수준이라고 하고, $$Power_1(n_1) = Power_2(n_2) = 1-\beta$$라고 하자.
- 그러면, $$n_2/n_1$$를 T1에서 T2로의 **relative efficiency**라고 한다.
<hr>
#### Chapter 2. The Dichotonous Data Problem  
CH 2.1 (Binomial test), CH 2.2 (Point estimation for p), CH 2.3 (Confidence Interval for p)는 기초이므로 책 읽어보기.
<hr>
#### Supplement to Chapter 2.  
Randomized tests (one-tail)  
1) Type 1 error at a Binomial Test
> - Consider H0 : p= 0.6

<hr>
