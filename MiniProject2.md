# 미니 프로젝트 2



> https://github.com/awesomedata/awesome-public-datasets

> > 미국의 공공 데이터를 집대성해놓은 곳.



이 중에서 하나 선택을 하고 각 컬럼을 파악하고 무슨 데이터를 뽑을 지 생각

맵리듀스로 뽑아내고 결과를 스쿱을 이용해서 mysql에 집어 넣는다.

파이썬에서 mysql데이터를 가져와서

판다스에서 그래프나 여러가지 기법을 활용해서 자료를 정리한다.

이 과정을 파워포인트로 세세하게 작성한다.

10페이지 이내로.

왜 이 데이터를 선택했는지 

찾아낸 정보는 무엇인지 

이 정보가 영향을 미치는 기업 또는 지역은 뭘까.

형식에 구애 받지 말라.



=====

뇌 사용량의 변화에 따른

미디어 매체의 증가 또는 변화

=====

미디어 쓰레기에 관한 문제.

우리가 매번 쓰고 지우는 데이터가 분명 쓰레기를 남길 것이라고 생각한다.

=====

전세계 총기사고 및 시위

https://github.com/jamesqo/gun-violence-data

먼저 어떤 나라에서 총기사고가 일어났는지 많이 일어난 나라는 어디이며 그 국가의 경제력은 어떠한가.
또는 많이 일어난 시기의 집권자는 누구였는가.

나라 / 일자 / 사망자와 부상자 / 의회 주변 구역

=====

1. hive 처리과정
   1. 테이블 처리 명령어
      1. https://knight76.tistory.com/entry/hive-ALTER-TABLE-%EC%98%88%EC%8B%9C
2. incident_id,date,state,city_or_county,address,n_killed,n_injured,incident_url,source_url,incident_url_fields_missing,congressional_district,gun_stolen,gun_type,incident_characteristics,latitude,location_description,longitude,notes,participant_age,participant_age_group,participant_gender,participant_name,participant_relationship,participant_status,participant_type,sources
3. incident_id float, `date` varchar(100), state varchar(100), city_or_county varchar(100), address varchar(100), n_killed float, n_injured float, incident_url varchar(100), source_url varchar(100), incident_url_fields_missing varchar(100), congressional_district float, gun_stolen varchar(100), gun_type varchar(100), incident_characteristics varchar(100), latitude float, location_description varchar(100), longitude float, notes varchar(100), participant_age varchar(100), participant_age_group varchar(100), participant_gender varchar(100), participant_name varchar(100), participant_relationship varchar(100), participant_status varchar(100), participant_type varchar(100), sources varchar(100)
4. mysql_col_del_house, senate
   1. incident_id float, `date` date, state varchar(100), city_or_county varchar(100), address varchar(100), n_killed float, n_injured float, incident_url varchar(100), source_url varchar(100), incident_url_fields_missing varchar(100), congressional_district float, gun_stolen varchar(100), gun_type varchar(100), incident_characteristics varchar(100), latitude float, location_description varchar(100), longitude float, notes varchar(100), participant_age varchar(100), participant_age_group varchar(100), participant_gender varchar(100), participant_name varchar(100), participant_relationship varchar(100), participant_status varchar(100), participant_type varchar(100), sources varchar(100)
5. all_col
   1. incident_id int, `date` date, state string, city_or_county string, address string, n_killed int, n_injured int, incident_url string, source_url string, incident_url_fields_missing boolean, congressional_district float, gun_stolen string, gun_type string, incident_characteristics string, latitude float, location_description string, longitude float, n_guns_involved float, notes string, participant_age string, participant_age_group string, participant_gender string, participant_name string, participant_relationship string, participant_status string, participant_type string, sources string, state_house_district float, state_senate_district float
6. del_col
   1. incident_id int, `date` date, state string, city_or_county string, address string, n_killed int, n_injured int, congressional_district float, gun_stolen string, gun_type string, incident_characteristics string, latitude float, location_description string, longitude float, n_guns_involved float, participant_age string, participant_age_group string, participant_gender string, participant_name string, participant_relationship string, participant_status string, participant_type string, state_house_district float, state_senate_district float
   2. del + notes
      1. incident_id int,  `date` date,  state string,  city_or_county string,  address string,  n_killed int,  n_injured int,  congressional_district float,  gun_stolen string,  gun_type string,  incident_characteristics string,  latitude float,  location_description string,  longitude float,  n_guns_involved float,  participant_age string,  participant_age_group string,  participant_gender string,  participant_name string,  participant_relationship string,  participant_status string,  participant_type string,  state_house_district float,  state_senate_district float
7. change_col_string -> varchar in hive
   1. incident_id int, `date` date, state varchar, city_or_county varchar, address varchar, n_killed int, n_injured int, incident_url varchar, source_url varchar, incident_url_fields_missing boolean, congressional_district float, gun_stolen varchar, gun_type varchar, incident_characteristics varchar, latitude float, location_description varchar, longitude float, n_guns_involved float, notes varchar, participant_age varchar, participant_age_group varchar, participant_gender varchar, participant_name varchar, participant_relationship varchar, participant_status varchar, participant_type varchar, sources varchar, state_house_district float, state_senate_district float
8. change_varchar(65355) in hive
   1. incident_id int, `date` date, state varchar(65355), city_or_county varchar(65355), address varchar(65355), n_killed int, n_injured int, incident_url varchar(65355), source_url varchar(65355), incident_url_fields_missing boolean, congressional_district float, gun_stolen varchar(65355), gun_type varchar(65355), incident_characteristics varchar(65355), latitude float, location_description varchar(65355), longitude float, n_guns_involved float, notes varchar(65355), participant_age varchar(65355), participant_age_group varchar(65355), participant_gender varchar(65355), participant_name varchar(65355), participant_relationship varchar(65355), participant_status varchar(65355), participant_type varchar(65355), sources varchar(65355), state_house_district float, state_senate_district float
9. del_col (mysql)
   1. incident_id int, `date` date, state varchar(65355), city_or_county varchar(65355), address varchar(65355), n_killed int, n_injured int, congressional_district float, gun_stolen varchar(65355), gun_type varchar(65355), incident_characteristics varchar(65355), latitude float, location_description varchar(65355), longitude float, n_guns_involved float, notes varchar(65355), participant_age varchar(65355), participant_age_group varchar(65355), participant_gender varchar(65355), participant_name varchar(65355), participant_relationship varchar(65355), participant_status varchar(65355), participant_type varchar(65355), state_house_district float, state_senate_district float
   2. del_col('incident_url', 'source_url','incident_url_fields_missing', 'sources', 'notes') + cutted date
      1. incident_id BIGINT, `date` date, state TEXT, city_or_county TEXT, address TEXT, n_killed BIGINT, n_injured BIGINT, congressional_district float, gun_stolen TEXT, gun_type TEXT, incident_characteristics TEXT, latitude float, location_description TEXT, longitude float, n_guns_involved float, participant_age TEXT, participant_age_group TEXT, participant_gender TEXT, participant_name TEXT, participant_relationship TEXT, participant_status TEXT, participant_type TEXT, state_house_district float, state_senate_district float
      2. incident_id string, `date` string, state string, city_or_county string, address string, n_killed string, n_injured string, congressional_district string, gun_stolen string, gun_type string, incident_characteristics string, latitude string, location_description string, longitude string, n_guns_involved string, participant_age string, participant_age_group string, participant_gender string, participant_name string, participant_relationship string, participant_status string, participant_type string, state_house_district string, state_senate_district string
      3. incident_id TEXT, date TEXT, state TEXT, city_or_county TEXT, address TEXT, n_killed TEXT, n_injured TEXT, congressional_district TEXT, gun_stolen TEXT, gun_type TEXT, incident_characteristics TEXT, latitude TEXT, location_description TEXT, longitude TEXT, n_guns_involved TEXT, participant_age TEXT, participant_age_group TEXT, participant_gender TEXT, participant_name TEXT, participant_relationship TEXT, participant_status TEXT, participant_type TEXT, state_house_district TEXT, state_senate_district TEXT



## 컬럼이 밀릴 때 (hive)

~~~sql
CREATE TABLE table_name(columns...) 
-> ROW FORMAT SERDE 
-> 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
~~~

###  # 이렇게 보내니까 데이터의 타입이 STRING으로 바뀌어있었다. 참고해야함.

###  # 아마 serde로 만들어서 그런거 같다

## 스쿱으로 보낼 때 

~~~sql
sqoop export --connect jdbc:mysql://localhost/billboard_db --table billboard --username hiveuser -P --columns [컬럼들] --export-dir /user/hive/warehouse/billboard_table --input-fields-terminated-by ',' --input-lines-terminated-by  '\n' --input-optionally-enclosed-by '\"' -m 1
~~~

- 옵션은 자신의 데이터에 맞게 유연하게 줄 것.

## mysql 테이블 관련

- 아무 옵션을 주지않고 컬럼헤더값만 주고 생성.
- 스쿱으로 주고 받을 때 항상 데이터 타입 확인 할 것.



## folium 참고 사이트

https://ichi.pro/ko/post/28980489868178

##### 씨푸드 식당 인터넷 기사

​	https://www.11alive.com/article/news/crime/he-was-murdered-and-his-wife-shot-outside-pappadeaux-the-killers-were-just-convicted-in-his-death/85-90741d49-a1d5-40f2-931a-a59d1934dc14



## mysql에서 꺼낼때

~~~python
from sqlalchemy import create_engine
import pandas as pd

!conda install --yes pymysql # Jupyter에 pymysql 설치하기 위해서 이 방법 사용 아나콘다 기준
import pymysql

# db_connection 경로 설정
db_connection_str = 'mysql+pymysql://mysql_user:password@mysql_host/db_name'

# create_engine을 사용하여 해당 경로로 연결하기
db_connection = create_engine(db_connection_str)

df = pd.read_sql('SELECT * FROM CUSTOMER LIMIT 10', con=db_connection)
df
~~~



