#---------------------------------------------------

# 6.2 연산자

y <- 3
y

x <- c(1, 2, 3, 4)
y <- c(2, 2, 2, 2)
z <- x + y    # 더하기 연산
z

z <- x * y    # 곱하기 연산
z

x <- c(1, 2, 3, 4)    #  x변수에 1,2,3,4를 할당. 즉 x의 길이는 4 
y <- c(1, 2)    # y변수에 1,2를 할당. 즉 y의 길이는 2
z <- x * y
z

10 - y    # 10에서 1,2를 뺌

x <- 4
y <- 2
x + y    # 더하기
x - y    # 빼기
x * y    # 곱하기
x / y    # 나누기
x ^ y    # 거듭제곱
x %% y    # 나눈 나머지
x %/% y    # 나눈 몫

x <- c(1, 2, 3)
y <- c(1, 2, 5)
x < y    # x보다 y가 큰가?
x >= y    # x는 y와 같거나 큰가?
x == y    # x는 y와 같은가?

x <- c(1, 2, 3)
y <- c(1, 2) 
x <= y

x <- c(TRUE, TRUE)
y <- c(TRUE, FALSE)
x & y
x | y

x && y
x || y

c(1 == 1, 2 == 2) & c(1 == 1,3 == 4)    #c(TRUE, TRUE) & c(TRUE, FALSE)와 같음
!(c(1 == 1, 2 == 2) & c(1 == 1,3 == 4))   

x <- c("a", "b")


#---------------------------------------------------

# 6.3 데이터 가져오기와 내보내기

x <- read.csv("C:/R/practice_project/r_practice/reservation_r_csv.csv")
head(x)    # 데이터 앞부분을 확인

install.packages("readxl")    #  패키지 설치
library(readxl)    # 패키지 로딩

y <- read_excel("C:/R/practice_project/r_practice/reservation_r_excel.xlsx")
head(y)

write.csv(reservation_r_csv, "csv_output.csv")

install.packages("writexl")    # 패키지 설치
library(writexl)    # 패키지 로딩
write_xlsx(reservation_r_excel, "excel_output.xlsx")    # 엑셀 파일로 내보냄

sink("output.txt")    # 출력을 output.text에 기록 시작
x <- 1
y <- 2
x
y
x+y
sink()    # 기록 마침

x <- c(1, 2, 3)
y <- c(4, 5, 6)
save(x, y, file = "save.Rdata")   # save.Rdata파일에 x와 y변수 내용 저장

rm(list = ls())    # 메모리의 변수를 모두 삭제
load("save.Rdata")    # save.Rdata의 내용을 불러옴

x <- c(1, 2, 3)
y <- c(4, 5, 6)
z <- c(7, 8, 9)
save(list = ls(), file = "save2.Rdata")    # 현재 변수들을 저장

connect <- file("result.txt", "w")    # 파일 설정
x <- iris$Sepal.Length
cat(summary(x), file=connect)    # summary함수의 결과를 파일에 기록
close(connect)    # 파일 종료

#---------------------------------------------------

# 6.4 데이터 확인하기

head(iris)    # 데이터셋 앞부분을 출력
head(iris, 10)

tail(iris) # 데이터셋 뒷부분을 출력

summary(iris)    # iris 모든 열의 요약 통계량을 출력
summary(iris$Sepal.Length)

str(iris)

View(iris)

dim(iris)    # 차원을 셈 iris는 150행 5열
nrow(iris)    # 행의 개수를 셈
ncol(iris)    # 열이 개수를 셈

length(iris)    # iris 열의 길이를 셈
x <- c(1, 2 , 3, 4, 5, 6, 7, 8, 9, 10)
x
length(x)    # x의 길이를 셈

ls()    # 변수 목록을 확인

x <- c(1, 2, 3, 4, 5)
object.size(x)    # 변수의 크기를 확인

x <- c(1, 2, 3, 4, 5, 6, 7, 8, NA, 10)    # 결측치(NA)하나 포함
x

is.na(x)    # 개별 데이터가 NA인지 확인
is.null(x)    # 데이터셋이 null인지 확인
is.numeric(x)    # 데이터셋이 숫자형인지 확인
is.character(x)    # 데이터셋이 문자형인지 확인
is.logical(x)    # 데이터셋이 논리형인지 확인
is.factor(x)    # 데이터셋이 팩터 구조인지 확인
is.data.frame(x)    # 데이터셋이 데이터 프레임 구조인지 확인

#---------------------------------------------------

# 6.5 데이터 조작하기

x <- c(1, 2, 3, 4, 5)
y <- c(6, 7, 8, 9, 10)
rbind(x, y)    # x와 y를 행으로 합침
cbind(x, y)    # x와 y를 열로 합침

df <- data.frame(name = c("a", "b"), score = c(80, 60))    # 데이터 프레임 생성
df
cbind(df, rank = c(1, 2))    # rank 열 추가

split(iris, iris$Species)    # Speccies 기준으로 데이터를 분리

subset(iris, Sepal.Length >= 7)
subset(iris, Sepal.Length >= 7, select = c("Sepal.Length", "Species"))    # Sepal.Length, Species 열만 선택

substr(iris$Species, 1, 3)    # 첫번째 자리부터 세번째 자리까지 선택

x <- data.frame(name = c("a", "b", "c"), height = c(170, 180, 160))    # 데이터 프레임 생성
y <- data.frame(name = c("c", "b", "a"), weight = c(50, 70, 60))    # name 순서가 반대로 되어 있음
merge(x, y)    # 데이터 병합
cbind(x, y)


x <- c(20, 10, 30, 50, 40)
sort(x, decreasing = FALSE)    # 내림차순 정렬 아님(오름차순)
sort(x, decreasing = TRUE)    # 내림차순 정렬

x <- c(20, 10, 30, 50, 40)
order(x, decreasing = FALSE)    
order(x, decreasing = TRUE)    # 내림차순 정렬일 때 인덱스 순서

x <- c(1, 1, 2, 2, 3, 3)
unique(x)

x <- 1
y <- 2
rm(x, y)    # x,y 변수를 제거

aggregate(Petal.Length ~ Species, iris, mean)
aggregate(cbind(Petal.Length, Sepal.Length) ~ Species, iris, mean)

x <- unique(iris$Petal.Width)    # Petal.Width의 유일 값을 확인
sort(x)    # x값을 정렬해서 확인해 봄
tapply(iris$Petal.Length , iris$Petal.Width , mean)    # iris$Petal.Width를 그룹으로 iris$Petal.Length 평균구함

mapply(max, iris[, 1:4])

x <- c(1, 1, 1, 2, 2, 2)     # 숫자형으로 생성
x
class(x)                # 숫자형으로 출력됨

x <- as.character(x)    # 문자형으로 변환
x
class(x)                # 문자형으로 출력됨

x <- as.numeric(x)      # 숫자형으로 변환
x
class(x)                # 숫자형으로 출력됨

x <- as.factor(x)       # 팩터 구조로 변환
x
class(x)                # 팩터 구조로 출력

x <- as.data.frame(x)   # 데이터 프레임 구조로 변환 
x
class(x)                # 데이터 프레임 구조로 출력됨

x$x <- TRUE             # x열에 참(TRUE) 값을 할당
x
class(x)                # 여전히 데이터 프레임 구조로 출력

y <- as.logical(x$x)    # 논리형으로 변환
y
class(y)                # 논리형으로 출력됨

#---------------------------------------------------

# 6.6 데이터 계산하기

x <- c(1, 2, 3, 4, 5) / 4    # x를 4로 나눔
x

round(x, 0)    # 소수점 첫째자리에서 반올림
floor(x)    # 소수점 이하를 내림
trunc(x)    # 소수점 아래 값 버림
abs(-10)    # 절댓값
log(10, base = 2)    # 밑이 2인 로그
sqrt(10)    # 제곱근
exp(10)    # 지수로 변환

x <- c(1, 2, 3, 4, 5)
sum(x)    # 합계
mean(x)    # 평균
median(x)    # 중앙값
max(x)    # 최댓값
min(x)    # 최솟값
range(x)    # 범위
sd(x)    # 표준편차
var(x)    # 분산

#---------------------------------------------------

# 6.7 데이터 그리기

plot(iris$Petal.Length)

plot(iris$Petal.Length, iris$Petal.Width)

# 품종에 따른 색상 분류 추가
plot(iris$Petal.Length, iris$Petal.Width, main = "iris data", xlab = "Petal Length", ylab = "Petal Width", col = iris$Species)

pairs(~ Sepal.Width + Sepal.Length + Petal.Width + Petal.Length, data = iris, col = iris$Species)

hist(iris$Sepal.Width)

x <- aggregate(Petal.Length~Species, iris, mean)    # 품종별 꽃잎의 길이의 평균을 구함
barplot(x$Petal.Length, names = x$Species)    # 막대 그래프 이름으로 품종을 지정

x <- aggregate(Petal.Length~Species, iris, sum)    # 품종별로 꽃잎 넓이를 합산
pie(x$Petal.Length, labels = x$Species)    # 품종 이름을 붙여 파이 그래프 그림

x <- tapply(iris$Petal.Length, iris$Petal.Width, mean)    # iris$Petal.Width를 그룹으로 iris$Petal.Length 평균구함
x
plot(x, type = 'o')    # 선 그래프 옵션으로 그림


x <- 2
if (x == 2) {
        print("x is two")
    } else {
        print("x is not two")
        }

x <- c(1, 2, 3, 4, 5)
ifelse (x == 2, TRUE, FALSE)

for (i in 1:5) {    # 1부터 5까지 증가
    print(i)
}

sum <- 0
for (i in seq(1, 5, by = 1)) {    # seq함수는 순차 값을 생성하는 함수
    sum <- sum + i    
}
sum

i <- 1
while(i <= 5) {    # 5보다 작거나 같을 경우
    print(i)
    i <- i + 1
}

i <- 1
while (i <= 5) {
    i <- i + 1
    if (i == 2) {
        next    # i가 2이면 while문 처음으로 감
    }        
    print(i)
}

i <- 1
repeat {
    print(i)
    if (i >= 5) {
        break    # 5보다 크거나 같으면 멈춤
    }
    i <- i + 1
}
