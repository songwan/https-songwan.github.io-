---
title: Building R packages
layout: post
summary: My first R pacakge
categories:
    - R
thumbnail: posts/R.png
author: Songwan
---
----
### Note
The contents of this post are mainly from the book "R packages" by Hadley Wickham. For more details, visit [official website for this book](http://r-pkgs.had.co.nz/r.html).

----
### 1. Required packages & versions
- R version 3.2.0 or higher
- devtools
- roxygen2
- testthat
- knitr
- check with library(devtools); has_devel()

----
### 2. Package structure

----
#### 2.1 Naming packages
- Consists of letters, numbers, and periods.
- Starts with a letter, not end with a period.
- Not recommend to use periods.
- Avoid using both upper and lower case letters.

----
#### 2.4 What is a package?
There are 4 status in a package
1. Source packages
- development version of a package that lives on your computer (e.g. R/, DESCRIPTION, ...)
- might contain temporary files
2. Bundled packages
- package that's been compressed into a single file. (e.g., .tar.gz)
- Any files listed in .Rbuildignore are not included in the bundle.
- if you wish to exclude a specific file or directory, use anchor (e.g., ^notes$ for notes directory)
- The safest way to exclude a specific file or directory is to use devtools::use_build_ignore("notes")
3. Binary packages
- Used when you want to distribute your pacakge to an R user who doesn't have package development tools
- platform specific (Windows, Mac, ...)
- Use devtools::build(binary=TRUE) to make binary package
4. Installed packages
- binary package that's been decompressed into a package library.
5. In memory packages
- To use a package, you must load it into memory.

----
#### 2.5 What is a library?
- directory contraining installed packages.

----
### 3. R code
- 모든 R코드는 R/ 디렉토리 안에 저장됨.
- 각 함수마다 R 파일을 만들거나 한 파일에 함수를 다 집어넣지 말 것!
- 가장 좋은 방법은 주제별로 함수를 한 파일에 넣는 것.
- R파일명에 대문자 사용하지 말 것. (OS마다 case-sensitive 한 경우가 있음).
- R/ 디렉토리 내에 서브디렉토리는 생성불가함.

#### 변수명
- 변수명은 소문자로,  "\_"를 사용해서 단어 간 구분 (e.g, my_var)
- 변수명은 명사형, 함수명은 동사형을 쓰는게 좋음.
- 의미있는 변수명 사용

#### 띄어쓰기
- 연산자 전후로 띄어쓰기, 콤마 뒤 띄어쓰기, :, ::, :::는 띄울필요 없음.
- 왼쪽괄호 전에 띄우기 (함수 부를 때 빼고) (e.g. if (TRUE) do(x)).
- 중괄호 사용법, 예시참조. (e.g.
  if (x == y) {
    print("aa")
  }
  )

#### 기타
- 한 줄당 80단어 이하로 작성.
- indentation은 double space 사용 (tab 사용하지 말기)
- "<-" 으로 할당하기
- # 으로 코멘트 작성하기 (# 한칸 띄운후 사용)
- 단락 나눌 때는 # 설명 ------------------ 형식 사용하기
- CRAN에 submit 할 계획이면 ASCII 코드만 사용해야 함.

----
### 4. R 패키지에 데이터 포함하기
- usethis::use_data() 실행하면 data-raw 폴더가 생성 됨.
- 새 스크립트 창을 열어서 usethis::use_data(sample_data, compress = "xz")를 하면 data디렉토리에 sample_data.rda 파일이 저장됨.
- 데이터 생성 R스크립트 파일은 data-raw 폴더에 저장
- 이렇게 하면 라이브러리를 로드 할 때마다 데이터가 포함되어 있음. 
