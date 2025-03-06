---
layout: single
title:  "250306 데이터 핸들링"
categories: PythonLeaning
tag: [python, blog, jekyll]
toc: true
author_profile: false
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


# **데이터 핸들링을 위한 Numpy와 Pandas**



  데이터를 불러올 때 쓰는 스킬에 대하여 배울 것임.  

  데이터를 직접 만드는 일은 별로 없기 때문에 데이터를 불러오는 기술이 지금은 중요함.  


## **파일 입출력**



### read_csv와 read_excel 함수

   엑셀로 생성된 데이터를 불러오는데 사용한다.    

   실제로 무엇을 쓸 것인지 보는 것이 좋음.  

   * 주요 인자 일람    

    **filepath**    

     기본값 없음  

     읽어올 파일의 경로 설정  

    **header**  

     헤더 인자를 이용해서 컬럼의 위치를 정의한다.  

     기본값: ‘infer’  

     기본값은 0이므로 따로 설정하지 않으면 맨 윗줄의 행이 헤더로 설정된다.  

     헤더가 없다면 None으로 설정.  

    **index_col**  

      기본값은 None, 0으로 시작하는 정수 인덱스. 인덱스로 설정할 컬럼 결정  

      정수 입력: 지정된 열의 번호를 인덱스로 설정 (첫 번째 열을 인덱스로 사용한다.)  

      문자열: 열 이름을 지정하여 해당 열을 인덱스로 설정할 수 있다.

    **usecols**  

      기본값: None  

      불러올 컬럼 목록 지정  

      정수 리스트 입력: 해당 리스트에 속한 위치에 속하는 열만 불러오기  

      문자열 리스트 입력: 읽을 열의 이름을 지정  

      (lambda) 함수 입력: 특정한 조건을 갖는 열을 불러오기  

    **encoding**  

      대표적인 한글 인코딩은 euc-kr과 cp949  

      기본: None  

      한글 깨지면 인코딩을 점검할 것  

    **sep**  

      기본: ","  

      구분자라고 보면 됨  

    **sheet_name**  

      불러올 시트의 위치 혹은 이름  

      기본값: 0 지정 안하면 맨앞의 데이터를 불러온다.  



### to_csv와 to_excel 함수  

  데이터프레임을 내보낼때 사용한다.



```python
import pandas as pd
import os
```


```python
#!pip install openpyxl ->재설치가 귀찮다면 이렇게 패키지를 설치할 수 있다.
```


```python
os.getcwd()
```

<pre>
'C:\\Users\\정민주'
</pre>

```python
os.listdir('데이터 공부')
```

<pre>
['.ipynb_checkpoints',
 '1주-1일 공부 노트.ipynb',
 '1주-1일 공부 노트2.ipynb',
 '1주-1일 공부 노트3.ipynb',
 '250305.ipynb',
 '5. Alexnet 구현하기.ipynb',
 'data11.txt',
 'example.txt',
 'House_Rent_Dataset.csv',
 'idol2.csv',
 'kpopidolsv3.csv',
 'starbucks_seoul.csv',
 'superstore_data.csv',
 'Titanic_dataset.xlsx',
 'train_and_test2.csv',
 'Untitled.ipynb',
 'Untitled1.ipynb',
 'user_data.pkl',
 '데이터내보내기.xlsx',
 '데이터내보내기_인덱스미포함.csv',
 '데이터내보내기_인덱스포함.csv',
 '서울시+공공자전거+실시간+대여정보.xls',
 '폴더2']
</pre>

```python
# 뒤에서 쓸 데이터셋 출처 : https://www.kaggle.com/datasets/nicolsalayoarias/all-kpop-idols/data
```


```python
# 기본 형태의 csv 데이터 불러오기
df = pd.read_csv('데이터 공부/kpopidolsv3.csv')
df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Stage Name</th>
      <th>Full Name</th>
      <th>Korean Name</th>
      <th>K Stage Name</th>
      <th>Date of Birth</th>
      <th>Group</th>
      <th>Debut</th>
      <th>Company</th>
      <th>Country</th>
      <th>Second Country</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Birthplace</th>
      <th>Other Group</th>
      <th>Former Group</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2Soul</td>
      <td>Kim Younghoon</td>
      <td>김영훈</td>
      <td>이솔</td>
      <td>10/09/1997</td>
      <td>7 O'clock</td>
      <td>26/08/2014</td>
      <td>Jungle</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>172.0</td>
      <td>55.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A.M</td>
      <td>Seong Hyunwoo</td>
      <td>성현우</td>
      <td>에이엠</td>
      <td>31/12/1996</td>
      <td>Limitless</td>
      <td>9/07/2019</td>
      <td>ONO</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>181.0</td>
      <td>62.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ace</td>
      <td>Jang Wooyoung</td>
      <td>장우영</td>
      <td>에이스</td>
      <td>28/08/1992</td>
      <td>VAV</td>
      <td>31/10/2015</td>
      <td>A team</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>177.0</td>
      <td>63.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aeji</td>
      <td>Kwon Aeji</td>
      <td>권애지</td>
      <td>애지</td>
      <td>25/10/1999</td>
      <td>Hash Tag</td>
      <td>11/10/2017</td>
      <td>LUK</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>163.0</td>
      <td>NaN</td>
      <td>Daegu</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>4</th>
      <td>AhIn</td>
      <td>Lee Ahin</td>
      <td>이아인</td>
      <td>아인</td>
      <td>27/09/1999</td>
      <td>MOMOLAND</td>
      <td>9/11/2016</td>
      <td>Double Kick</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>160.0</td>
      <td>44.0</td>
      <td>Wonju</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1773</th>
      <td>ZN</td>
      <td>Bae Jinye</td>
      <td>배진예</td>
      <td>지엔</td>
      <td>9/06/1994</td>
      <td>LABOUM</td>
      <td>27/08/2014</td>
      <td>NH</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>169.0</td>
      <td>48.0</td>
      <td>Bucheon</td>
      <td>UNI.T</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>1774</th>
      <td>Zoa</td>
      <td>Cho Hyewon</td>
      <td>조혜원</td>
      <td>조아</td>
      <td>31/05/2005</td>
      <td>Weeekly</td>
      <td>30/07/2020</td>
      <td>Play M</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>170.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>1775</th>
      <td>Zuho</td>
      <td>Bae Juho</td>
      <td>백주호</td>
      <td>주호</td>
      <td>4/07/1996</td>
      <td>SF9</td>
      <td>5/10/2016</td>
      <td>FNC</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1776</th>
      <td>Z-UK</td>
      <td>Jeong Jaewook</td>
      <td>정재욱</td>
      <td>지욱</td>
      <td>27/01/1993</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>174.0</td>
      <td>62.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bigflo</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1777</th>
      <td>Zuny</td>
      <td>Kim Joomi</td>
      <td>김주미</td>
      <td>주니</td>
      <td>8/12/1994</td>
      <td>Ladies' Code</td>
      <td>7/03/2013</td>
      <td>Polaris</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Gwangju</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
  </tbody>
</table>
<p>1778 rows × 16 columns</p>
</div>



```python
# 헤더 설정하기
```


```python
df = pd.read_csv('데이터 공부/kpopidolsv3.csv')
display(df.head()) # head: 첫 n(n=5) 행을 반환하는 메서드
display(df.columns)
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Stage Name</th>
      <th>Full Name</th>
      <th>Korean Name</th>
      <th>K Stage Name</th>
      <th>Date of Birth</th>
      <th>Group</th>
      <th>Debut</th>
      <th>Company</th>
      <th>Country</th>
      <th>Second Country</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Birthplace</th>
      <th>Other Group</th>
      <th>Former Group</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2Soul</td>
      <td>Kim Younghoon</td>
      <td>김영훈</td>
      <td>이솔</td>
      <td>10/09/1997</td>
      <td>7 O'clock</td>
      <td>26/08/2014</td>
      <td>Jungle</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>172.0</td>
      <td>55.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A.M</td>
      <td>Seong Hyunwoo</td>
      <td>성현우</td>
      <td>에이엠</td>
      <td>31/12/1996</td>
      <td>Limitless</td>
      <td>9/07/2019</td>
      <td>ONO</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>181.0</td>
      <td>62.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ace</td>
      <td>Jang Wooyoung</td>
      <td>장우영</td>
      <td>에이스</td>
      <td>28/08/1992</td>
      <td>VAV</td>
      <td>31/10/2015</td>
      <td>A team</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>177.0</td>
      <td>63.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aeji</td>
      <td>Kwon Aeji</td>
      <td>권애지</td>
      <td>애지</td>
      <td>25/10/1999</td>
      <td>Hash Tag</td>
      <td>11/10/2017</td>
      <td>LUK</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>163.0</td>
      <td>NaN</td>
      <td>Daegu</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>4</th>
      <td>AhIn</td>
      <td>Lee Ahin</td>
      <td>이아인</td>
      <td>아인</td>
      <td>27/09/1999</td>
      <td>MOMOLAND</td>
      <td>9/11/2016</td>
      <td>Double Kick</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>160.0</td>
      <td>44.0</td>
      <td>Wonju</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
  </tbody>
</table>
</div>


<pre>
Index(['Stage Name', 'Full Name', 'Korean Name', 'K Stage Name',
       'Date of Birth', 'Group', 'Debut', 'Company', 'Country',
       'Second Country', 'Height', 'Weight', 'Birthplace', 'Other Group',
       'Former Group', 'Gender'],
      dtype='object')
</pre>

```python
# 로그 데이터 처리
df = pd.read_csv('데이터 공부/kpopidolsv3.csv', header = None)
display(df.head())
display(df.columns)
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
      <th>13</th>
      <th>14</th>
      <th>15</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Stage Name</td>
      <td>Full Name</td>
      <td>Korean Name</td>
      <td>K Stage Name</td>
      <td>Date of Birth</td>
      <td>Group</td>
      <td>Debut</td>
      <td>Company</td>
      <td>Country</td>
      <td>Second Country</td>
      <td>Height</td>
      <td>Weight</td>
      <td>Birthplace</td>
      <td>Other Group</td>
      <td>Former Group</td>
      <td>Gender</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2Soul</td>
      <td>Kim Younghoon</td>
      <td>김영훈</td>
      <td>이솔</td>
      <td>10/09/1997</td>
      <td>7 O'clock</td>
      <td>26/08/2014</td>
      <td>Jungle</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>172</td>
      <td>55</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A.M</td>
      <td>Seong Hyunwoo</td>
      <td>성현우</td>
      <td>에이엠</td>
      <td>31/12/1996</td>
      <td>Limitless</td>
      <td>9/07/2019</td>
      <td>ONO</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>181</td>
      <td>62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ace</td>
      <td>Jang Wooyoung</td>
      <td>장우영</td>
      <td>에이스</td>
      <td>28/08/1992</td>
      <td>VAV</td>
      <td>31/10/2015</td>
      <td>A team</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>177</td>
      <td>63</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aeji</td>
      <td>Kwon Aeji</td>
      <td>권애지</td>
      <td>애지</td>
      <td>25/10/1999</td>
      <td>Hash Tag</td>
      <td>11/10/2017</td>
      <td>LUK</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>163</td>
      <td>NaN</td>
      <td>Daegu</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
  </tbody>
</table>
</div>


<pre>
Index([0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15], dtype='int64')
</pre>

```python
# index col 설정하기
# 일단 앞의 5개 결과 보여주기로 데이터 확인
df = pd.read_csv('데이터 공부/kpopidolsv3.csv')
display(df.head())
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Stage Name</th>
      <th>Full Name</th>
      <th>Korean Name</th>
      <th>K Stage Name</th>
      <th>Date of Birth</th>
      <th>Group</th>
      <th>Debut</th>
      <th>Company</th>
      <th>Country</th>
      <th>Second Country</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Birthplace</th>
      <th>Other Group</th>
      <th>Former Group</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2Soul</td>
      <td>Kim Younghoon</td>
      <td>김영훈</td>
      <td>이솔</td>
      <td>10/09/1997</td>
      <td>7 O'clock</td>
      <td>26/08/2014</td>
      <td>Jungle</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>172.0</td>
      <td>55.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A.M</td>
      <td>Seong Hyunwoo</td>
      <td>성현우</td>
      <td>에이엠</td>
      <td>31/12/1996</td>
      <td>Limitless</td>
      <td>9/07/2019</td>
      <td>ONO</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>181.0</td>
      <td>62.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ace</td>
      <td>Jang Wooyoung</td>
      <td>장우영</td>
      <td>에이스</td>
      <td>28/08/1992</td>
      <td>VAV</td>
      <td>31/10/2015</td>
      <td>A team</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>177.0</td>
      <td>63.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aeji</td>
      <td>Kwon Aeji</td>
      <td>권애지</td>
      <td>애지</td>
      <td>25/10/1999</td>
      <td>Hash Tag</td>
      <td>11/10/2017</td>
      <td>LUK</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>163.0</td>
      <td>NaN</td>
      <td>Daegu</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>4</th>
      <td>AhIn</td>
      <td>Lee Ahin</td>
      <td>이아인</td>
      <td>아인</td>
      <td>27/09/1999</td>
      <td>MOMOLAND</td>
      <td>9/11/2016</td>
      <td>Double Kick</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>160.0</td>
      <td>44.0</td>
      <td>Wonju</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 방법 1. set_index
df = df.set_index('Full Name')
display(df.head())
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Stage Name</th>
      <th>Korean Name</th>
      <th>K Stage Name</th>
      <th>Date of Birth</th>
      <th>Group</th>
      <th>Debut</th>
      <th>Company</th>
      <th>Country</th>
      <th>Second Country</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Birthplace</th>
      <th>Other Group</th>
      <th>Former Group</th>
      <th>Gender</th>
    </tr>
    <tr>
      <th>Full Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Kim Younghoon</th>
      <td>2Soul</td>
      <td>김영훈</td>
      <td>이솔</td>
      <td>10/09/1997</td>
      <td>7 O'clock</td>
      <td>26/08/2014</td>
      <td>Jungle</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>172.0</td>
      <td>55.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>Seong Hyunwoo</th>
      <td>A.M</td>
      <td>성현우</td>
      <td>에이엠</td>
      <td>31/12/1996</td>
      <td>Limitless</td>
      <td>9/07/2019</td>
      <td>ONO</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>181.0</td>
      <td>62.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>Jang Wooyoung</th>
      <td>Ace</td>
      <td>장우영</td>
      <td>에이스</td>
      <td>28/08/1992</td>
      <td>VAV</td>
      <td>31/10/2015</td>
      <td>A team</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>177.0</td>
      <td>63.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>Kwon Aeji</th>
      <td>Aeji</td>
      <td>권애지</td>
      <td>애지</td>
      <td>25/10/1999</td>
      <td>Hash Tag</td>
      <td>11/10/2017</td>
      <td>LUK</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>163.0</td>
      <td>NaN</td>
      <td>Daegu</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>Lee Ahin</th>
      <td>AhIn</td>
      <td>이아인</td>
      <td>아인</td>
      <td>27/09/1999</td>
      <td>MOMOLAND</td>
      <td>9/11/2016</td>
      <td>Double Kick</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>160.0</td>
      <td>44.0</td>
      <td>Wonju</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
  </tbody>
</table>
</div>



```python
df = pd.read_csv('데이터 공부/kpopidolsv3.csv', index_col = 0) # index_col = 'Full Name' 으로 설정하기
df.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Full Name</th>
      <th>Korean Name</th>
      <th>K Stage Name</th>
      <th>Date of Birth</th>
      <th>Group</th>
      <th>Debut</th>
      <th>Company</th>
      <th>Country</th>
      <th>Second Country</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Birthplace</th>
      <th>Other Group</th>
      <th>Former Group</th>
      <th>Gender</th>
    </tr>
    <tr>
      <th>Stage Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2Soul</th>
      <td>Kim Younghoon</td>
      <td>김영훈</td>
      <td>이솔</td>
      <td>10/09/1997</td>
      <td>7 O'clock</td>
      <td>26/08/2014</td>
      <td>Jungle</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>172.0</td>
      <td>55.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>A.M</th>
      <td>Seong Hyunwoo</td>
      <td>성현우</td>
      <td>에이엠</td>
      <td>31/12/1996</td>
      <td>Limitless</td>
      <td>9/07/2019</td>
      <td>ONO</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>181.0</td>
      <td>62.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>Ace</th>
      <td>Jang Wooyoung</td>
      <td>장우영</td>
      <td>에이스</td>
      <td>28/08/1992</td>
      <td>VAV</td>
      <td>31/10/2015</td>
      <td>A team</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>177.0</td>
      <td>63.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>Aeji</th>
      <td>Kwon Aeji</td>
      <td>권애지</td>
      <td>애지</td>
      <td>25/10/1999</td>
      <td>Hash Tag</td>
      <td>11/10/2017</td>
      <td>LUK</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>163.0</td>
      <td>NaN</td>
      <td>Daegu</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>AhIn</th>
      <td>Lee Ahin</td>
      <td>이아인</td>
      <td>아인</td>
      <td>27/09/1999</td>
      <td>MOMOLAND</td>
      <td>9/11/2016</td>
      <td>Double Kick</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>160.0</td>
      <td>44.0</td>
      <td>Wonju</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 특정 컬럼만 불러오기 
```


```python
df = pd.read_excel('데이터 공부/Titanic_dataset.xlsx')
df.columns
#컬럼 모두를 불러오게 됨
```

<pre>
Index(['pclass', 'survived', 'name', 'sex', 'age', 'sibsp', 'parch', 'ticket',
       'fare', 'cabin', 'embarked', 'boat', 'body', 'home.dest'],
      dtype='object')
</pre>

```python
df = pd.read_excel('데이터 공부/Titanic_dataset.xlsx', usecols = ['A1', 'A2', 'A3'])
df.columns
```


```python
# 사용한 데이터셋 출처 : https://www.kaggle.com/datasets/marouandaghmoumi/titanic-dataset
```


```python
df.columns
```

<pre>
Index(['pclass', 'survived', 'name', 'sex', 'age', 'sibsp', 'parch', 'ticket',
       'fare', 'cabin', 'embarked', 'boat', 'body', 'home.dest'],
      dtype='object')
</pre>

```python
df = pd.read_excel('데이터 공부/Titanic_dataset.xlsx', usecols = lambda x:'B' in x)
df.columns
```

<pre>
Index([], dtype='object')
</pre>

```python
df = pd.read_excel('데이터 공부/Titanic_dataset.xlsx')
df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pclass</th>
      <th>survived</th>
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>ticket</th>
      <th>fare</th>
      <th>cabin</th>
      <th>embarked</th>
      <th>boat</th>
      <th>body</th>
      <th>home.dest</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>Allen, Miss. Elisabeth Walton</td>
      <td>female</td>
      <td>29.0000</td>
      <td>0</td>
      <td>0</td>
      <td>24160</td>
      <td>211.3375</td>
      <td>B5</td>
      <td>S</td>
      <td>2</td>
      <td>NaN</td>
      <td>St Louis, MO</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>Allison, Master. Hudson Trevor</td>
      <td>male</td>
      <td>0.9167</td>
      <td>1</td>
      <td>2</td>
      <td>113781</td>
      <td>151.5500</td>
      <td>C22 C26</td>
      <td>S</td>
      <td>11</td>
      <td>NaN</td>
      <td>Montreal, PQ / Chesterville, ON</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>0</td>
      <td>Allison, Miss. Helen Loraine</td>
      <td>female</td>
      <td>2.0000</td>
      <td>1</td>
      <td>2</td>
      <td>113781</td>
      <td>151.5500</td>
      <td>C22 C26</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Montreal, PQ / Chesterville, ON</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>0</td>
      <td>Allison, Mr. Hudson Joshua Creighton</td>
      <td>male</td>
      <td>30.0000</td>
      <td>1</td>
      <td>2</td>
      <td>113781</td>
      <td>151.5500</td>
      <td>C22 C26</td>
      <td>S</td>
      <td>NaN</td>
      <td>135.0</td>
      <td>Montreal, PQ / Chesterville, ON</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>0</td>
      <td>Allison, Mrs. Hudson J C (Bessie Waldo Daniels)</td>
      <td>female</td>
      <td>25.0000</td>
      <td>1</td>
      <td>2</td>
      <td>113781</td>
      <td>151.5500</td>
      <td>C22 C26</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Montreal, PQ / Chesterville, ON</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1304</th>
      <td>3</td>
      <td>0</td>
      <td>Zabour, Miss. Hileni</td>
      <td>female</td>
      <td>14.5000</td>
      <td>1</td>
      <td>0</td>
      <td>2665</td>
      <td>14.4542</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>328.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1305</th>
      <td>3</td>
      <td>0</td>
      <td>Zabour, Miss. Thamine</td>
      <td>female</td>
      <td>NaN</td>
      <td>1</td>
      <td>0</td>
      <td>2665</td>
      <td>14.4542</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1306</th>
      <td>3</td>
      <td>0</td>
      <td>Zakarian, Mr. Mapriededer</td>
      <td>male</td>
      <td>26.5000</td>
      <td>0</td>
      <td>0</td>
      <td>2656</td>
      <td>7.2250</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>304.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1307</th>
      <td>3</td>
      <td>0</td>
      <td>Zakarian, Mr. Ortin</td>
      <td>male</td>
      <td>27.0000</td>
      <td>0</td>
      <td>0</td>
      <td>2670</td>
      <td>7.2250</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1308</th>
      <td>3</td>
      <td>0</td>
      <td>Zimmerman, Mr. Leo</td>
      <td>male</td>
      <td>29.0000</td>
      <td>0</td>
      <td>0</td>
      <td>315082</td>
      <td>7.8750</td>
      <td>NaN</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>1309 rows × 14 columns</p>
</div>



```python
df = pd.read_excel('데이터 공부/Titanic_dataset.xlsx', sheet_name = 'titanic3')
df

# 시트명을 입력하여 해당 시트의 데이터만 가져온다. 컬럼이 없거나 한 빈 시트는 가져와지지 않는 것 같다.
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pclass</th>
      <th>survived</th>
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>ticket</th>
      <th>fare</th>
      <th>cabin</th>
      <th>embarked</th>
      <th>boat</th>
      <th>body</th>
      <th>home.dest</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>Allen, Miss. Elisabeth Walton</td>
      <td>female</td>
      <td>29.0000</td>
      <td>0</td>
      <td>0</td>
      <td>24160</td>
      <td>211.3375</td>
      <td>B5</td>
      <td>S</td>
      <td>2</td>
      <td>NaN</td>
      <td>St Louis, MO</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>Allison, Master. Hudson Trevor</td>
      <td>male</td>
      <td>0.9167</td>
      <td>1</td>
      <td>2</td>
      <td>113781</td>
      <td>151.5500</td>
      <td>C22 C26</td>
      <td>S</td>
      <td>11</td>
      <td>NaN</td>
      <td>Montreal, PQ / Chesterville, ON</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>0</td>
      <td>Allison, Miss. Helen Loraine</td>
      <td>female</td>
      <td>2.0000</td>
      <td>1</td>
      <td>2</td>
      <td>113781</td>
      <td>151.5500</td>
      <td>C22 C26</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Montreal, PQ / Chesterville, ON</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>0</td>
      <td>Allison, Mr. Hudson Joshua Creighton</td>
      <td>male</td>
      <td>30.0000</td>
      <td>1</td>
      <td>2</td>
      <td>113781</td>
      <td>151.5500</td>
      <td>C22 C26</td>
      <td>S</td>
      <td>NaN</td>
      <td>135.0</td>
      <td>Montreal, PQ / Chesterville, ON</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>0</td>
      <td>Allison, Mrs. Hudson J C (Bessie Waldo Daniels)</td>
      <td>female</td>
      <td>25.0000</td>
      <td>1</td>
      <td>2</td>
      <td>113781</td>
      <td>151.5500</td>
      <td>C22 C26</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Montreal, PQ / Chesterville, ON</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1304</th>
      <td>3</td>
      <td>0</td>
      <td>Zabour, Miss. Hileni</td>
      <td>female</td>
      <td>14.5000</td>
      <td>1</td>
      <td>0</td>
      <td>2665</td>
      <td>14.4542</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>328.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1305</th>
      <td>3</td>
      <td>0</td>
      <td>Zabour, Miss. Thamine</td>
      <td>female</td>
      <td>NaN</td>
      <td>1</td>
      <td>0</td>
      <td>2665</td>
      <td>14.4542</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1306</th>
      <td>3</td>
      <td>0</td>
      <td>Zakarian, Mr. Mapriededer</td>
      <td>male</td>
      <td>26.5000</td>
      <td>0</td>
      <td>0</td>
      <td>2656</td>
      <td>7.2250</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>304.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1307</th>
      <td>3</td>
      <td>0</td>
      <td>Zakarian, Mr. Ortin</td>
      <td>male</td>
      <td>27.0000</td>
      <td>0</td>
      <td>0</td>
      <td>2670</td>
      <td>7.2250</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1308</th>
      <td>3</td>
      <td>0</td>
      <td>Zimmerman, Mr. Leo</td>
      <td>male</td>
      <td>29.0000</td>
      <td>0</td>
      <td>0</td>
      <td>315082</td>
      <td>7.8750</td>
      <td>NaN</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>1309 rows × 14 columns</p>
</div>



```python
# 데이터 내보내기

df = pd.DataFrame({"사원": ["A", "B", "C"],
                   "근로시간": [40, 45, 50]})
df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>사원</th>
      <th>근로시간</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>



```python
df.to_csv("데이터 공부/데이터내보내기_인덱스미포함.csv", encoding = "euc-kr", index = False)
df.to_csv("데이터 공부/데이터내보내기_인덱스포함.csv", encoding = "euc-kr", index = True)
df.to_excel("데이터 공부/데이터내보내기.xlsx", index = True)
```

<img src = 'https://media.discordapp.net/attachments/991299515866959925/1347116051485167646/2025-03-06_165744.png?ex=67caa716&is=67c95596&hm=6a11356b40dac03448b712b8785f2d3b77b38a9130cae1c3c181df1d502da379&=&format=webp&quality=lossless&width=615&height=513'>


## **여러 데이터 불러와서 합치기**

  ### 파일 불러와서 합치기

   1. 불러올 파일 경로로 구성된 리스트 생성하기

   2. 빈 데이터프레임 만들기

   3. 1에서 만든 리스트의 각 요소를 순회하면서 데이터를 불러오고 빈 데이터프레임과 병합하기


### concat() 

  두 개이상의 DataFrame을 병합할 때 사용한다.

 



```python
# 예제 데이터프레임 직접 생성. (기존 파일은 맞지도 않고, 자꾸 에러가 나서 직접 만들기로 했다.)
dfa = pd.DataFrame({"기존": ["A", "B", "C"],
                   "데이터": [40, 45, 50]})
dfa
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>기존</th>
      <th>데이터</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 예제 데이터프레임 직접 생성. (기존 파일은 맞지도 않고, 자꾸 에러가 나서 직접 만들기로 했다.)
dfb = pd.DataFrame({"기존1": ["A", "B", "C"],
                   "데이터1": [40, 45, 50]})
dfb
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>기존1</th>
      <th>데이터1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>



```python
dfa.to_csv("여러 데이터 불러오기/행병합예제_1.csv", encoding = "euc-kr", index = True)
dfb.to_csv("여러 데이터 불러오기/행병합예제_2.csv", encoding = "euc-kr", index = True)
```


```python
df1 = pd.read_csv("여러 데이터 불러오기/행병합예제_1.csv", encoding = "euc-kr")
df2 = pd.read_csv("여러 데이터 불러오기/행병합예제_2.csv", encoding = "euc-kr")

display(df1.head())
display(df2.head())
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>기존</th>
      <th>데이터</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>A</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>B</td>
      <td>45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>C</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>기존1</th>
      <th>데이터1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>A</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>B</td>
      <td>45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>C</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>



```python
pd.concat([df1, df2], axis = 0, ignore_index = True) 
# 가로축 기준으로 위아래에 달라붙음. 이전 인덱스를 무시하기에 0~6까지의 인덱스가 만들어졌다.
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>기존</th>
      <th>데이터</th>
      <th>기존1</th>
      <th>데이터1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>A</td>
      <td>40.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>B</td>
      <td>45.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>C</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>B</td>
      <td>45.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>C</td>
      <td>50.0</td>
    </tr>
  </tbody>
</table>
</div>



```python
pd.concat([df1, df2], axis = 0, ignore_index = False)
# 인덱스를 유지한다.
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>기존</th>
      <th>데이터</th>
      <th>기존1</th>
      <th>데이터1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>A</td>
      <td>40.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>B</td>
      <td>45.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>C</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>B</td>
      <td>45.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>C</td>
      <td>50.0</td>
    </tr>
  </tbody>
</table>
</div>



```python
dfa.to_csv("여러 데이터 불러오기/열병합예제_1.csv", encoding = "euc-kr", index = True)
dfb.to_csv("여러 데이터 불러오기/열병합예제_2.csv", encoding = "euc-kr", index = True)
```


```python
df3 = pd.read_csv("여러 데이터 불러오기/열병합예제_1.csv", encoding = "euc-kr")
df4 = pd.read_csv("여러 데이터 불러오기/열병합예제_2.csv", encoding = "euc-kr")

display(df3.head())
display(df4.head())
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>기존</th>
      <th>데이터</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>A</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>B</td>
      <td>45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>C</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>기존1</th>
      <th>데이터1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>A</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>B</td>
      <td>45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>C</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>



```python
pd.concat([df3, df4], axis = 1, ignore_index = True) # 열을 기준으로 양옆에 데이터가 붙는다.
# 기존 인덱스를 무시해서 1~5까지의 인덱스가 새로 붙었다.
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>A</td>
      <td>40</td>
      <td>0</td>
      <td>A</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>B</td>
      <td>45</td>
      <td>1</td>
      <td>B</td>
      <td>45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>C</td>
      <td>50</td>
      <td>2</td>
      <td>C</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>



```python
pd.concat([df3, df4], axis = 1, ignore_index = False)
# 기존 인덱스를 살린다.
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>기존</th>
      <th>데이터</th>
      <th>Unnamed: 0</th>
      <th>기존1</th>
      <th>데이터1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>A</td>
      <td>40</td>
      <td>0</td>
      <td>A</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>B</td>
      <td>45</td>
      <td>1</td>
      <td>B</td>
      <td>45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>C</td>
      <td>50</td>
      <td>2</td>
      <td>C</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>


## **loc와 lioc인덱서**

 loc와 iloc 인덱서는 특정 데이터를 인덱싱하거나 슬라이싱할 때 사용하는 메서드이다.  

 * loc 인덱서: 행과 열의 이름(명시적 인덱스)을 사용하여 데이터를 선택하며, 조건 기반의 필터링을 할

때도 사용

 * iloc 인덱서: 행과 열의 숫자 인덱스(암묵적 인덱스)를 사용하여 데이터를 선택한다.

 * loc 메서드는 슬라이싱에서마지막 인덱스를 포함하나, iloc 인덱서는 포함하지 않는다.



```python
data = {'Name': ['Alice', 'Bob', 'Charlie'],
        'Age': [25, 30, 35],
        'City': ['New York', 'Los Angeles', 'Chicago']}
df = pd.DataFrame(data, index=['a', 'b', 'c'])
df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>Alice</td>
      <td>25</td>
      <td>New York</td>
    </tr>
    <tr>
      <th>b</th>
      <td>Bob</td>
      <td>30</td>
      <td>Los Angeles</td>
    </tr>
    <tr>
      <th>c</th>
      <td>Charlie</td>
      <td>35</td>
      <td>Chicago</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 단일 행 선택 (라벨 기반) a 인덱스에 해당하는 행을 불러온다. 타입은 시리즈이다.
# 시리즈 여러 개가 데이터프레임을 이룸.
display(df.loc['a'])
```

<pre>
Name       Alice
Age           25
City    New York
Name: a, dtype: object
</pre>

```python
# 여러 행과 열 선택
display(df.loc[['a', 'b'], ['Name', 'City']])
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>Alice</td>
      <td>New York</td>
    </tr>
    <tr>
      <th>b</th>
      <td>Bob</td>
      <td>Los Angeles</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 슬라이싱
display(df.loc['Alice': 'Bob'])
# 인덱스가 아니어서 빈 데이터가 나옴.
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>



```python
# 조건 필터링
# df['Age']: Age라는 컬럼을 가져오겠다
display(df.loc[df['Age'] > 25, 'Name'])

# 다른 구문과 헷갈리지 않도록 주의. 이 구문 쓰는 걸 많이 틀렸었음.
```

<pre>
b        Bob
c    Charlie
Name: Name, dtype: object
</pre>

```python
# 단일 행 선택 (숫자 인덱스 기반)
print(df.iloc[0])

# 여러 행과 열 선택
print(df.iloc[0:2, 1:3])

# 특정 행과 열 선택
print(df.iloc[[0, 2], [0, 2]])
# [행, 행], [열, 열] 이렇게 선택한다. [첫번째 행, 세 번째 행], [첫 번째 컬럼, 두 번째 컬럼]
# cf. ndarray: arr[[0,2], [0,2]]
```

<pre>
Name       Alice
Age           25
City    New York
Name: a, dtype: object
   Age         City
a   25     New York
b   30  Los Angeles
      Name      City
a    Alice  New York
c  Charlie   Chicago
</pre>
## **행 및 열 선택과 제거**

 열을 선택할 때는 loc나 iloc를 꼭 사용하지 않아도 된다.  

 * df[‘열 이름’] # 시리즈를 반환  

 * df[[‘열 이름’]] # 데이터프레임을 반환  

 * df[[‘열 이름1’, ‘열 이름2’, ..]] # 데이터 프레임을 반환  



```python
df = pd.read_csv('데이터 공부/kpopidolsv3.csv')
df.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Stage Name</th>
      <th>Full Name</th>
      <th>Korean Name</th>
      <th>K Stage Name</th>
      <th>Date of Birth</th>
      <th>Group</th>
      <th>Debut</th>
      <th>Company</th>
      <th>Country</th>
      <th>Second Country</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Birthplace</th>
      <th>Other Group</th>
      <th>Former Group</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2Soul</td>
      <td>Kim Younghoon</td>
      <td>김영훈</td>
      <td>이솔</td>
      <td>10/09/1997</td>
      <td>7 O'clock</td>
      <td>26/08/2014</td>
      <td>Jungle</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>172.0</td>
      <td>55.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A.M</td>
      <td>Seong Hyunwoo</td>
      <td>성현우</td>
      <td>에이엠</td>
      <td>31/12/1996</td>
      <td>Limitless</td>
      <td>9/07/2019</td>
      <td>ONO</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>181.0</td>
      <td>62.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ace</td>
      <td>Jang Wooyoung</td>
      <td>장우영</td>
      <td>에이스</td>
      <td>28/08/1992</td>
      <td>VAV</td>
      <td>31/10/2015</td>
      <td>A team</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>177.0</td>
      <td>63.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aeji</td>
      <td>Kwon Aeji</td>
      <td>권애지</td>
      <td>애지</td>
      <td>25/10/1999</td>
      <td>Hash Tag</td>
      <td>11/10/2017</td>
      <td>LUK</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>163.0</td>
      <td>NaN</td>
      <td>Daegu</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>4</th>
      <td>AhIn</td>
      <td>Lee Ahin</td>
      <td>이아인</td>
      <td>아인</td>
      <td>27/09/1999</td>
      <td>MOMOLAND</td>
      <td>9/11/2016</td>
      <td>Double Kick</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>160.0</td>
      <td>44.0</td>
      <td>Wonju</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
  </tbody>
</table>
</div>



```python
df['Group'] #시리즈로 부름
```

<pre>
0          7 O'clock
1          Limitless
2                VAV
3           Hash Tag
4           MOMOLAND
            ...     
1773          LABOUM
1774         Weeekly
1775             SF9
1776             NaN
1777    Ladies' Code
Name: Group, Length: 1778, dtype: object
</pre>

```python
df[['Group']] #데이터프레임
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7 O'clock</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Limitless</td>
    </tr>
    <tr>
      <th>2</th>
      <td>VAV</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hash Tag</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MOMOLAND</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>1773</th>
      <td>LABOUM</td>
    </tr>
    <tr>
      <th>1774</th>
      <td>Weeekly</td>
    </tr>
    <tr>
      <th>1775</th>
      <td>SF9</td>
    </tr>
    <tr>
      <th>1776</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1777</th>
      <td>Ladies' Code</td>
    </tr>
  </tbody>
</table>
<p>1778 rows × 1 columns</p>
</div>



```python
display(df.drop('Group', axis = 1)) # return이 없다면 None이 나오게 된다.
display(df)

# df = df.drop('Name', axis = 1)
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Stage Name</th>
      <th>Full Name</th>
      <th>Korean Name</th>
      <th>K Stage Name</th>
      <th>Date of Birth</th>
      <th>Debut</th>
      <th>Company</th>
      <th>Country</th>
      <th>Second Country</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Birthplace</th>
      <th>Other Group</th>
      <th>Former Group</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2Soul</td>
      <td>Kim Younghoon</td>
      <td>김영훈</td>
      <td>이솔</td>
      <td>10/09/1997</td>
      <td>26/08/2014</td>
      <td>Jungle</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>172.0</td>
      <td>55.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A.M</td>
      <td>Seong Hyunwoo</td>
      <td>성현우</td>
      <td>에이엠</td>
      <td>31/12/1996</td>
      <td>9/07/2019</td>
      <td>ONO</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>181.0</td>
      <td>62.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ace</td>
      <td>Jang Wooyoung</td>
      <td>장우영</td>
      <td>에이스</td>
      <td>28/08/1992</td>
      <td>31/10/2015</td>
      <td>A team</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>177.0</td>
      <td>63.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aeji</td>
      <td>Kwon Aeji</td>
      <td>권애지</td>
      <td>애지</td>
      <td>25/10/1999</td>
      <td>11/10/2017</td>
      <td>LUK</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>163.0</td>
      <td>NaN</td>
      <td>Daegu</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>4</th>
      <td>AhIn</td>
      <td>Lee Ahin</td>
      <td>이아인</td>
      <td>아인</td>
      <td>27/09/1999</td>
      <td>9/11/2016</td>
      <td>Double Kick</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>160.0</td>
      <td>44.0</td>
      <td>Wonju</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1773</th>
      <td>ZN</td>
      <td>Bae Jinye</td>
      <td>배진예</td>
      <td>지엔</td>
      <td>9/06/1994</td>
      <td>27/08/2014</td>
      <td>NH</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>169.0</td>
      <td>48.0</td>
      <td>Bucheon</td>
      <td>UNI.T</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>1774</th>
      <td>Zoa</td>
      <td>Cho Hyewon</td>
      <td>조혜원</td>
      <td>조아</td>
      <td>31/05/2005</td>
      <td>30/07/2020</td>
      <td>Play M</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>170.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>1775</th>
      <td>Zuho</td>
      <td>Bae Juho</td>
      <td>백주호</td>
      <td>주호</td>
      <td>4/07/1996</td>
      <td>5/10/2016</td>
      <td>FNC</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1776</th>
      <td>Z-UK</td>
      <td>Jeong Jaewook</td>
      <td>정재욱</td>
      <td>지욱</td>
      <td>27/01/1993</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>174.0</td>
      <td>62.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bigflo</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1777</th>
      <td>Zuny</td>
      <td>Kim Joomi</td>
      <td>김주미</td>
      <td>주니</td>
      <td>8/12/1994</td>
      <td>7/03/2013</td>
      <td>Polaris</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Gwangju</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
  </tbody>
</table>
<p>1778 rows × 15 columns</p>
</div>


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Stage Name</th>
      <th>Full Name</th>
      <th>Korean Name</th>
      <th>K Stage Name</th>
      <th>Date of Birth</th>
      <th>Group</th>
      <th>Debut</th>
      <th>Company</th>
      <th>Country</th>
      <th>Second Country</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Birthplace</th>
      <th>Other Group</th>
      <th>Former Group</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2Soul</td>
      <td>Kim Younghoon</td>
      <td>김영훈</td>
      <td>이솔</td>
      <td>10/09/1997</td>
      <td>7 O'clock</td>
      <td>26/08/2014</td>
      <td>Jungle</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>172.0</td>
      <td>55.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A.M</td>
      <td>Seong Hyunwoo</td>
      <td>성현우</td>
      <td>에이엠</td>
      <td>31/12/1996</td>
      <td>Limitless</td>
      <td>9/07/2019</td>
      <td>ONO</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>181.0</td>
      <td>62.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ace</td>
      <td>Jang Wooyoung</td>
      <td>장우영</td>
      <td>에이스</td>
      <td>28/08/1992</td>
      <td>VAV</td>
      <td>31/10/2015</td>
      <td>A team</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>177.0</td>
      <td>63.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aeji</td>
      <td>Kwon Aeji</td>
      <td>권애지</td>
      <td>애지</td>
      <td>25/10/1999</td>
      <td>Hash Tag</td>
      <td>11/10/2017</td>
      <td>LUK</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>163.0</td>
      <td>NaN</td>
      <td>Daegu</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>4</th>
      <td>AhIn</td>
      <td>Lee Ahin</td>
      <td>이아인</td>
      <td>아인</td>
      <td>27/09/1999</td>
      <td>MOMOLAND</td>
      <td>9/11/2016</td>
      <td>Double Kick</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>160.0</td>
      <td>44.0</td>
      <td>Wonju</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1773</th>
      <td>ZN</td>
      <td>Bae Jinye</td>
      <td>배진예</td>
      <td>지엔</td>
      <td>9/06/1994</td>
      <td>LABOUM</td>
      <td>27/08/2014</td>
      <td>NH</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>169.0</td>
      <td>48.0</td>
      <td>Bucheon</td>
      <td>UNI.T</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>1774</th>
      <td>Zoa</td>
      <td>Cho Hyewon</td>
      <td>조혜원</td>
      <td>조아</td>
      <td>31/05/2005</td>
      <td>Weeekly</td>
      <td>30/07/2020</td>
      <td>Play M</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>170.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>1775</th>
      <td>Zuho</td>
      <td>Bae Juho</td>
      <td>백주호</td>
      <td>주호</td>
      <td>4/07/1996</td>
      <td>SF9</td>
      <td>5/10/2016</td>
      <td>FNC</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1776</th>
      <td>Z-UK</td>
      <td>Jeong Jaewook</td>
      <td>정재욱</td>
      <td>지욱</td>
      <td>27/01/1993</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>174.0</td>
      <td>62.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bigflo</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1777</th>
      <td>Zuny</td>
      <td>Kim Joomi</td>
      <td>김주미</td>
      <td>주니</td>
      <td>8/12/1994</td>
      <td>Ladies' Code</td>
      <td>7/03/2013</td>
      <td>Polaris</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Gwangju</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
  </tbody>
</table>
<p>1778 rows × 16 columns</p>
</div>



```python
df.drop([0,1,2,3], axis = 0)
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Stage Name</th>
      <th>Full Name</th>
      <th>Korean Name</th>
      <th>K Stage Name</th>
      <th>Date of Birth</th>
      <th>Group</th>
      <th>Debut</th>
      <th>Company</th>
      <th>Country</th>
      <th>Second Country</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Birthplace</th>
      <th>Other Group</th>
      <th>Former Group</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>AhIn</td>
      <td>Lee Ahin</td>
      <td>이아인</td>
      <td>아인</td>
      <td>27/09/1999</td>
      <td>MOMOLAND</td>
      <td>9/11/2016</td>
      <td>Double Kick</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>160.0</td>
      <td>44.0</td>
      <td>Wonju</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Ahra</td>
      <td>Go Ahra</td>
      <td>고아라</td>
      <td>아라</td>
      <td>21/02/2001</td>
      <td>Favorite</td>
      <td>5/07/2017</td>
      <td>Astory</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Yeosu</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Ahyeon</td>
      <td>Jung Ahyeon</td>
      <td>정아현</td>
      <td>아현</td>
      <td>11/04/2007</td>
      <td>BABYMONSTER</td>
      <td>0/01/1900</td>
      <td>YG</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Ahyoon</td>
      <td>Choi Subin</td>
      <td>최수빈</td>
      <td>아윤</td>
      <td>23/10/2004</td>
      <td>BOTOPASS</td>
      <td>26/08/2020</td>
      <td>WKS ENE</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Ahyoon</td>
      <td>Shin Ahyoon</td>
      <td>신아윤</td>
      <td>아윤</td>
      <td>24/09/2003</td>
      <td>Queenz Eye</td>
      <td>24/10/2022</td>
      <td>Big Mountain</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Seoul</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1773</th>
      <td>ZN</td>
      <td>Bae Jinye</td>
      <td>배진예</td>
      <td>지엔</td>
      <td>9/06/1994</td>
      <td>LABOUM</td>
      <td>27/08/2014</td>
      <td>NH</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>169.0</td>
      <td>48.0</td>
      <td>Bucheon</td>
      <td>UNI.T</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>1774</th>
      <td>Zoa</td>
      <td>Cho Hyewon</td>
      <td>조혜원</td>
      <td>조아</td>
      <td>31/05/2005</td>
      <td>Weeekly</td>
      <td>30/07/2020</td>
      <td>Play M</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>170.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
    <tr>
      <th>1775</th>
      <td>Zuho</td>
      <td>Bae Juho</td>
      <td>백주호</td>
      <td>주호</td>
      <td>4/07/1996</td>
      <td>SF9</td>
      <td>5/10/2016</td>
      <td>FNC</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1776</th>
      <td>Z-UK</td>
      <td>Jeong Jaewook</td>
      <td>정재욱</td>
      <td>지욱</td>
      <td>27/01/1993</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>174.0</td>
      <td>62.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bigflo</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1777</th>
      <td>Zuny</td>
      <td>Kim Joomi</td>
      <td>김주미</td>
      <td>주니</td>
      <td>8/12/1994</td>
      <td>Ladies' Code</td>
      <td>7/03/2013</td>
      <td>Polaris</td>
      <td>South Korea</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Gwangju</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>F</td>
    </tr>
  </tbody>
</table>
<p>1774 rows × 16 columns</p>
</div>


## **조건 연산을 이용한 필터링**



```python
df = pd.read_excel('데이터 공부/Titanic_dataset.xlsx')
df.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pclass</th>
      <th>survived</th>
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>ticket</th>
      <th>fare</th>
      <th>cabin</th>
      <th>embarked</th>
      <th>boat</th>
      <th>body</th>
      <th>home.dest</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>Allen, Miss. Elisabeth Walton</td>
      <td>female</td>
      <td>29.0000</td>
      <td>0</td>
      <td>0</td>
      <td>24160</td>
      <td>211.3375</td>
      <td>B5</td>
      <td>S</td>
      <td>2</td>
      <td>NaN</td>
      <td>St Louis, MO</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>Allison, Master. Hudson Trevor</td>
      <td>male</td>
      <td>0.9167</td>
      <td>1</td>
      <td>2</td>
      <td>113781</td>
      <td>151.5500</td>
      <td>C22 C26</td>
      <td>S</td>
      <td>11</td>
      <td>NaN</td>
      <td>Montreal, PQ / Chesterville, ON</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>0</td>
      <td>Allison, Miss. Helen Loraine</td>
      <td>female</td>
      <td>2.0000</td>
      <td>1</td>
      <td>2</td>
      <td>113781</td>
      <td>151.5500</td>
      <td>C22 C26</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Montreal, PQ / Chesterville, ON</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>0</td>
      <td>Allison, Mr. Hudson Joshua Creighton</td>
      <td>male</td>
      <td>30.0000</td>
      <td>1</td>
      <td>2</td>
      <td>113781</td>
      <td>151.5500</td>
      <td>C22 C26</td>
      <td>S</td>
      <td>NaN</td>
      <td>135.0</td>
      <td>Montreal, PQ / Chesterville, ON</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>0</td>
      <td>Allison, Mrs. Hudson J C (Bessie Waldo Daniels)</td>
      <td>female</td>
      <td>25.0000</td>
      <td>1</td>
      <td>2</td>
      <td>113781</td>
      <td>151.5500</td>
      <td>C22 C26</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Montreal, PQ / Chesterville, ON</td>
    </tr>
  </tbody>
</table>
</div>



```python
df['age'] > 20
```

<pre>
0        True
1       False
2       False
3        True
4        True
        ...  
1304    False
1305    False
1306     True
1307     True
1308     True
Name: age, Length: 1309, dtype: bool
</pre>

```python
df.loc[df['age'] > 40, ['name', 'age']]

#40세 초과인 사람들의 이름과 나이 컬럼을 같이 가져오겠다
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>Anderson, Mr. Harry</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Andrews, Miss. Kornelia Theodosia</td>
      <td>63.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Appleton, Mrs. Edward Dale (Charlotte Lamson)</td>
      <td>53.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Artagaveytia, Mr. Ramon</td>
      <td>71.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Astor, Col. John Jacob</td>
      <td>47.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1264</th>
      <td>van Billiard, Mr. Austin Blyler</td>
      <td>40.5</td>
    </tr>
    <tr>
      <th>1272</th>
      <td>Vander Cruyssen, Mr. Victor</td>
      <td>47.0</td>
    </tr>
    <tr>
      <th>1287</th>
      <td>Widegren, Mr. Carl/Charles Peter</td>
      <td>51.0</td>
    </tr>
    <tr>
      <th>1290</th>
      <td>Wilkes, Mrs. James (Ellen Needs)</td>
      <td>47.0</td>
    </tr>
    <tr>
      <th>1301</th>
      <td>Youseff, Mr. Gerious</td>
      <td>45.5</td>
    </tr>
  </tbody>
</table>
<p>227 rows × 2 columns</p>
</div>



```python
df['age'].between(10, 30)
#나이 10~30인 값이면 참이고 아니면 거짓으로 표기
```

<pre>
0        True
1       False
2       False
3        True
4        True
        ...  
1304     True
1305    False
1306     True
1307     True
1308     True
Name: age, Length: 1309, dtype: bool
</pre>

```python
df.loc[df['age'].between(10, 30)] 
#아까랑 똑같은데 데이터프레임으로, 해당하는 행을 다 가져온다.
# 10대에서 30대인 사람이 1309명중에 527명임을 알 수 있다.
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pclass</th>
      <th>survived</th>
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>ticket</th>
      <th>fare</th>
      <th>cabin</th>
      <th>embarked</th>
      <th>boat</th>
      <th>body</th>
      <th>home.dest</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>Allen, Miss. Elisabeth Walton</td>
      <td>female</td>
      <td>29.0</td>
      <td>0</td>
      <td>0</td>
      <td>24160</td>
      <td>211.3375</td>
      <td>B5</td>
      <td>S</td>
      <td>2</td>
      <td>NaN</td>
      <td>St Louis, MO</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>0</td>
      <td>Allison, Mr. Hudson Joshua Creighton</td>
      <td>male</td>
      <td>30.0</td>
      <td>1</td>
      <td>2</td>
      <td>113781</td>
      <td>151.5500</td>
      <td>C22 C26</td>
      <td>S</td>
      <td>NaN</td>
      <td>135.0</td>
      <td>Montreal, PQ / Chesterville, ON</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>0</td>
      <td>Allison, Mrs. Hudson J C (Bessie Waldo Daniels)</td>
      <td>female</td>
      <td>25.0</td>
      <td>1</td>
      <td>2</td>
      <td>113781</td>
      <td>151.5500</td>
      <td>C22 C26</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Montreal, PQ / Chesterville, ON</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1</td>
      <td>1</td>
      <td>Astor, Mrs. John Jacob (Madeleine Talmadge Force)</td>
      <td>female</td>
      <td>18.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17757</td>
      <td>227.5250</td>
      <td>C62 C64</td>
      <td>C</td>
      <td>4</td>
      <td>NaN</td>
      <td>New York, NY</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1</td>
      <td>1</td>
      <td>Aubart, Mme. Leontine Pauline</td>
      <td>female</td>
      <td>24.0</td>
      <td>0</td>
      <td>0</td>
      <td>PC 17477</td>
      <td>69.3000</td>
      <td>B35</td>
      <td>C</td>
      <td>9</td>
      <td>NaN</td>
      <td>Paris, France</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1300</th>
      <td>3</td>
      <td>1</td>
      <td>Yasbeck, Mrs. Antoni (Selini Alexander)</td>
      <td>female</td>
      <td>15.0</td>
      <td>1</td>
      <td>0</td>
      <td>2659</td>
      <td>14.4542</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1304</th>
      <td>3</td>
      <td>0</td>
      <td>Zabour, Miss. Hileni</td>
      <td>female</td>
      <td>14.5</td>
      <td>1</td>
      <td>0</td>
      <td>2665</td>
      <td>14.4542</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>328.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1306</th>
      <td>3</td>
      <td>0</td>
      <td>Zakarian, Mr. Mapriededer</td>
      <td>male</td>
      <td>26.5</td>
      <td>0</td>
      <td>0</td>
      <td>2656</td>
      <td>7.2250</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>304.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1307</th>
      <td>3</td>
      <td>0</td>
      <td>Zakarian, Mr. Ortin</td>
      <td>male</td>
      <td>27.0</td>
      <td>0</td>
      <td>0</td>
      <td>2670</td>
      <td>7.2250</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1308</th>
      <td>3</td>
      <td>0</td>
      <td>Zimmerman, Mr. Leo</td>
      <td>male</td>
      <td>29.0</td>
      <td>0</td>
      <td>0</td>
      <td>315082</td>
      <td>7.8750</td>
      <td>NaN</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>527 rows × 14 columns</p>
</div>



```python
df.loc[df['name'].isin(['Aubart, Mme. Leontine Pauline', 'Zakarian, Mr. Ortin'])]

# isin - 특정 컬럼 안에서 특정 값을 가진 행만 모으기. 
# 일부 일치하는 것이 아니라 완전 일치해야 해당 행을 가져올 수 있다.
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pclass</th>
      <th>survived</th>
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>ticket</th>
      <th>fare</th>
      <th>cabin</th>
      <th>embarked</th>
      <th>boat</th>
      <th>body</th>
      <th>home.dest</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>12</th>
      <td>1</td>
      <td>1</td>
      <td>Aubart, Mme. Leontine Pauline</td>
      <td>female</td>
      <td>24.0</td>
      <td>0</td>
      <td>0</td>
      <td>PC 17477</td>
      <td>69.300</td>
      <td>B35</td>
      <td>C</td>
      <td>9</td>
      <td>NaN</td>
      <td>Paris, France</td>
    </tr>
    <tr>
      <th>1307</th>
      <td>3</td>
      <td>0</td>
      <td>Zakarian, Mr. Ortin</td>
      <td>male</td>
      <td>27.0</td>
      <td>0</td>
      <td>0</td>
      <td>2670</td>
      <td>7.225</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



```python
df.loc[(df['age'].between(40, 50)) & (df['sex'].isin(['female']))]
#40에서 50세 사이의 여성만 불러오겠다
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pclass</th>
      <th>survived</th>
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>ticket</th>
      <th>fare</th>
      <th>cabin</th>
      <th>embarked</th>
      <th>boat</th>
      <th>body</th>
      <th>home.dest</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17</th>
      <td>1</td>
      <td>1</td>
      <td>Baxter, Mrs. James (Helene DeLaudeniere Chaput)</td>
      <td>female</td>
      <td>50.0</td>
      <td>0</td>
      <td>1</td>
      <td>PC 17558</td>
      <td>247.5208</td>
      <td>B58 B60</td>
      <td>C</td>
      <td>6</td>
      <td>NaN</td>
      <td>Montreal, PQ</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1</td>
      <td>1</td>
      <td>Beckwith, Mrs. Richard Leonard (Sallie Monypeny)</td>
      <td>female</td>
      <td>47.0</td>
      <td>1</td>
      <td>1</td>
      <td>11751</td>
      <td>52.5542</td>
      <td>D35</td>
      <td>S</td>
      <td>5</td>
      <td>NaN</td>
      <td>New York, NY</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1</td>
      <td>1</td>
      <td>Bidois, Miss. Rosalie</td>
      <td>female</td>
      <td>42.0</td>
      <td>0</td>
      <td>0</td>
      <td>PC 17757</td>
      <td>227.5250</td>
      <td>NaN</td>
      <td>C</td>
      <td>4</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>35</th>
      <td>1</td>
      <td>1</td>
      <td>Bowen, Miss. Grace Scott</td>
      <td>female</td>
      <td>45.0</td>
      <td>0</td>
      <td>0</td>
      <td>PC 17608</td>
      <td>262.3750</td>
      <td>NaN</td>
      <td>C</td>
      <td>4</td>
      <td>NaN</td>
      <td>Cooperstown, NY</td>
    </tr>
    <tr>
      <th>41</th>
      <td>1</td>
      <td>1</td>
      <td>Brown, Mrs. James Joseph (Margaret Tobin)</td>
      <td>female</td>
      <td>44.0</td>
      <td>0</td>
      <td>0</td>
      <td>PC 17610</td>
      <td>27.7208</td>
      <td>B4</td>
      <td>C</td>
      <td>6</td>
      <td>NaN</td>
      <td>Denver, CO</td>
    </tr>
    <tr>
      <th>44</th>
      <td>1</td>
      <td>1</td>
      <td>Burns, Miss. Elizabeth Margaret</td>
      <td>female</td>
      <td>41.0</td>
      <td>0</td>
      <td>0</td>
      <td>16966</td>
      <td>134.5000</td>
      <td>E40</td>
      <td>C</td>
      <td>3</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>63</th>
      <td>1</td>
      <td>1</td>
      <td>Chaffee, Mrs. Herbert Fuller (Carrie Constance...</td>
      <td>female</td>
      <td>47.0</td>
      <td>1</td>
      <td>0</td>
      <td>W.E.P. 5734</td>
      <td>61.1750</td>
      <td>E31</td>
      <td>S</td>
      <td>4</td>
      <td>NaN</td>
      <td>Amenia, ND</td>
    </tr>
    <tr>
      <th>98</th>
      <td>1</td>
      <td>1</td>
      <td>Douglas, Mrs. Walter Donald (Mahala Dutton)</td>
      <td>female</td>
      <td>48.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17761</td>
      <td>106.4250</td>
      <td>C86</td>
      <td>C</td>
      <td>2</td>
      <td>NaN</td>
      <td>Deephaven, MN / Cedar Rapids, IA</td>
    </tr>
    <tr>
      <th>99</th>
      <td>1</td>
      <td>1</td>
      <td>Duff Gordon, Lady. (Lucille Christiana Sutherl...</td>
      <td>female</td>
      <td>48.0</td>
      <td>1</td>
      <td>0</td>
      <td>11755</td>
      <td>39.6000</td>
      <td>A16</td>
      <td>C</td>
      <td>1</td>
      <td>NaN</td>
      <td>London / Paris</td>
    </tr>
    <tr>
      <th>124</th>
      <td>1</td>
      <td>1</td>
      <td>Frolicher-Stehli, Mrs. Maxmillian (Margaretha ...</td>
      <td>female</td>
      <td>48.0</td>
      <td>1</td>
      <td>1</td>
      <td>13567</td>
      <td>79.2000</td>
      <td>B41</td>
      <td>C</td>
      <td>5</td>
      <td>NaN</td>
      <td>Zurich, Switzerland</td>
    </tr>
    <tr>
      <th>131</th>
      <td>1</td>
      <td>1</td>
      <td>Gibson, Mrs. Leonard (Pauline C Boeson)</td>
      <td>female</td>
      <td>45.0</td>
      <td>0</td>
      <td>1</td>
      <td>112378</td>
      <td>59.4000</td>
      <td>NaN</td>
      <td>C</td>
      <td>7</td>
      <td>NaN</td>
      <td>New York, NY</td>
    </tr>
    <tr>
      <th>141</th>
      <td>1</td>
      <td>1</td>
      <td>Greenfield, Mrs. Leo David (Blanche Strouse)</td>
      <td>female</td>
      <td>45.0</td>
      <td>0</td>
      <td>1</td>
      <td>PC 17759</td>
      <td>63.3583</td>
      <td>D10 D12</td>
      <td>C</td>
      <td>7</td>
      <td>NaN</td>
      <td>New York, NY</td>
    </tr>
    <tr>
      <th>146</th>
      <td>1</td>
      <td>1</td>
      <td>Harper, Mrs. Henry Sleeper (Myna Haxtun)</td>
      <td>female</td>
      <td>49.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17572</td>
      <td>76.7292</td>
      <td>D33</td>
      <td>C</td>
      <td>3</td>
      <td>NaN</td>
      <td>New York, NY</td>
    </tr>
    <tr>
      <th>160</th>
      <td>1</td>
      <td>1</td>
      <td>Hippach, Mrs. Louis Albert (Ida Sophia Fischer)</td>
      <td>female</td>
      <td>44.0</td>
      <td>0</td>
      <td>1</td>
      <td>111361</td>
      <td>57.9792</td>
      <td>B18</td>
      <td>C</td>
      <td>4</td>
      <td>NaN</td>
      <td>Chicago, IL</td>
    </tr>
    <tr>
      <th>169</th>
      <td>1</td>
      <td>0</td>
      <td>Isham, Miss. Ann Elizabeth</td>
      <td>female</td>
      <td>50.0</td>
      <td>0</td>
      <td>0</td>
      <td>PC 17595</td>
      <td>28.7125</td>
      <td>C49</td>
      <td>C</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Paris, France New York, NY</td>
    </tr>
    <tr>
      <th>178</th>
      <td>1</td>
      <td>1</td>
      <td>Kimball, Mrs. Edwin Nelson Jr (Gertrude Parsons)</td>
      <td>female</td>
      <td>45.0</td>
      <td>1</td>
      <td>0</td>
      <td>11753</td>
      <td>52.5542</td>
      <td>D19</td>
      <td>S</td>
      <td>5</td>
      <td>NaN</td>
      <td>Boston, MA</td>
    </tr>
    <tr>
      <th>181</th>
      <td>1</td>
      <td>1</td>
      <td>Leader, Dr. Alice (Farnham)</td>
      <td>female</td>
      <td>49.0</td>
      <td>0</td>
      <td>0</td>
      <td>17465</td>
      <td>25.9292</td>
      <td>D17</td>
      <td>S</td>
      <td>8</td>
      <td>NaN</td>
      <td>New York, NY</td>
    </tr>
    <tr>
      <th>238</th>
      <td>1</td>
      <td>1</td>
      <td>Robert, Mrs. Edward Scott (Elisabeth Walton Mc...</td>
      <td>female</td>
      <td>43.0</td>
      <td>0</td>
      <td>1</td>
      <td>24160</td>
      <td>211.3375</td>
      <td>B3</td>
      <td>S</td>
      <td>2</td>
      <td>NaN</td>
      <td>St Louis, MO</td>
    </tr>
    <tr>
      <th>253</th>
      <td>1</td>
      <td>1</td>
      <td>Ryerson, Mrs. Arthur Larned (Emily Maria Borie)</td>
      <td>female</td>
      <td>48.0</td>
      <td>1</td>
      <td>3</td>
      <td>PC 17608</td>
      <td>262.3750</td>
      <td>B57 B59 B63 B66</td>
      <td>C</td>
      <td>4</td>
      <td>NaN</td>
      <td>Haverford, PA / Cooperstown, NY</td>
    </tr>
    <tr>
      <th>260</th>
      <td>1</td>
      <td>1</td>
      <td>Shutes, Miss. Elizabeth W</td>
      <td>female</td>
      <td>40.0</td>
      <td>0</td>
      <td>0</td>
      <td>PC 17582</td>
      <td>153.4625</td>
      <td>C125</td>
      <td>S</td>
      <td>3</td>
      <td>NaN</td>
      <td>New York, NY / Greenwich CT</td>
    </tr>
    <tr>
      <th>275</th>
      <td>1</td>
      <td>1</td>
      <td>Spedden, Mrs. Frederic Oakley (Margaretta Corn...</td>
      <td>female</td>
      <td>40.0</td>
      <td>1</td>
      <td>1</td>
      <td>16966</td>
      <td>134.5000</td>
      <td>E34</td>
      <td>C</td>
      <td>3</td>
      <td>NaN</td>
      <td>Tuxedo Park, NY</td>
    </tr>
    <tr>
      <th>281</th>
      <td>1</td>
      <td>1</td>
      <td>Stengel, Mrs. Charles Emil Henry (Annie May Mo...</td>
      <td>female</td>
      <td>43.0</td>
      <td>1</td>
      <td>0</td>
      <td>11778</td>
      <td>55.4417</td>
      <td>C116</td>
      <td>C</td>
      <td>5</td>
      <td>NaN</td>
      <td>Newark, NJ</td>
    </tr>
    <tr>
      <th>288</th>
      <td>1</td>
      <td>1</td>
      <td>Swift, Mrs. Frederick Joel (Margaret Welles Ba...</td>
      <td>female</td>
      <td>48.0</td>
      <td>0</td>
      <td>0</td>
      <td>17466</td>
      <td>25.9292</td>
      <td>D17</td>
      <td>S</td>
      <td>8</td>
      <td>NaN</td>
      <td>Brooklyn, NY</td>
    </tr>
    <tr>
      <th>311</th>
      <td>1</td>
      <td>1</td>
      <td>Wick, Mrs. George Dennick (Mary Hitchcock)</td>
      <td>female</td>
      <td>45.0</td>
      <td>1</td>
      <td>1</td>
      <td>36928</td>
      <td>164.8667</td>
      <td>NaN</td>
      <td>S</td>
      <td>8</td>
      <td>NaN</td>
      <td>Youngstown, OH</td>
    </tr>
    <tr>
      <th>314</th>
      <td>1</td>
      <td>1</td>
      <td>Widener, Mrs. George Dunton (Eleanor Elkins)</td>
      <td>female</td>
      <td>50.0</td>
      <td>1</td>
      <td>1</td>
      <td>113503</td>
      <td>211.5000</td>
      <td>C80</td>
      <td>C</td>
      <td>4</td>
      <td>NaN</td>
      <td>Elkins Park, PA</td>
    </tr>
    <tr>
      <th>352</th>
      <td>2</td>
      <td>1</td>
      <td>Brown, Mrs. Thomas William Solomon (Elizabeth ...</td>
      <td>female</td>
      <td>40.0</td>
      <td>1</td>
      <td>1</td>
      <td>29750</td>
      <td>39.0000</td>
      <td>NaN</td>
      <td>S</td>
      <td>14</td>
      <td>NaN</td>
      <td>Cape Town, South Africa / Seattle, WA</td>
    </tr>
    <tr>
      <th>358</th>
      <td>2</td>
      <td>1</td>
      <td>Bystrom, Mrs. (Karolina)</td>
      <td>female</td>
      <td>42.0</td>
      <td>0</td>
      <td>0</td>
      <td>236852</td>
      <td>13.0000</td>
      <td>NaN</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>New York, NY</td>
    </tr>
    <tr>
      <th>365</th>
      <td>2</td>
      <td>0</td>
      <td>Carter, Mrs. Ernest Courtenay (Lilian Hughes)</td>
      <td>female</td>
      <td>44.0</td>
      <td>1</td>
      <td>0</td>
      <td>244252</td>
      <td>26.0000</td>
      <td>NaN</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>London</td>
    </tr>
    <tr>
      <th>371</th>
      <td>2</td>
      <td>1</td>
      <td>Christy, Mrs. (Alice Frances)</td>
      <td>female</td>
      <td>45.0</td>
      <td>0</td>
      <td>2</td>
      <td>237789</td>
      <td>30.0000</td>
      <td>NaN</td>
      <td>S</td>
      <td>12</td>
      <td>NaN</td>
      <td>London</td>
    </tr>
    <tr>
      <th>387</th>
      <td>2</td>
      <td>1</td>
      <td>Davies, Mrs. John Morgan (Elizabeth Agnes Mary...</td>
      <td>female</td>
      <td>48.0</td>
      <td>0</td>
      <td>2</td>
      <td>C.A. 33112</td>
      <td>36.7500</td>
      <td>NaN</td>
      <td>S</td>
      <td>14</td>
      <td>NaN</td>
      <td>St Ives, Cornwall / Hancock, MI</td>
    </tr>
    <tr>
      <th>436</th>
      <td>2</td>
      <td>1</td>
      <td>Hart, Mrs. Benjamin (Esther Ada Bloomfield)</td>
      <td>female</td>
      <td>45.0</td>
      <td>1</td>
      <td>1</td>
      <td>F.C.C. 13529</td>
      <td>26.2500</td>
      <td>NaN</td>
      <td>S</td>
      <td>14</td>
      <td>NaN</td>
      <td>Ilford, Essex / Winnipeg, MB</td>
    </tr>
    <tr>
      <th>440</th>
      <td>2</td>
      <td>1</td>
      <td>Herman, Mrs. Samuel (Jane Laver)</td>
      <td>female</td>
      <td>48.0</td>
      <td>1</td>
      <td>2</td>
      <td>220845</td>
      <td>65.0000</td>
      <td>NaN</td>
      <td>S</td>
      <td>9</td>
      <td>NaN</td>
      <td>Somerset / Bernardsville, NJ</td>
    </tr>
    <tr>
      <th>471</th>
      <td>2</td>
      <td>1</td>
      <td>Kelly, Mrs. Florence "Fannie"</td>
      <td>female</td>
      <td>45.0</td>
      <td>0</td>
      <td>0</td>
      <td>223596</td>
      <td>13.5000</td>
      <td>NaN</td>
      <td>S</td>
      <td>9</td>
      <td>NaN</td>
      <td>London / New York, NY</td>
    </tr>
    <tr>
      <th>489</th>
      <td>2</td>
      <td>1</td>
      <td>Louch, Mrs. Charles Alexander (Alice Adelaide ...</td>
      <td>female</td>
      <td>42.0</td>
      <td>1</td>
      <td>0</td>
      <td>SC/AH 3085</td>
      <td>26.0000</td>
      <td>NaN</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Weston-Super-Mare, Somerset</td>
    </tr>
    <tr>
      <th>502</th>
      <td>2</td>
      <td>1</td>
      <td>Mellinger, Mrs. (Elizabeth Anne Maidment)</td>
      <td>female</td>
      <td>41.0</td>
      <td>0</td>
      <td>1</td>
      <td>250644</td>
      <td>19.5000</td>
      <td>NaN</td>
      <td>S</td>
      <td>14</td>
      <td>NaN</td>
      <td>England / Bennington, VT</td>
    </tr>
    <tr>
      <th>529</th>
      <td>2</td>
      <td>1</td>
      <td>Parrish, Mrs. (Lutie Davis)</td>
      <td>female</td>
      <td>50.0</td>
      <td>0</td>
      <td>1</td>
      <td>230433</td>
      <td>26.0000</td>
      <td>NaN</td>
      <td>S</td>
      <td>12</td>
      <td>NaN</td>
      <td>Woodford County, KY</td>
    </tr>
    <tr>
      <th>551</th>
      <td>2</td>
      <td>1</td>
      <td>Ridsdale, Miss. Lucy</td>
      <td>female</td>
      <td>50.0</td>
      <td>0</td>
      <td>0</td>
      <td>W./C. 14258</td>
      <td>10.5000</td>
      <td>NaN</td>
      <td>S</td>
      <td>13</td>
      <td>NaN</td>
      <td>London, England / Marietta, Ohio and Milwaukee...</td>
    </tr>
    <tr>
      <th>564</th>
      <td>2</td>
      <td>1</td>
      <td>Smith, Miss. Marion Elsie</td>
      <td>female</td>
      <td>40.0</td>
      <td>0</td>
      <td>0</td>
      <td>31418</td>
      <td>13.0000</td>
      <td>NaN</td>
      <td>S</td>
      <td>9</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>570</th>
      <td>2</td>
      <td>1</td>
      <td>Toomey, Miss. Ellen</td>
      <td>female</td>
      <td>50.0</td>
      <td>0</td>
      <td>0</td>
      <td>F.C.C. 13531</td>
      <td>10.5000</td>
      <td>NaN</td>
      <td>S</td>
      <td>9</td>
      <td>NaN</td>
      <td>Indianapolis, IN</td>
    </tr>
    <tr>
      <th>583</th>
      <td>2</td>
      <td>1</td>
      <td>Watt, Mrs. James (Elizabeth "Bessie" Inglis Mi...</td>
      <td>female</td>
      <td>40.0</td>
      <td>0</td>
      <td>0</td>
      <td>C.A. 33595</td>
      <td>15.7500</td>
      <td>NaN</td>
      <td>S</td>
      <td>9</td>
      <td>NaN</td>
      <td>Aberdeen / Portland, OR</td>
    </tr>
    <tr>
      <th>610</th>
      <td>3</td>
      <td>0</td>
      <td>Ahlin, Mrs. Johan (Johanna Persdotter Larsson)</td>
      <td>female</td>
      <td>40.0</td>
      <td>1</td>
      <td>0</td>
      <td>7546</td>
      <td>9.4750</td>
      <td>NaN</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Sweden Akeley, MN</td>
    </tr>
    <tr>
      <th>647</th>
      <td>3</td>
      <td>1</td>
      <td>Assaf Khalil, Mrs. Mariana ("Miriam")</td>
      <td>female</td>
      <td>45.0</td>
      <td>0</td>
      <td>0</td>
      <td>2696</td>
      <td>7.2250</td>
      <td>NaN</td>
      <td>C</td>
      <td>C</td>
      <td>NaN</td>
      <td>Ottawa, ON</td>
    </tr>
    <tr>
      <th>666</th>
      <td>3</td>
      <td>0</td>
      <td>Barbara, Mrs. (Catherine David)</td>
      <td>female</td>
      <td>45.0</td>
      <td>0</td>
      <td>1</td>
      <td>2691</td>
      <td>14.4542</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Syria Ottawa, ON</td>
    </tr>
    <tr>
      <th>811</th>
      <td>3</td>
      <td>0</td>
      <td>Ford, Mrs. Edward (Margaret Ann Watson)</td>
      <td>female</td>
      <td>48.0</td>
      <td>1</td>
      <td>3</td>
      <td>W./C. 6608</td>
      <td>34.3750</td>
      <td>NaN</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Rotherfield, Sussex, England Essex Co, MA</td>
    </tr>
    <tr>
      <th>832</th>
      <td>3</td>
      <td>0</td>
      <td>Goodwin, Mrs. Frederick (Augusta Tyler)</td>
      <td>female</td>
      <td>43.0</td>
      <td>1</td>
      <td>6</td>
      <td>CA 2144</td>
      <td>46.9000</td>
      <td>NaN</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Wiltshire, England Niagara Falls, NY</td>
    </tr>
    <tr>
      <th>851</th>
      <td>3</td>
      <td>1</td>
      <td>Hansen, Mrs. Claus Peter (Jennie L Howard)</td>
      <td>female</td>
      <td>45.0</td>
      <td>1</td>
      <td>0</td>
      <td>350026</td>
      <td>14.1083</td>
      <td>NaN</td>
      <td>S</td>
      <td>11</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>967</th>
      <td>3</td>
      <td>0</td>
      <td>Lindblom, Miss. Augusta Charlotta</td>
      <td>female</td>
      <td>45.0</td>
      <td>0</td>
      <td>0</td>
      <td>347073</td>
      <td>7.7500</td>
      <td>NaN</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1106</th>
      <td>3</td>
      <td>0</td>
      <td>Panula, Mrs. Juha (Maria Emilia Ojala)</td>
      <td>female</td>
      <td>41.0</td>
      <td>0</td>
      <td>5</td>
      <td>3101295</td>
      <td>39.6875</td>
      <td>NaN</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1153</th>
      <td>3</td>
      <td>0</td>
      <td>Robins, Mrs. Alexander A (Grace Charity Laury)</td>
      <td>female</td>
      <td>47.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5. 3337</td>
      <td>14.5000</td>
      <td>NaN</td>
      <td>S</td>
      <td>NaN</td>
      <td>7.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1158</th>
      <td>3</td>
      <td>0</td>
      <td>Rosblom, Mrs. Viktor (Helena Wilhelmina)</td>
      <td>female</td>
      <td>41.0</td>
      <td>0</td>
      <td>2</td>
      <td>370129</td>
      <td>20.2125</td>
      <td>NaN</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1211</th>
      <td>3</td>
      <td>0</td>
      <td>Skoog, Mrs. William (Anna Bernhardina Karlsson)</td>
      <td>female</td>
      <td>45.0</td>
      <td>1</td>
      <td>4</td>
      <td>347088</td>
      <td>27.9000</td>
      <td>NaN</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1290</th>
      <td>3</td>
      <td>1</td>
      <td>Wilkes, Mrs. James (Ellen Needs)</td>
      <td>female</td>
      <td>47.0</td>
      <td>1</td>
      <td>0</td>
      <td>363272</td>
      <td>7.0000</td>
      <td>NaN</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



```python
~(df['age'].between(0, 10)) # 0~10세가 아니면 True . ~: not 다.
```

<pre>
0        True
1       False
2       False
3        True
4        True
        ...  
1304     True
1305     True
1306     True
1307     True
1308     True
Name: age, Length: 1309, dtype: bool
</pre>

```python
df.loc[~(df['age'].between(0, 10))] #데이터프레임으로, 0~10세인 정보 빼고 보겠다.
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pclass</th>
      <th>survived</th>
      <th>name</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>ticket</th>
      <th>fare</th>
      <th>cabin</th>
      <th>embarked</th>
      <th>boat</th>
      <th>body</th>
      <th>home.dest</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>Allen, Miss. Elisabeth Walton</td>
      <td>female</td>
      <td>29.0</td>
      <td>0</td>
      <td>0</td>
      <td>24160</td>
      <td>211.3375</td>
      <td>B5</td>
      <td>S</td>
      <td>2</td>
      <td>NaN</td>
      <td>St Louis, MO</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>0</td>
      <td>Allison, Mr. Hudson Joshua Creighton</td>
      <td>male</td>
      <td>30.0</td>
      <td>1</td>
      <td>2</td>
      <td>113781</td>
      <td>151.5500</td>
      <td>C22 C26</td>
      <td>S</td>
      <td>NaN</td>
      <td>135.0</td>
      <td>Montreal, PQ / Chesterville, ON</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>0</td>
      <td>Allison, Mrs. Hudson J C (Bessie Waldo Daniels)</td>
      <td>female</td>
      <td>25.0</td>
      <td>1</td>
      <td>2</td>
      <td>113781</td>
      <td>151.5500</td>
      <td>C22 C26</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Montreal, PQ / Chesterville, ON</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>1</td>
      <td>Anderson, Mr. Harry</td>
      <td>male</td>
      <td>48.0</td>
      <td>0</td>
      <td>0</td>
      <td>19952</td>
      <td>26.5500</td>
      <td>E12</td>
      <td>S</td>
      <td>3</td>
      <td>NaN</td>
      <td>New York, NY</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1</td>
      <td>1</td>
      <td>Andrews, Miss. Kornelia Theodosia</td>
      <td>female</td>
      <td>63.0</td>
      <td>1</td>
      <td>0</td>
      <td>13502</td>
      <td>77.9583</td>
      <td>D7</td>
      <td>S</td>
      <td>10</td>
      <td>NaN</td>
      <td>Hudson, NY</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1304</th>
      <td>3</td>
      <td>0</td>
      <td>Zabour, Miss. Hileni</td>
      <td>female</td>
      <td>14.5</td>
      <td>1</td>
      <td>0</td>
      <td>2665</td>
      <td>14.4542</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>328.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1305</th>
      <td>3</td>
      <td>0</td>
      <td>Zabour, Miss. Thamine</td>
      <td>female</td>
      <td>NaN</td>
      <td>1</td>
      <td>0</td>
      <td>2665</td>
      <td>14.4542</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1306</th>
      <td>3</td>
      <td>0</td>
      <td>Zakarian, Mr. Mapriededer</td>
      <td>male</td>
      <td>26.5</td>
      <td>0</td>
      <td>0</td>
      <td>2656</td>
      <td>7.2250</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>304.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1307</th>
      <td>3</td>
      <td>0</td>
      <td>Zakarian, Mr. Ortin</td>
      <td>male</td>
      <td>27.0</td>
      <td>0</td>
      <td>0</td>
      <td>2670</td>
      <td>7.2250</td>
      <td>NaN</td>
      <td>C</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1308</th>
      <td>3</td>
      <td>0</td>
      <td>Zimmerman, Mr. Leo</td>
      <td>male</td>
      <td>29.0</td>
      <td>0</td>
      <td>0</td>
      <td>315082</td>
      <td>7.8750</td>
      <td>NaN</td>
      <td>S</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>1223 rows × 14 columns</p>
</div>



## **오늘의 종합 평가**
1. 슬라이싱, axis에 대한 이해가 부족하다. 물론 오늘 다시 배운거긴 하지만 그래도 너무 헷갈리고, 쳐다보기만 해도 막막하다. 주말에 문제를 계속 풀어야겠다.
   * 사실 axis = 0은 행이고 axis = 1은 열이라는 말도 맞긴 한데, 구글링해보니 행들의 연산은 결국 위아래 방향이라 세로고, 열들의 연산은 양옆으로 열이 추가되니 방향이 가로라고 한다.
   * 이는 데이터프레임을 축 기준으로 붙여보면 빠르게 이해할 수 있다. 그래서 조금 감이 왔는데, 아직도 헷갈리니 역시 문제를 더 들여다봐야겠다.
2. 역시 행렬에 대한 구조가 나에게는 어려운 것 같다. 텐서는 익숙한 개념인 RGB값이 나와서 괜찮았는데, 오히려 2차원에서 뭐 찾아내라고 하는게 어렵다.
3. loc iloc와 같은 기본적인 것들과 그것들과 같이 쓰는 함수, 클래스에서 쓰는 함수, 아닌 함수를 구분하여 문법을 공부해야겠다.
   * 예전에 같은 공부를 했을 때도 이게 헷갈려서 엉터리 코드를 적다가 데이터 필터링을 제대로 하지 못했다. 이번에는 그런 일이 없도록 해야겠다.
  
   
