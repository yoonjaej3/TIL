# JSON


## JSON 배열 만들기

```
var jsonArray 	= new Array();
for (var i=0; i<3; i++) {
	var jsonObj		= new Object();
		
	jsonObj.id		= (i+1);
	jsonObj.content	= "테스트";
		
	jsonArray.push(JSON.parse(jsonObj));
}
```
- 자바스크립트 Array 를 생성해서 프로퍼티로 id, content를 생성한 뒤, JSON 라이브러리로 파싱하는 방법

![image](https://user-images.githubusercontent.com/57666307/179436076-19ace55e-e753-4aed-a018-825c1c5634ad.png)



## JSON 추가/삭제

```
//json object
var fruit= {name: "apple", count : 2, price: 3000};
console.log(">>>> fruit");
console.log(fruit);

//add data  (key, value)
console.log(">>>> add color");
fruit.color = 'red'
console.log(fruit);

//delete data
console.log(">>>> delete count");  
delete fruit.count;
console.log(fruit);
```
