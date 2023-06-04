# Golden_Time_Finding_The_Underprivileged

### [Data Science Term Project - Golden_Time_Finding_The_Underprivileged]
Github :
https://github.com/RyuKwanKon/Golden_Time_Finding_The_Underprivileged</br>
DataSet :  https://drive.google.com/uc?id=1ez0tNCX49Cxjzt6Ir4jkxy7Z9TnzOV60

Team member
* 201935039 류관곤

### [Data curation And Load Dataset]

---

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
