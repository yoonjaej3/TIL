##  DB Link

 한 데이터베이스에서 네트워크상의 다른 데이터베이스에 접속하기 위한 설정을 해주는 오라클 객체 입니다.
 
 DB Link 설정을 하면 한 DB에서 다른 DB의 내용을 볼 수있습니다.
 
 예를들어서 'A' DB에서 'B' DB로 DB Link 를 걸고자 한다면 우선 'A' DB의 TNSNAMES.ORA파일에 'B' DB 접속정보를 추가해 줍니다.
 
'A' DB 의 System 계정DPTJ

 GRANT CREATE PUBLIC DATABASE LINK, DROP PUBLIC DATABASE LINK TO A DB_ID;

 'A' DB에 권한을 주고, 아래와 같이 DB Link를 생성합니다.

CREATE DATABASE LINK TEST_LINK CONNECT TO B DB_ID IDENTIFIED BY PASSWORD USING 'B DB'

```
  TEST_LINK  -> Link 이름
  B DB_ID -> B DB 접속 아이디
  PASSWORD  -> B DB 접속 패스워드
 'B DB'  -> B DB 의 TNSNAMES.ORA에 등록된 Name
```

### DB Link 가 걸렸는지 확인

```
SELECT * FROM Table@TEST_LINK
```


### 모든 DB Link 를 확인하는 SQL
 ```
 SELECT * FROM all_db_links
 ```

### DB Link 삭제
```
DROP DATABASE LINK TEST_LINK
```


출처 : https://ldcc.tistory.com/73

