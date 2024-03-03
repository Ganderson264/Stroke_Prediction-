The original data contained 5,110 records in healthcare-dataset-stroke-data.csv obtained from the Kaggle Website

This data is organized by the following columns and values/value ranges:
<ul>
  <li>gender : Female, Male, Other</li>
  <li>age : .08 to 82 years</li>
  <li>hypertension : 0 (no), 1 (yes)</li>
  <li>heart_disease : 0 (no), 1 (yes)</li>
  <li>ever_married : no, yes</li>
  <li>work_type : Children, Never worked,​ Self-Employed,​ Govt_job,​ Private​</li>
  <li>Residence_type : Urban, Rural</li>
  <li>avg_glucose_level : 55.12 to 271.74</li>
  <li>bmi : NaN, 10.3​ to 97.6​</li>
  <li>smoking_status : never, Smoked​, unknown​, Formerly smoked​, smokes​</li>
  <li>stroke : 0 (no), 1 (yes)</li>
</ul>
The dataset is EXTREMELY Inbalanced as less than 5% of the cases show a positive result for stroke
For the "First Model" the data was "cleaned" by:
<ul>
  <li>Dropping : 
    <ul>
      <li>the only record with gender as "Other"</li>
      <li>records with "NaN" as bmi value</li>
    </ul>
  <li>Encoding or replacing columns with 2 possible values :
    <ul>
      <li>replace "gender" with male values : 0 (no) or 1 (yes)</li>
      <li>encoded ever_married with values : 0 (no) or 1 (yes)</li>
      <li>replace Residence_Type with Urban : 0 (no) or 1 (yes)</li>
    </ul>
  </li>
</ul>
<ul>
  <li>Data set A set was created by Encoding or replacing columns with more than 2 possible values as follows:
  <ul>
    <li>from the work_type column others where created and assigned 0,1 values accordingly as follows:</li>
    <ul>
      <li>work_type_Govt_job</li>
      <li>work_type_Never_worked</li>
      <li>work_type_Private</li>
      <li>work_type_Self-employed</li>
      <li>work_type_children</li>
    </ul>
    <li>from the smoking_status column others where created and assigned 0,1 values accordingly as follows:</li>
    <ul>
      <li>smoking_status_Unknown</li>
      <li>smoking_status_formerly smoked</li>
      <li>smoking_status_never smoked</li>
      <li>smoking_status_smokes</li>
    </ul>
  </ul>
  <li>Data set B was created by Encoding values for columns with more than 2 possible values as follows:
  <ul>
    <li>the work_type column values where replaced based on a perceived stress level as follows:</li>
    <ul>
      <li>children : 0</li>
      <li>Never_worked : 1</li>
      <li>Govt_job : 2 </li>
      <li>Private : 3</li>
      <li>Self-employed : 4</li>
    </ul>
    <li>the smoking_status column values where replaced based on a perceived health risk level as follows:</li>
    <ul>
      <li>never smoked : 0</li>
      <li>Unknown : 1</li>
      <li>formerly smoked : 2</li>
      <li>smokes : 3</li>
    </ul>    
</ul>

    Scalled versions of Data sets A and B where created by running them through StandardScaller and MinMaxScaller
To these new Scalled versions
