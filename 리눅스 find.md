## find

### 경로
find의 인자값으로는 경로를 받습니다. 상대 경로, 절대 경로 모두 가능하며 대부분의 리눅스의 경우 이 경로 인자 값을 생략한다면 현재 위치(.)를 입력받은 것으로 간주하지만 
유닉스의 경우 이 경로를 입력받지 않으면 명령어 실행이 안되니 유의하셔야 합니다.


### 파일명으로 찾기
```
# 현재 디렉토리에서 test가 포함되는 파일 찾기
find . -name "*test*"

# 현재 디렉토리에서 .txt 확장자 모두 찾기
find . -name "*.txt"

# 현재 디렉토리에서 .txt 확장자 파일 검색 후 모두 삭제
find . -name "*.txt" -delete

# 현재 디렉토리에서 test로 시작되는 파일 찾기
find . -name "test*"

# 현재 디렉토리에서 test로 끝나는 파일 찾기
find . -name "*test"
```

### 타입으로 찾기 (-type)
```
# 현재 디렉토리에서 모든 디렉토리 찾기
find . -type d

# 현재 디렉토리에서 test가 들어가는 디렉토리 찾기
find . -name "*test*" -type d

# 현재 디렉토리에서 모든 파일 찾기
find . -type f
```

### 파일 크기로 찾기 (-empty, -size)

```
# 현재 디렉토리에서 빈 디렉토리이거나 크기가 0인 파일 검색
find . -empty

# 현재 디렉토리에서 test가 들어가는 빈 디렉토리이거나 크기가 0인 파일 검색하여 삭제
find . -name "*test*" -empty -delete

# 현재 디렉토리에서 1024byte인 파일 검색
find . -size 1024c

# 현재 디렉토리에서 1024byte보다 큰 파일 검색
find . -size +1024c

# 현재 디렉토리에서 1024byte보다 작은 파일 검색
find . -size -1024c

# 현재 디렉토리에서 1kb보다 크고 10kb보다 작은 파일 검색
```

### 검색된 파일에서 추가 명령 실행하기 (-exec)
```
# 현재 디렉토리에 "test"가 들어가는 파일을 찾아서 상세정보 출력
find . -name "*test*" -exec ls -l {} \;

# 현재 디렉토리에 있는 파일에서 "test"가 들어가는 내용 찾기 
find . -type f -exec grep "test" {} \;

# 현재 디렉토리에 ".txt" 확장자를 찾아서 모두 삭제
find . -name "*.txt" -exec rm {} \;
```
### 특정 디렉토리에 find 조건에 맞는 결과 값이 몇개 존재하는지
```
$ find ./ -type f | wc -l
4
```

### 확장자가 .jpg인 파일만 찾아서 바로 삭제

```
$ find ./ -name "*.jpg" -exec rm {} \;
$ ls
dir1/  dir2/  dir3/  dir4/  file1  file2  file3  file4
```

https://itholic.github.io/linux-basic-command/
