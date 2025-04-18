---
title: "2025-04-19 NPS (Net Promoter Score) 정리"
date: 2025-04-19
categories: [분석, 지표]
tags: [NPS, 고객추천지수, 데이터분석]
---


<head>
  <style>
    table.dataframe {
      white-space: normal;
      width: 100%;
      height: 240px;
      display: block;
      overflow: auto;
      font-family: Arial, sans-serif;
      font-size: 0.9rem;
      line-height: 20px;
      text-align: center;
      border: 0px !important;
    }

    table.dataframe th {
      text-align: center;
      font-weight: bold;
      padding: 8px;
    }

    table.dataframe td {
      text-align: center;
      padding: 8px;
    }

    table.dataframe tr:hover {
      background: #b8d1f3; 
    }

    .output_prompt {
      overflow: auto;
      font-size: 0.9rem;
      line-height: 1.45;
      border-radius: 0.3rem;
      -webkit-overflow-scrolling: touch;
      padding: 0.8rem;
      margin-top: 0;
      margin-bottom: 15px;
      font: 1rem Consolas, "Liberation Mono", Menlo, Courier, monospace;
      color: $code-text-color;
      border: solid 1px $border-color;
      border-radius: 0.3rem;
      word-break: normal;
      white-space: pre;
    }

  .dataframe tbody tr th:only-of-type {
      vertical-align: middle;
  }

  .dataframe tbody tr th {
      vertical-align: top;
  }

  .dataframe thead th {
      text-align: center !important;
      padding: 8px;
  }

  .page__content p {
      margin: 0 0 0px !important;
  }

  .page__content p > strong {
    font-size: 0.8rem !important;
  }

  </style>
</head>




# NPS (Net Promoter Score) = 순고객추천지수

* 고객이 우리 서비스를 다른 사람에게 추천할 의향이 있는지를 나타낸다.
* 기존의 고객 만족 점수가 실제 고객 행동과 차이가 있다는 분석 결과에 기반하여 도입된 새로운 지수이다.



## NPS 고객 분류 기준

* **비추천 고객 (Detractors)**  
  - 점수: 1~6점 (10점 만점 기준)  
  - 재구매 의향이 낮고, 주변에 부정적인 소문을 낼 가능성이 있는 고객

* **중립 고객 (Passives)**  
  - 점수: 7~8점  
  - 특별한 불만은 없지만 적극적으로 추천하지도 않는 중립적인 고객

* **추천 고객 (Promoters)**  
  - 점수: 9~10점  
  - 서비스를 다른 사람에게 기꺼이 추천할 의향이 있는 충성도 높은 고객



### NPS 계산 방법

> **NPS = 추천 고객 비율(%) - 비추천 고객 비율(%)**



## NPS 점수 척도 변경 사례

여러 실험을 통해 점수의 척도 기준이 변경되었으며, 아래와 같이 다양한 형태로 나타나기도 한다.

* 첫 번째 예시:  
![NPS 예시1](https://cdn.discordapp.com/attachments/1351886685637578783/1362845153395740835/2025-04-19_023950.png?ex=6803dff5&is=68028e75&hm=f049c1cdcfe6760a3763b6c003bdd43eab57d3e2110220589e4375f247bee366&)

* 두 번째 예시:  
(노랑: Detractors, 회색: Passive, 초록: Promoters)  
![NPS 예시2](https://cdn.discordapp.com/attachments/1351886685637578783/1362846225334009966/2025-04-19_024408.png?ex=6803e0f4&is=68028f74&hm=7cbe628c5d6550ceaa61459736216aa06d56369d27c86b93819706dd65395299&)

* 세 번째 예시:  
(빨강: Detractors, 노랑: Passive, 연한초록~초록: Promoters — 추천 고객 내에서도 세부 단계 존재)



## NPS 해석 시 주의사항

* **국가, 산업, 도메인**에 따라 평균값이 다를 수 있음에 주의하여야 한다.  
* 자사의 지수만 보는 것보다, **동종 업계와 타사의 지수와 비교**하는 것이 더 중요하다.  



  

> 📌 본 내용은 **제로베이스 스쿨**의 자료를 참고하여 작성되었습니다.  




---






