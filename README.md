# Golden_Time_Finding_The_Underprivileged

---

DataSet :  https://drive.google.com/uc?id=1ez0tNCX49Cxjzt6Ir4jkxy7Z9TnzOV60

Team member
* 201935039 Ryu KwanKon
* 201935013 Kim Daehun
* 201935028 Kim Jongmin

[Architecture]

---

<img width="800" alt="스크린샷 2023-06-10 오전 4 17 55" src="https://github.com/RyuKwanKon/Golden_Time_Finding_The_Underprivileged/assets/97783148/437d49bb-6252-475d-91a8-54b7b94fb8f3">

<details>
<summary>[Project Objective]</summary>
<br/><br/>
To find the marginalized area within the golden time and propose the fact through a government agency or contest.<br/>
Golden Time is directly related to human life, and in Korea, there is no data in specific regions for this fact, so I thought it was a meaningful topic.

</details>

---

<details>
<summary>[Data curation And Load Dataset]</summary>
<br/>
<br/>
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
<br/>
<br/>
 
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
<br/>

Reason for selection

* Random Forest is an algorithm that creates a number of decision trees and gives the final answer by ensemble and majority voting.
* Processing various data types: Random Forest can handle both categorical and continuous features.
* High predictive performance: Random Forest performs predictions by combining various decision trees, which typically provides higher predictive performance than other algorithms.

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
<br/><br/>
  
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

<details>
<summary>[Data Preprocessing] - KMeans Clustering</summary>
<br/><br/>
  
Reason for selection

* This is because there is no risk level of emergency action in the dataset, which is the target we want to guess.
* We will cluster using the association according to the arrival time of the site and the risk of the event, and use the estimated label as the level of first aid risk in the area.
* Simplest partitioning method for clustering analysis and widely used in data mining  applications.
<br/>  
  
Feature Selection

의식상태, 환자증상1, 현장과의거리
* 현장도착시각-년, 현장도착시각-월, 현장도착시각-일, 현장도착시각-시간, 현장도착시각-분
* 신고시각-년, 신고시각-월, 신고시각-일, 신고시각-시간, 신고시각-분

Feature Reduction

* Using PCA, The characteristics of '의식상태', '환자증상1', and '현장과의거리' are combined to form one dimension.

Encoding

* To give different weights for each patient's state of consciousness and symptoms.
</details>

---

<details>
<summary>[Data Modeling and Evalution] - KMeans Clustering 2-D</summary>
<br/><br/>
  
Model
* KMeans Clustering

K
* 6
* It is judged that the most ideal clustering was achieved by separating the X-axis and the Y-axis.

Evaluation
* Elbow Method
  -  When K is 2 or 3, the arrival time on the X axis is not separated, so it is judged that it is not meaningful clustering.
* silhouette_score
  - When K is 5, the arrival time on the X-axis is not separated in a situation where the value of the Y-axis is large, so it is judged that it is not meaningful clustering.


<img width="330" alt="스크린샷 2023-06-10 오전 3 26 40" src="https://github.com/RyuKwanKon/Golden_Time_Finding_The_Underprivileged/assets/97783148/a102b81f-db2a-4bdf-ad4c-7f47ffa9fa0a">
</details>

---

<details>
<summary>[Analysis]</summary>
<br/><br/>
  
* It is expressed as the frequency of labels of clustering according to each region of Seongnam-si.
* In most dongs in Seongnam-si, the values corresponding to the first cluster appear to be distributed in the majority. Therefore, most areas in Seongnam City are predicted to be able to get help quickly in emergencies.
  
<img width="836" alt="스크린샷 2023-06-10 오전 3 24 03" src="https://github.com/RyuKwanKon/Golden_Time_Finding_The_Underprivileged/assets/97783148/91abd116-199b-4ad9-bedb-eba9f1eda6fc">
</details>

---

[Reference]
<br/><br/>
Dataset: https://data.gg.go.kr/portal/data/service/selectServicePage.do?infId=SE00GA6F273B8PIJ9N8412495661&infSeq=1
