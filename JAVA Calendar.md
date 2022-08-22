### 자바에서 현재 날짜시간 구하기

기준 : 현재 날짜시간

=> 20201008160222 (2020년 10월 08일 16시 02분 22초)

```
  try {
        SimpleDateFormat sdf = new SimpleDateFormat(“yyyyMMddHHmmss”);



        // 현재 날짜시간 구하기
        Calendar cal = Calendar.getInstance();

       

        // 출력
        String resultDate = sdf.format(cal.getTime());

        
        String year = resultDate.substring(0, 4);
        String month = resultDate.substring(4, 6);
        String day = resultDate.substring(6, 8);
        String hour = resultDate.substring(8, 10);
        String minute = resultDate.substring(10, 12);
        String second = resultDate.substring(12, 14);

       

        System.out.println(resultDate + ” (” + year + “년 ” + month + “월 ” + day + “일 “
        + hour + “시 ” + minute + “분 ” + second + “초)”);

        
    } catch (Exception e) {
        e.printStackTrace();
    }
    
 ```

### 자바에서 특정일의 날짜시간 구하기

기준 : 20200101092030 (2020년 01월 01일 09시 20분 30초)

=> 20200101092030 (2020년 01월 01일 09시 20분 30초)

```
   try {
        SimpleDateFormat sdf = new SimpleDateFormat(“yyyyMMddHHmmss”);
       
        // 특정일의 날짜시간 구하기
        // 2020년 01월 01일 09시 20분 30초
        String strDate = “20200101092030”;
        Date date = sdf.parse(strDate);

        Calendar cal = Calendar.getInstance();
        cal.setTime(date);
        

        // 출력
        String resultDate = sdf.format(cal.getTime());

        String year = resultDate.substring(0, 4);
        String month = resultDate.substring(4, 6);
        String day = resultDate.substring(6, 8);
        String hour = resultDate.substring(8, 10);
        String minute = resultDate.substring(10, 12);
        String second = resultDate.substring(12, 14);


        System.out.println(resultDate + ” (” + year + “년 ” + month + “월 ” + day + “일 “
        + hour + “시 ” + minute + “분 ” + second + “초)”);

    } catch (Exception e) {
        e.printStackTrace();
    }

```


### 자바에서 특정일 다음날(1일 후) 날짜시간 구하기

기준 : 20200101092030 (2020년 01월 01일 09시 20분 30초)

=> 20200102092030 (2020년 01월 02일 09시 20분 30초)
```

    try {
        SimpleDateFormat sdf = new SimpleDateFormat(“yyyyMMddHHmmss”);
       
        // 특정일 다음날(1일 후) 날짜시간 구하기
        // 2020년 01월 01일 09시 20분 30초의 다음날(1일 후)
        String strDate = “20200101092030”;
        Date date = sdf.parse(strDate);


        Calendar cal = Calendar.getInstance();
        cal.setTime(date);
       
        cal.add(Calendar.DATE, 1); // 다음날(1일 후)

        // 출력
        String resultDate = sdf.format(cal.getTime());

        String year = resultDate.substring(0, 4);
        String month = resultDate.substring(4, 6);
        String day = resultDate.substring(6, 8);
        String hour = resultDate.substring(8, 10);
        String minute = resultDate.substring(10, 12);
        String second = resultDate.substring(12, 14);


        System.out.println(resultDate + ” (” + year + “년 ” + month + “월 ” + day + “일 “
        + hour + “시 ” + minute + “분 ” + second + “초)”);

    } catch (Exception e) {
        e.printStackTrace();
    }
```

```

기준 : 20200101092030 (2020년 01월 01일 09시 20분 30초)

이전날(1일 전, 어제) : cal.add(Calendar.DATE, -1);

=> 20191231092030 (2019년 12월 31일 09시 20분 30초)

다음날(1일 후, 내일) : cal.add(Calendar.DATE, 1);

=> 20200102092030 (2020년 01월 02일 09시 20분 30초)

이전달(지난달) : cal.add(Calendar.MONTH, -1);

=> 20191201092030 (2019년 12월 01일 09시 20분 30초)

다음달(내달) : cal.add(Calendar.MONTH, 1);

=> 20200201092030 (2020년 02월 01일 09시 20분 30초)

이전연도(작년) : cal.add(Calendar.YEAR, -1);

=> 20190101092030 (2019년 01월 01일 09시 20분 30초)

다음연도(내년) : cal.add(Calendar.YEAR, 1);

=> 20210101092030 (2021년 01월 01일 09시 20분 30초)

```

출처 : http://it-archives.com/222110304107/
