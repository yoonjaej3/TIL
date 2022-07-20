## 자주쓰이는 RealGrid


### **컬럼 설정 시 입력길이 제한**(maxLength)

- **데이터에 소수점이 있는 경우**
    - **데이터 입력시 .도 length에 포함됨(해당 사항 고려해서 maxLength 설정)**

```flow
{
		name: "prchsAgrmnAmt", fieldName: "prchsAgrmnAmt", width: 100, header: { text: "매입약정총액", imgReqRed: true }, tag: 'req', visible: true, dataType: "number",
		styles: { "type": "number", "textAlignment": "far", "numberFormat": "#,##0"},
		editor: { "type": "number", "editFormat": "#,##0", "**maxLength**": 22 },
		footer: realFormat.sum2,
	},
```


### **소수점(ftype=”decimal”) 사용 시 필수 설정 항목**

- **digits (소수점 위 길이 설정)**
    - 예) **digits=”3”**
        - **123.12**
- **decimal-point(소수점 아래 길이 설정)**
    - 예) **decimal-point=”2”**
        - **123.12**

### **NaN 방지 (Not a Number)**

1. **decimal-point=”0”이면 oninput 참고 -  point(.) 생성 방지**

  2.  **decimal-point≠”0”이면(1이상) oninput 필수 아님**

```
<input type="text" bw-type="bw-input" bw-model="intrsRcptMnths" id="inp_intrsRcptMnths" ftype="decimal" decimal-point="3" maxlength="3" class="w30" digits="3"
				oninput="this.value = this.value.replace(/[^0-9.]/g,'').replace('.','')" />개월
```
