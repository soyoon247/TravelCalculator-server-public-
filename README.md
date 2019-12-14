### **Travel Calculator**

![https://a.slack-edge.com/production-standard-emoji-assets/10.2/apple-medium/2708-fe0f@2x.png](https://a.slack-edge.com/production-standard-emoji-assets/10.2/apple-medium/2708-fe0f@2x.png)

여행 계산기 입니다.
유저가 여행지와 여행일정을 입력하면 여행 계산기는 실시간으로 취합한 자료를 기반으로 유저의 예상 여행 경비를 제공합니다.

### **Motivation**

"7박 8일 일정으로 런던 다녀오려면 얼마정도 들지?" 에 대한 객관적이고, 신속한 대답을 유저에게 제공하고 싶었습니다.

### **Data preparation**

여행 계산기가 제공하는 주요 정보는 항공권, 숙박, 식비 3 가지입니다.

항공권과 호텔 정보는 전세계 항공권과 호텔의 스케줄과 요금에 대한 데이터를 보유하고 있는 GDS 중 하나인 Amadeus 의 실시간 API 정보와 다양한 숙박시설의 요금을 비교하는 메타서치엔진인 트리바고에서 제공하는 도시별 hotel price index 를 취합하여 산정하고 있습니다.

식비는 NUMBEO restaurant price index를 사용해 도시별 ‘하루 식비 평균’으로 데이터를 준비했습니다.

## **back-side**

### **Caclulate 는 여행계산기의 메인 서비스 입니다.**


현재 총 15개 도시에 대한 경비 계산 서비스를 지원합니다.

여행하고자 하는 도시를 선택 후 출발일, 도착일을 입력하면 해당 일정의 항공권, 호텔 정보와 해당 도시의 평균 식비를 계산하여 총 예상 경비를 제공해드립니다.

견적 결과 페이지는 크게 두 개 항목으로 구성되어있습니다.

- '항공권 평균가격 + 호텔 평균가격 + 평균 식비 = 전체 경비' 의 한 줄로 요약되는 요약 견적
- 견적에 포함된 항공권, 호텔과 해당 도시의 주요 레스토랑 정보입니다.

![temp_1576063618161 -659236361](https://user-images.githubusercontent.com/49752614/70617861-e26f5880-1c54-11ea-99f0-bfe3753036b2.gif)
![temp_1576062282647 -660197056](https://user-images.githubusercontent.com/49752614/70616366-9a026b80-1c51-11ea-8f65-9dc55dd3bd86.gif)


요약 견적에 소개되는 경비의 산정 기준은 다음과 같습니다.

[항공권]

- 입력된 조건 (도시, 일정) 에 부합하는 최대 250 건의 실시간 항공 정보를 토대로 최저가 20건을 제외한 80 ~ 100 건의 평균 가격을 계산합니다.
- 만약 전체 항공 정보가 100건 이하라면 전체 항공권의 평균 가격을 계산합니다.
- 호출된 항공권 중 직항이 포함되어 있을 경우 직항의 평균 가격을 별도로 계산하여 제공해드립니다.

[호텔]

- 입력된 조건 (도시, 일정) 에 부합하는 도시 중심부 30 km 내에 위치한 실시간 호텔 정보를 토대로 평균 가격을 계산합니다.
- 만약 일치하는 호텔 조건이 없다면 해당 도시의 최근 5개월 3성급 호텔의 평균 가격을 견적에 포함하여 제공합니다.

[식비]

- 2019 하반기 기준 Numbeo 에서 발표한 도시별 평균 식비를 견적에 포함하여 제공합니다.

### **Trends**

![image](https://user-images.githubusercontent.com/49752614/70850471-fd98cd00-1ecd-11ea-9a6e-73e0f1290f93.png)


Trends 페이지는 여행계산기의 수집데이터를 바탕으로 관심사, 연령대, 성별을 입력하게 되면 다른 유저들이 가장 많이 방문하는 도시를 보여드립니다. 더하여 관심사와 밀접한 landmark, store, 관광지를 기반으로 wordcluoud를 보여드리고 있습니다.

### **User-page**


![mypage](https://user-images.githubusercontent.com/49752614/70615350-91a93100-1c4f-11ea-9404-d8464b191b71.gif)


여행계산기는 회원가입한 유저에게 마이페이지 기능을 제공하고 있습니다. 로그인한 유저가 calculate 로 여행 예상 견적을 내면, 유저는 마이페이지를 통해 이를 확인할 수 있습니다. 마이페이지에서는 유저의 기본 정보와 더불어 검색히스토리에서 검색한 도시, 요약 견적의 총 예상 경비, 출발일, 도착일 등을 보여드립니다.
