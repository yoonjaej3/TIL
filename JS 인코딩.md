## 문자열 인코딩 함수


### 문자 인코딩 함수 : escape() encodeURI() encodeURIComponent()   

- __escape(string)__ : ASCII(아스키) 문자를  유니코드 형식으로 변환  , 1바이트는 %XX 2바이트는 %uXXXX형태로 변환 

- __unescape(string)__ : 유니코드문자를 디코딩 encodeURI(string) : 주어진 문자열을 URI로 특수문자( :  ; / = ? & 등의 특수문자) 제외 encoding 한다. 

- __decodeURI(string)__ : 주어진 문자열에서 encoding 된 URI를 decoding 한다. 

- __encodeURIComponent(string)__ : 주어진 문자열을 URI로 모든 문자( :  ; / = ? & 등의 특수문자)를 encoding 한다. 

- __decodeURIComponent(string)__ : 주어진 문자열에서 encoding 된 URI를 decoding 한다
