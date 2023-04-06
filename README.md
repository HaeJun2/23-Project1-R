# 이해준

README.md 작성요령 (파일이름 = 대문자)
1. 이름 : h1
2. 강의날짜 : h2
3. 학습내용 :  h2이하 자유 사용
4. 작성 코드
5. 최근 내용이 위에 오도록 작성
6. 날자 별 구분이 잘 가도록 작성

작성한 코드가 너무 길 경우 README말고 다른곳 저장(재사용 불가할정도로 길 경우)
*************


## 2023-04-06 R언어

### 매트릭스 - 행과 열에 이름 붙이기
    - > colnames(score) <- c('국어','영어','수학')
    - > rownames(score) <- c('john','tom','mark','jane')
             국어 영어 수학
        john   90   88   96
        tom    87   94   74
        mark   76  500   75
        jane   98   27   58
    - > score['john','국어']    # [1] 90
    - > score['mark',]          # 국어 영어 수학 
                                   76  500   75 
    - > rownames(score)         # [1] "john" "tom"  "mark" "jane"
    - > colnames(score)[2]      # [1] "영어"

### 데이터프레임
    - 매트릭스와 마찬가지로 2차원 형태의 데이터를 저장하고 분석하는데 사용되는 자료구조
    - 여러 자료형을 입력 가능

    > city = c("Seoul", "Tokyo", "Washington")
    > rank = c(1,3,2)
    > city.info = data.frame(city, rank)
    > city.info
                city rank
        1      Seoul    1
        2      Tokyo    3
        3 Washington    2
    
    - iris = 150그루의 붓꽃에 대해 4개 분야의 측정 데이터와 품종 정보를 결합해서 만든 데이터셋

### 데이터셋의 기본 정보 알아보기
    - dim(iris)                 #행과 열의 개수 보이기
    - colnames(iris)            #열 이름 보이기
    - head(iris)                #데이터셋의 앞부분 일부 보기 /뒷부분은 tail
    - str(iris)                 #데이터셋 요약 정보
    - levels(iris[,5])          #품종의 종류 보기(중복 제거)
    - table(iris[,"species])    #품종의 종류별 행의 개수 세기

### 매트릭스와 데이터프레임 다루기
    - colSums(iris[,-5])    #열별 합계/평균:Means   
    #-5는 5번째 컬럼을 제외(5번째 열은 str타입)

    - 행과 열의 방향 변환하기
        > z = matrix(1:20, nrow=4,ncol=5)   
    #행과열의 값과 데이터 개수의 값이 같도록 선언해줘야 한다.
        > t(z)      #행과 열 뒤바뀜
            [,1] [,2] [,3] [,4]
        [1,]    1    2    3    4
        [2,]    5    6    7    8
        [3,]    9   10   11   12
        [4,]   13   14   15   16
        [5,]   17   18   19   20

    - 조건에 맞는 행과 열의 값 추출
        > IR.2 = subset(iris, Sepal.Length>5.0 & Sepal.Width>4.0)
        > IR.2[,c(2,4)]
        Sepal.Width Petal.Width
        16         4.4         0.4
        33         4.1         0.1
        34         4.2         0.2
    
    - 산술연산
        > a = matrix(1:20,4,5)
        > b = matrix(21:40,4,5)
        > 2*a
                [,1] [,2] [,3] [,4] [,5]
            [1,]    2   10   18   26   34
            [2,]    4   12   20   28   36
            [3,]    6   14   22   30   38
            [4,]    8   16   24   32   40
        > a+b
                [,1] [,2] [,3] [,4] [,5]
            [1,]   22   30   38   46   54
            [2,]   24   32   40   48   56
            [3,]   26   34   42   50   58
            [4,]   28   36   44   52   60

    - 자료구조 확인
        > class(iris)           #iris 데이터셋의 자료구조 확인
        > class(state.x77)      #state.x77 데이터셋의 자료구조 확인
        > is.matrix(iris)       #데이터셋이 매트릭스인지 확인

    - 자료구조 변환
        is.matrix(state.x77)
        st = data.frame(state.x77)      #매트릭스인 state.x77을 데이터셋으로 변환
        head(st)
        class(st)
        #반대의 경우
        iris.m = as.matrix(iris[,1:4])

    - 데이터프레임 열 추출
        > iris$Species    

### 데이터의 입력과 출력
    > age = c('임의의 값')
    > young = min(age)  #age중 제일 낮은 값
    > old = max(age)    #age중 제일 높은 값

    - svDialogs패키지 다운로드 : install.packages('svDialogs')
                                library(svDialogs)
        >user.input = dlgInput('Input income')$res
        >user.input
        >income = as.numeric(user.input)    #문자열을 숫자로
        >income
        >tax = income * 0.05                #세금 계산
        >cat('세금 :',tax)
    
    - print함수
        1.하나의 값을 출력할 때
        2. 데이터프레임과 같은 2차원 자료구조를 출력할 때
        3. 출력후 자동 줄바꿈
    - cat함수
        1. 여러 개의 값을 연결해서 출력할 때
        ########작성필요

### 파일을 이용해 데이터를 읽고 쓰기
    - R에서 파일을 읽으려면 현재 작업 폴더와 파일 이름을 지정해야 한다
    > getwd()   #현재 작업 폴더 알아내기
    > setwd('C:/Users/user/Documents/test') #작업폴더 변경하기

    - csv파일 : R에서 데이터 분석을 위해 가장 많이 사용하는 파일 형태, 경로를 알고 있어야 하는 단점

    > air = read.csv('airquality.csv', header=T)    #csv파일 읽기
    > head(air)
        Ozone Solar.R Wind Temp Month Day
    1    41     190  7.4   67     5   1
    2    36     118  8.0   72     5   2
    3    12     149 12.6   74     5   3
    4    18     313 11.5   62     5   4
    5    NA      NA 14.3   56     5   5
    6    28      NA 14.9   66     5   6
    > class(air)    #csv자료구조 확인
    [1] "data.frame"
    
    - write.csv = 데이터 쓰기
    > my.iris = subset(iris, Species=='setosa')
    > write.csv(my.iris,'my_iris.csv',row.names=F)  #파일쓰기
    > read.csv('my_iris.csv', header=T)             #my_iris.csv읽기

    - 엑셀파일도 라이브러리를 설치해서 읽을 수 있음(csv만xlsx로 바꿔주면 가능)

    
    
**************


## 2023-03-23 R언어

### 윈도우 패키지 매니저
    - Chocolatey 
    - Winget
    - Scoop

### R 패키지 설치
    - R에서 콘솔창에 install.packages() 함수를 이용하면 알아서 설치
    - install.packages('ggplot2')
    - 파일영역의 package탭에서 확인 가능(Update버튼 = 패키지 업데이트, 체크된 패키지만 사용)
    - 함수 사용 : library(ggplot2)
                 ggplot(data = iris, aes(x = Petal.length, y = Petal.width) + geom_point())
    = library(cowsay)
       say("Hello world", by="cat")

### 도움말
    - 소스창에서 ?에 함수명을 붙이면 도움말 
        ex) ?sort
    - 세부사항 값 참조 예제 등 포함되어있음
    - Sys.time() : 시간

### 변수
    - 프로그램 내에서 값을 저장해 놓을 수 있는 보관소
    - 변수 만들기 : a <- 10     <-는 대입연산자 = 도 가능
    - 하나의 변수에는 하나의 값만 저장 가능
    - 변수 내용 확인하기 / 환경창에도 표시됨
        > total <- 5050
        
        > total
        [1] 5050

        > print(total)
        [1] 5050

        > cat('합계 = ', total)
        합계 =  5050

        > cat(total)
        5050

    - 작명 규칙
        1. 첫 글자는 영문자나 마침표로 시작, 이왕이면 영문자
        2. 두 번째 글자부터는 영문자, 숫자, 마침표, 밑줄 가능
        3. 변수명에서 대문자와 소문자는 별개의 문자 취급
        4. 변수명 중간에 빈 칸을 넣을 수 없음
    
    - 자료형
        1. 숫자형 : 1, 2, -4
        2. 문자형 : 'Tom',"Jane"
        3. 논리형 : true false  /   Ture가 1 False가 2
        4. 특수 값 : NULL, NA, NaN, Inf, -Inf
        - a는 숫자형 b는 문자형일 경우 print(a + b) 불가능

### 벡터
    - 배열처럼 여러 값을 저장할 수 있음
        > score <- c(68, 95, 83, 76, 90, 80, 85, 91, 82, 70)
        > mean(score)

    - 1차원 배열과 동일 

    - 수학에서의 벡터와 의미가 다름

    - 연속적인 숫자로 이루어진 벡터
        > v1 <- 50:80
         [1] 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64
        [16] 65 66 67 68 69 70 71 72 73 74 75 76 77 78 79
        [31] 80

    - []안의 값은 시작 인덱스, 화면 크기에 따라 가변적(인덱스는1부터 시작)
        > v5 <- rep(1,times=5)
        [1] 1 1 1 1 1
        > v8 <- rep(c('a', 'b', 'c'), each = 3)
        [1] "a" "a" "a" "b" "b" "b" "c" "c" "c"

    - 벡터에 이름 붙이기 key:value?
        > absent <- c(8, 2, 0, 4, 1)
        > names(absent) <- c('MON','TUE','WED','THU','FRI')
        > absent
        MON TUE WED THU FRI 
        8   2   0   4   1 
        > absent[i] : 해당 인덱스 키,값 출력
        > absent[1:3] : 1~3 자료 출력
        > absent[1,5,2] : 1부터 5까지 2의 간격으로
        > absent[-2] : 인덱스 2를 제외한 나머지
        > absent[-c(3:5)]
        > named numeric(0)
        -- 눈에 익히기, 외울 필요 없음

### 함수
    - 값을 입력받아 정해진 계산을 수행한 후 결과값 f(x)를 돌려줌
    - 매개변수(parameter) : 함수의 입력값을 받는 변수
        >str <- paste('good','morning', sep=' / '
        >str
        [1] "good / morning"
    
### 벡터의 활용
    - 자료 분석은 자료에 담긴 // 필요


************
## 2023-03-16 R언어

### 공용PC git 계정
    - 공용PC의 경우 강의실 도착하면 등록된 git계정 확인
    - 끝날때 사용자 이름/이메일을 선택하여 삭제
    >> git config --global --unset user.name 사용자이름/이메일

### R언어 특징
    1. 데이터 분석에 특화
        -  통계를 포함한 데이터 분석 작업에 활용할 목적으로 개발
        -  컴파일 과정 없이 바로 컴파일

    2. 사용자 커뮤니티
        -  초보자를 위한 학습 자료가 풍부, 사용자층이 두터움

    3. 다양한 패키지 제공
        -  데이터 분석에 사용되는 함수들을 종류별로 묶어 패키지로 제공
        -  데이터 분석에 필요한 거의 모든 기능 제공
        -  최신 이론 발표 시 바로 패키지가 만들어져 신속하게 활용 가능

    4. 미적이고 기능적인 통계 그래프 제공
        -  데이터분석은 결과를 시각적으로 표현하는게 중요
        -  ggplot패키지 이용

    5. 편리한 프로그래밍 환경 (IDE)
        -  모든작업을 R스튜디오 내에서 처리 가능 

    6. 무료 사용
        - 오픈소스
        - 1년에 1~2번 정기적으로 업데이트

### R을 배우는 이유
    - 4차 산업혁명의 중심은 '데이터'
    - 전공을 불문하고 어떤 분야로 진출하든 점점 더 중요한 스팩
    
### chatGPT
    - 유저와 대화하는것은 학습하지 못함(불완전한상태)

### 리눅스를 사용하는 이유
    - 패키지매니저(윈도우 : 초코레이티)
    - 개발자용 프로그램이 리눅스가 제일 먼저 출시됨
    - 오픈소스
    - 저가용 노트북에서도 원활하게 운영체제가 가동됨


### R 설치
    - 디폴트로 설치

[R설치](https://cran.r-project.org/mirrors.html, "R link")

    
### R스튜디오 설치
    - PRODUCTS > R Studio IDE > 하단에 Open Source Edition
    - 해당 링크에서도 R언어 다운로드 가능
    - 디폴트로 설치

[R Studio설치](https://posit.co/, "R Studio link")

### R
    소스 / 콘솔 / 환경 / 파일영역 총 4가지로 나뉘어짐
    = 를 <-로 대체해서 사용(대입)
    파일영역의 ... 으로 디렉토리 변경한 후
    More의 set as working directory

    A <- 51:80
        - A에 51부터 80까지 하나씩 대입
        - 환경영역 보면 A변수의 인덱스와 값이 나오는데 인덱스가 1부터 시작함(비전공자도 쉽게 이해하기 위해)
    
    print(A)
        - A 출력

    콘솔창에서 괄호를 하나 빠뜨리고 엔터키를 치면 한 줄이 끝났다고 
    생각하지 않고 마저 입력하라고 >가 +로 변함, 마저 입력 가능 

    2의 3제곱 = 2^3
    나머지 = 5%%4
    주석 = #
    
    R은 인터프리터 방식의 언어(스크립트 언어)





*********************
## 2023-03-09 R언어

GIT, VSCODE연동
GIT홈페이지 보면PRO GIT 책이 있고 한국어로 된 PDF도 받을 수 있음
양이 많지만 받아두고 가끔 읽어보기

단순 명령어 set - 어디 걸어가라, 몇번버스를 타라
복잡 명령어 set - 안양역으로 가라

기존 cpu들은 복잡명령어 사용 - cpu연산으로 인해 뜨거워짐
 m1칩 출시 - 단순명령어 사용으로 발열x

R언어 - 비교적 최근에 나온 언어 중 데이터를 다루기 가장 쉬움
데이터에 특화되어있는언어
S-PLUS의 무료버전형태

BSD - 버클리대학에서만든 리눅스(기본만갖춤)
BSD기반으로 MACOS 개발
커널 - 하드웨어 호환 커널
