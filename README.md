# Golden_Time_Finding_The_Underprivileged

### [Data Science Term Project - Golden_Time_Finding_The_Underprivileged]
---
Github :
https://github.com/RyuKwanKon/Golden_Time_Finding_The_Underprivileged</br>
DataSet :  https://drive.google.com/uc?id=1ez0tNCX49Cxjzt6Ir4jkxy7Z9TnzOV60

Team member
* 201935039 류관곤

<details>
<summary>[Data curation And Load Dataset]</summary>
Low(sample) X Column(feature) = 35626 X 33<br/>

Target: [현장도착년월일, 현장도착시각] <br/>

Categorical feature
> 시군명, 출동소방서, 출동안전센터, 접수경로, 관할구분, 환자성별, 긴급구조시, 긴급구조구, 긴급구조동, 긴급구조리, 외국인여부, 국적, 구급처종명, 환자증상1, 환자증상2, 질병외_교통사고, 질병외_사고부상, 질병외_비외상성손상, 의식상태, 구급대원1_자격, 구급대원2_자격, 운전요원_자격
<br/>

Numerical feature
> 집계년도, 현장과의거리, 환자연령
<br/>

DateType feature
> 출동년월일, 출동시각, 현장도착년월일, 현장도착시각, 현장과의거리, 귀소년월일, 귀소시각
<br/>

Outlier Data
* It is judged that the outlier data is the abnormally large difference between the reporting time and the arrival time.
* It is judged that there was an exception to the data with an arrival time of more than 60 minutes.

> EX) Invalid input<br/>
* 현장도착시각       /    신고시각     /      Time of arrival<br/>
* 2022-02-14 18:28:00 / 2022-02-13 18:04:00 / 1464.0
* 2022-05-12 23:30:00 / 2022-05-11 23:18:00 / 1452.0

> EX)<br/>
* 현장도착시각       /    신고시각     /      Time of arrival<br/>
* 2022-01-26 08:55:00 / 2022-01-26 06:27:00 / 148.0
* 2022-02-09 10:46:00 / 2022-02-09 08:59:00 / 107.0

<br/>
Nan Data

*   현장도착년월일        6675
*   현장도착시각         6675
*   귀소년월일             1
*   귀소시각              1
*   환자연령           8719
*   환자성별           8508
*   국적            35004
*   구급처종명          4475
*   환자증상1         10838
*   환자증상2         20344
*   질병외_교통사고      33900
*   질병외_사고부상      30700
*   질병외_비외상성손상    34994
*   의식상태           9303
*   구급대원1_자격      17737
*   구급대원2_자격         94
*   운전요원_자격          16
  
</details>
---
<details>
<summary>[Data Preprocessing]</summary>
Handle Dirty Data
1.   현장도착년월일, 현장도착시각 --> Drop Sample <br/>
  Since the corresponding data feature corresponds to the target, a sample with an empty feature cannot be used. <br/>


2.   구급처종명, 접수경로 --> Fill "기타" <br/>
  For this data, Target replaced the value of "기타" that was treated as an exception in the existing data set.


3.   긴급구조구, 긴급구조동, 긴급구조리 --> Drop Sample <br/>
  The data feature is a feature that can have a high correlation with the target value.


4.   긴급구조시 --> Drop Column <br/>
  Since the data set is a Gyeonggi-do data set, the values of the corresponding features are all the same.


5.   집계년도 --> Drop column <br/>
  Since the data set is a 2022 data set, all data values for feature are the same.

6. Outlier Data --> Drop Sample
<br/><br/>

Feature Selection
*   drop_columns: [긴급구조시, 집계년도, 외국인여부, 환자연령, 환자성별, 국적, 구급대원1_자격, 구급대원2_자격, 운전요원_자격, 환자증상2, 질병외_교통사고, 질병외_사고부상, 질병외_비외상성손상, 귀소년월일, 귀소시각]
<br/><br/>

Feature Creation
*   출동년월일, 현장도착년월일 --> 출동시각-년, 출동시각-월, 출동시각-일, 현장도착시각-년, 현장도착시각-월, 현장도착시각-일
*   출동시각, 현장도착시각 --> 출동시각-시간, 출동시각-분, 현장도착시각-시간, 현장도착시각-분

</details>
---

<details>
<summary>[Data Preprocessing] - Random Forest</summary>
Feature selection

* categorical_columns [출동안전센터, 접수경로, 관할구분, 구급처종명, 긴급구조지역]
* date_columns [신고시각-월, 신고시각-일, 신고시각-시간, 신고시각-분, 출동시각-월, 출동시각-일, 출동시각-시간, 출동시각-분]
* float_columns [현장과의거리]
* target [현장도착시각-월, 현장도착시각-일, 현장도착시각-시간, 현장도착시각-분]

Encoding
*  One-Hot-Encoding
</details>
---

<details>
<summary>[Data Modeling and Evalution] - Random Forest</summary>
---

Model - Random Forest
* Used to predict arrival times for each region
<br/><br/>

Evaluation
* MSE
* MAE
* R^2 Score
<br/><br/>

Improve - Using GridSearch, parameter tuning
* n_estimators : 20 (limit of computational speed)
* max_depth : 12
* min_samples_leaf : 8
* min_samples_split : 8
<br/><br/>

Result
* MSE: 10.712984950240724 --> 1.3607359571304816
* MAE: 2.741359063662159 --> 0.938702478484288
* R^2 Score: 0.6489067220589864 --> 0.9475601394094079
</details>
---
