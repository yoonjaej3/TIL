## grep 명령어


### 특정 파일에서 'error' 문자열 찾기
grep 'error' 파일명

### 여러개의 파일에서 'error' 문자열 찾기
grep 'error' 파일명1 파일명2

### 현재 디렉토리내에 있는 모든 파일에서 'error' 문자열 찾기
grep 'error' *

### 특정 확장자를 가진 모든 파일에서 'error' 문자열 찾기
grep 'error' *.log

### 실시간 로그 보기 (tail + grep)
tail -f mylog.log | grep 192.168.15.86

mylog파일을 실시간으로 액세스하고 IP주소가 192.168.49.16인 행만 추출

### 특정 파일에서 여러개 문자열 찾기
cat mylog.txt | grep 'Apple' | grep 'Banana'

mylog.txt 파일에서 Apple과 Banana이 있는 문자열들을 찾기

### grep -n 'Apple' mylog.txt > result.txt
grep -n 'Apple' mylog.txt > result.txt

mylog.txt 파일에서 Apple이 있는 문자열들을 result.txt 파일에 저장
