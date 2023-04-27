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


## 2023-04-27

<p></p>

### 막대그래프를 그려봅시다

막대그래프 작성의 기초

-   데이터가 포함하고 있는 정포를 이해하기 쉽게 표현하는 과정을 데이터 시각화(data visualization)이라고 함.
-   막대그래프는 기본적인 데이터 시각화 도구.
-   막대그래프는 그룹별로 집계된 데이터를 표현하는 도구이기 때문에 막대그래프를 작성하기 위해서는 먼저      그룹별로 데이터를 집계하는 작업이 필요함.
-   도수분포표 계산 하기.
    ```r
    fav <- c("A", "B", "C", "A", "B", "C", "A", "A", "A", "B", "B", "C")
    fav
    table(fav)
    ```
-   막대그래프

    ```r
    ds <- table(fav)
    ds
    barplot(ds, main = "favorite")
    #막대그래프 그리기
    barplot(ds, main = "favorite", col = c("red", "blue", "green"))
    #색상 지정
    barplot(ds, main = "favorite", col = c("red", "blue", "green"), xlab = "xlab", ylab = "ylab")
    #색인 지정
    barplot(ds, main = "favorite", col = rainbow(4), xlab = "xlab", ylab = "ylab")
    #팔레트에서 색을 지정하여 사용하기
    barplot(ds, main = "favorite", col = rainbow(4), xlab = "xlab", ylab = "ylab", horiz = TRUE)
    #막대그래프를 수평방향으로 출력하기
    barplot(ds, main = "favorite", col = rainbow(4), xlab = "xlab", ylab = "ylab", names = c("1", "2", "3"))
    #X축 그룹의 이름 지정하기
    barplot(ds, main = "favorite", col = rainbow(4), xlab = "xlab", ylab = "ylab", names = c("1", "2", "3"), las = 2)
    #X축 그룸의 이름을 
    ```

-   실행 결과.
    ![0](0.png)

-   나이대별 인구 추정.
    ```r
    #데이터 입력
    age.A = c(13709, 10974, 7979, 5000, 4250)
    age.B = c(17540, 29701, 36209, 33947, 22487)
    age.C = c(991, 2195, 5366, 12980, 19007)

    ds = rbind(age.A, age.B, age.C)
    colnames(ds) = c('1970', '1990', '2010', '2030', '2050')

    par(mfrow=c(1,1), mar=c(5, 5, 5, 7))        #mar = 마진
    barplot(ds, main= '인구 추정'
      , col=rainbow(3)                          #col = 막대에 컬러주기(각각 지정 가능)
      , beside=T                                #beside = 그래프를 스택이 아닌 형태로 나타내기
      , legend.text=T                           #legend = 범례추가
      #, legend.text=c('0~14세', '15~64세','65세 이상') # 범례 내용 바꾸기
      , args.legend = list(x='topright', bty = 'o', inset=c(-0.25,0))
    )
    #x='topright' >> 범례를 출력할 기본 위치 지정
    #bty = 'o' >>>> 테두리 선 추가
    #inset=c(-0.25,0) >> 범례를 x축과 y축 기준으로 이동시킨다, y축은 위가아닌 아래쪽으로 이동된다.

    ```

-   히스토그램
-   외관상 막대그래프와 유사하나 막대사이에 간격이 있으면 막대그래프, 간격이 없으면 히스토그램
-   히스토그램에서는 막대의 면적이 의미가 있다.
    ```r
    head(cars)
    dist = cars[,2]
    dist
    hist(dist,
        , main='Histogram for 제동거리'     #제목
        , xlab='제동거리'                   #x축 레이블
        , ylab='빈도수'                     #y축 레이블
        , border='blue'                     #막대 테두리색
        , col='green'                       #막대 색
        , las=2                             #x축 글씨 방향(0~3)
        , breaks=5                          #막대 개수 조절
    )
    result = hist(dist                      #result에 데이터 선택해서 저장
        , main='histogram for 제동거리'
        , breaks=5)
    result                                  #result 출력
    ```

-   다중 그래프
-   zoom버튼 클릭 시 그래프를 크게 볼 수 있다.
-   zoom으로 그래프 창을 새로 띄웠을 경우 우클릭으로 복사가 가능하다.
    ```r
    par(mfrow=c(2,2), mar=c(3,3,4,2)) #화면분할(2*2)

    hist(iris$Sepal.Length
        , main='Sepal.Length'
        , col='orange')

    barplot(table(mtcars$cy1)
            , main='mtcars'
            , col=c('red','green','blue'))

    barplot(table(mtcars$gear)
            , main='mtcars'
            , col=rainbow(3)
            , horiz=TRUE)

    pie(table(mtcars$cy1)
        , main='mtcars'
        , col=topo.colors(3)           #topo팔레트 사용
        , radius=2)

    par(mfrow=c(1,1), mar=c(5,4,4,2)+.1) #화면분할 취소
    ```

-   원그래프
    ```r
    install.packages('plotrix')         #원그래프를 3d로 나타내기

    favor = c('WINTER', 'SUMMER', 'SPRING','FALL')
    ds = table(favor)
    ds
    library(plotrix)
    pie3D(ds                            #pie3D는 3d pie는 평면 원
        , main='선호계절'
        , radius=1
        , col=rainbow(3)
        , explode=0.1                   #여백
    )
    ```
-   선그래프
-   연도별 인구 증가와 같이 시간의 변화아 따라 수집된 데이터를 시각화하는 데 주로 사용
    ```r
    month = 1:12                                #데이터 입력
    late = c(5,8,7,9,4,6,12,13,8,6,6,4)           
    plot(month                                  #xdata
        , late                                  #ydata
        , main='지각생통계'                      #제목
        , type='l'                              #그래프 종류 선택(알파벳)
        , lty=1                                 #선의 종류 선택
        , lwd=1                                 #선의 굵기 선택
        , xlab='Month'                          #x축 레이블
        , ylab='Late cnt'                       #y축 레이블
    )
    ```


<p></p>
****************************************

## 2023-04-13 

### 파일 입출력에서 알아야 할 내용 : 결과물을 파일로 출력하는 방법

-   작업 폴더 지정
    ```r
    setwd('C:/Rwork')   //경로
    getwd() //출력
    sink('result.txt', append = T) //파일 출력 시작
    sink() //파일 출력 정지
    head(test) -> view(test) //airquality파일 출력
    ```

### 조건문
-   ifelse
    ```r
    job.type = 'A'
    if (job.type == 'B') {
        bonus = 200
    } else{
        bonus = 100
    }
    print(bouns)        //100 출력
    //else는 생략 가능
    // and = & / or = |
    ```

    ```r
    //삼항연산자와 비슷한 구조
    //구조 = ifelse(비교조건, 참일 때 값, 거짓일 때 값)
    a = 10
    b = 20
    c = ifelse(a>b, a, b)
    print(c)
    ```

### 반복문
- for문 구조
    ```r
    for(반복 변수 in 반복 범위(클론)){
        //반복할 명령문
    }
    for (i in 1:5){
        print('*')
    }
    for (i in 1:9){
        cat(i, '\n)
    }
    ```r
    
- while문 구조
    ```r
    sum = 0
    i = -1
    while(i <= 100) {
        sum = sum + i
        i = i+1
    }
    print(sum)
    `rrr

- apply() 계열 함수
    ```r
    // 매트릭스나 데이터프레임에 있는 행들이나 열들을 하나하나 차례로 꺼내 평균이나 합계 등을 구하는 작업을 수행할 때 유용
    apply(데이터셋, 행/열 방향 지정, 적용 함수)
    apply(iris[,1:4], 1, mean)  //행 방향으로 적용
    apply(iris[,1:4], 2, mean)  //열 방향으로 함수 적용
    ```

### 사용자 정의 함수
- 사용자 정의 함수 = 사용자가 스스로 만드는 함수
    /*함수명 = function(파라미터 목록){
        실행할 명령문
        return(실행 결과)
    }*/
    ```r
    mymax = function(x,y) {
        num.max = x
        if (y>x) {
            num.max = y
        }
        return(num.max)
    }

    mydiv = function(x, y=2) {
        result = x/y
        return(result)
    }                           // y=2 디폴트로 넣어서 y 생략 가능
    ```

-   저장과 재실행
    ```r
    //자주쓰는 함수를 파일로 만들어 저장해뒀다가
    setwd('C:/Users/user/Documents/test')           //wd경로
    source('C:/Users/user/Documents/test/mydiv.R')   //호출
    a = mydiv(20,4)
    print(a)
    ```

-   조건에 맞는 데이터 위치 찾기
    ```r
    score = c(76, 84, 69, 50, 95, 60, 82, 71, 88, 84)
    which(score==69)    //3
    which.max(score)    //min도 사용가능

    idx = which(score<=60)
    idx   // 4 6
    score[idx] = 61
    score   //76 84 69 61 95 61 82 71 88 84
    ```
    
    

*********************

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
        용도 : 하나의 값을 출력할 때 사용
        출력 : 데이터 프레임과 같은 2차원 자료구조를 출력
        특징 : 출력 후 자동 줄바꿈
    - cat함수
        용도 : 여러개의 값을 연결해서 출력할 때 사용
        특징 : 벡터는 출력되나 2차원 자료구조는 출력할 수 없음
        특징 : 출력 후 줄바꿈을 위해 \n입력 

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
