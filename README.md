# Map 활용하여 list 데이터 비교 처리 방법

1. map 데이터 비교<br>

함수<br>
|이름|설명|
|:---|:---:|---:|
|map.getOrDefault|찾는 키가 존재한다면 찾는 키의 값을 반환 아니면 기본 설정된 값을 반환|

ex) result.add(map.getOrDefault(element,getEmpty(element);
|이름|설명|
|getEmptyMap|사용자 설정 함수로 초기값으로 설정해 둔 함수<br>
->map 안에 들어있는 값과 element 라는 list의 값을 비교하여<br>
true 일 경우 element를 현재 맵의 값을 반환 <br>
false 일 경우 getEmptyMap 값을 반환 <br>



#이와 관련 코드 소스<br>
예시 변수<br>
|변수|값|설명|
|:---:|:---:|:---:|
|alpabet|['A','B','C','D','F']|고정 리스트|
|list|[{'A',1},{'C',1},{'F',1}]|조회해서 가져온 리스트|



비교 조건 : list 배열 안에 없는 alpabet의 변수를 초기값으로 지정하는 문제<br>
<br>
'''C

@초기값 함수
private Map getEmtpyMap(String element) {
         Map<String,String> resultmap = new HashMap<String,String>();
         resultmap.put("emdnm", element);
         resultmap.put("count","0");
         return resultmap;
}

@결과 전체 코드
Map<String,Map> map =new HashMap<String,Map>();
for(int i =0; i<list.size(); i++) {
    map.put(list.get(i).get("emdnm"),list.get(i));
}
for(String element : alpabet) {
    result.add(map.getOrDefault(element, getEmtpyMap(element)));
}
return result;
'''

+결과 
|list|[{'A',1},{'B',0},{'C',1},{'D',0},{'F',1}]<br>


<br>
+map 함수 이용 안할 경우 코드
'''C
  for(String element : areaList) {
            Map<String,String> resultmap = new HashMap<String,String>();
            if(list.size() > 0 && list != null) {
                for(int i = 0; i<list.size(); i++) {
                    if(element.equals((String)list.get(i).get("emdnm"))) {
                         resultmap.put("emdnm",(String)list.get(i).get("emdnm"));
                         resultmap.put("count",String.valueOf(list.get(i).get("count")));
                         resultmap.put("walistCnt",String.valueOf(list.get(i).get("walistCnt")));
                         resultmap.put("warate",String.valueOf(list.get(i).get("warate")));
                         map.add(resultmap);
                        // flag = true;
                         break;
                    }
                }
                if(!flag) {
                     resultmap.put("emdnm",element);
                     resultmap.put("count","0");
                     resultmap.put("walistCnt","0");
                     resultmap.put("warate","0");
                     map.add(resultmap);
                }
                flag = false;
            }
        }
'''
+결과<br>
출력 속도는 비슷하겠지만 유지보수 하는 입장에서는 코드가 길어지면 문제가 될 수 있다.
