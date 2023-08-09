import numpy as np

import pandas as pd

import matplotlib.pyplot as plt

import seaborn as sns

pip install matplotlib seaborn plotlypip install matplotlib seaborn
plotly

filename=r\'I:\\Metterial\\02) EDA (Explotory data analysis\\Group case
study 4-08-2023\\New folder\\New folder\\loan.csv\'

loan = pd.read_csv(filename,dtype=object)

loan.head()

  -------- --------- --------------- --------- --------------- ------- ----------------- ------- --------------------- ------------- ---------- -------- -------------- -------- ----------------- -------- ----------- --- --------------- ---- ---------- ------ ------------------------ ----- ------------------------ ----- -------------------- ----- ---------------------- ----- -------------------------- --- --------------- --- --------------------- ----- ----------------------- ----- -------------------- ----- -------------------------------- -----
  **id**             **member_id**             **loan_amnt**           **funded_amnt**           **funded_amnt_inv**                 **term**            **int_rate**            **installment**            **grade**       **sub_grade**        **\...**          **num_tl_90g_dpd_24m**         **num_tl_op_past_12m**         **pct_tl_nvr_dlq**         **percent_bc_gt_75**         **pub_rec_bankruptcies**       **tax_liens**       **tot_hi_cred_lim**         **total_bal_ex_mort**         **total_bc_limit**         **total_il_high_credit_limit**   

  **0**    573354                    737474                    10000                     100                           9950                     36                      7.51%                      311.11               A                   A4              \...                            NaN                            NaN                        NaN                          NaN                              0                   0                         NaN                           NaN                        NaN                                    NaN
                                                                                                                                                months                                                                                                                                                                                                                                                                                                                                                                                                            

  **1**    476321                    603324                    15000                     15000                         14800                    36                      8.94%                      476.58               A                   A5              \...                            NaN                            NaN                        NaN                          NaN                              0                   0                         NaN                           NaN                        NaN                                    NaN
                                                                                                                                                months                                                                                                                                                                                                                                                                                                                                                                                                            

  **2**    451484                    556265                    2000                      2000                          2000                     36                      13.57%                     67.94                C                   C3              \...                            NaN                            NaN                        NaN                          NaN                              0                   0                         NaN                           NaN                        NaN                                    NaN
                                                                                                                                                months                                                                                                                                                                                                                                                                                                                                                                                                            

  **3**    1018129                   1246557                   35000                     35000                         33951.84413              60                      20.89%                     944.71               F                   F1              \...                            NaN                            NaN                        NaN                          NaN                              2                   0                         NaN                           NaN                        NaN                                    NaN
                                                                                                                                                months                                                                                                                                                                                                                                                                                                                                                                                                            

  **4**    800018                    1005270                   14000                     14000                         14000                    60                      17.49%                     351.64               D                   D5              \...                            NaN                            NaN                        NaN                          NaN                              0                   0                         NaN                           NaN                        NaN                                    NaN
                                                                                                                                                months                                                                                                                                                                                                                                                                                                                                                                                                            
  -------- --------- --------------- --------- --------------- ------- ----------------- ------- --------------------- ------------- ---------- -------- -------------- -------- ----------------- -------- ----------- --- --------------- ---- ---------- ------ ------------------------ ----- ------------------------ ----- -------------------- ----- ---------------------- ----- -------------------------- --- --------------- --- --------------------- ----- ----------------------- ----- -------------------- ----- -------------------------------- -----

5 rows × 111 columns

In \[7\]:

*#looking all the colunms name*

loan.columns

Out\[7\]:

Index(\[\'id\', \'member_id\', \'loan_amnt\', \'funded_amnt\',
\'funded_amnt_inv\',

\'term\', \'int_rate\', \'installment\', \'grade\', \'sub_grade\',

\...

\'num_tl_90g_dpd_24m\', \'num_tl_op_past_12m\', \'pct_tl_nvr_dlq\',

\'percent_bc_gt_75\', \'pub_rec_bankruptcies\', \'tax_liens\',

\'tot_hi_cred_lim\', \'total_bal_ex_mort\', \'total_bc_limit\',

\'total_il_high_credit_limit\'\],

dtype=\'object\', length=111)

In \[10\]:

loan.info()

\<class \'pandas.core.frame.DataFrame\'\>

RangeIndex: 39717 entries, 0 to 39716

Columns: 111 entries, id to total_il_high_credit_limit

dtypes: object(111)

memory usage: 33.6+ MB

In \[8\]:

*#summaring number of the missing value in each column*

​

loan.isnull().sum()

​

Out\[8\]:

id 0

member_id 0

loan_amnt 0

funded_amnt 0

funded_amnt_inv 0

\...

tax_liens 39

tot_hi_cred_lim 39717

total_bal_ex_mort 39717

total_bc_limit 39717

total_il_high_credit_limit 39717

Length: 111, dtype: int64

##percentes of missing value in each columns

round(loan.isnull().sum()/len(loan.index), 2)\*100

In \[14\]:

round(loan.isnull().sum()**/**len(loan.index), 2)**\***100

Out\[14\]:

id 0.0

member_id 0.0

loan_amnt 0.0

funded_amnt 0.0

funded_amnt_inv 0.0

\...

tax_liens 0.0

tot_hi_cred_lim 100.0

total_bal_ex_mort 100.0

total_bc_limit 100.0

total_il_high_credit_limit 100.0

Length: 111, dtype: float64

In \[16\]:

missing_columns **=**
loan.columns\[100**\***(loan.isnull().sum()**/**len(loan.index)) **\>**
90\]

print(missing_columns)

Index(\[\'mths_since_last_record\', \'next_pymnt_d\',
\'mths_since_last_major_derog\',

\'annual_inc_joint\', \'dti_joint\', \'verification_status_joint\',

\'tot_coll_amt\', \'tot_cur_bal\', \'open_acc_6m\', \'open_il_6m\',

\'open_il_12m\', \'open_il_24m\', \'mths_since_rcnt_il\',
\'total_bal_il\',

\'il_util\', \'open_rv_12m\', \'open_rv_24m\', \'max_bal_bc\',
\'all_util\',

\'total_rev_hi_lim\', \'inq_fi\', \'total_cu_tl\', \'inq_last_12m\',

\'acc_open_past_24mths\', \'avg_cur_bal\', \'bc_open_to_buy\',
\'bc_util\',

\'mo_sin_old_il_acct\', \'mo_sin_old_rev_tl_op\',
\'mo_sin_rcnt_rev_tl_op\',

\'mo_sin_rcnt_tl\', \'mort_acc\', \'mths_since_recent_bc\',

\'mths_since_recent_bc_dlq\', \'mths_since_recent_inq\',

\'mths_since_recent_revol_delinq\', \'num_accts_ever_120_pd\',

\'num_actv_bc_tl\', \'num_actv_rev_tl\', \'num_bc_sats\', \'num_bc_tl\',

\'num_il_tl\', \'num_op_rev_tl\', \'num_rev_accts\',
\'num_rev_tl_bal_gt_0\',

\'num_sats\', \'num_tl_120dpd_2m\', \'num_tl_30dpd\',
\'num_tl_90g_dpd_24m\',

\'num_tl_op_past_12m\', \'pct_tl_nvr_dlq\', \'percent_bc_gt_75\',

\'tot_hi_cred_lim\', \'total_bal_ex_mort\', \'total_bc_limit\',

\'total_il_high_credit_limit\'\],

dtype=\'object\')

In \[17\]:

loan **=** loan.drop(missing_columns, axis**=**1)

print(loan.shape)

(39717, 55)

In \[11\]:

*\# percentes of missing values 100%*

In \[17\]:

100**\***(loan.isnull().sum()**/**len(loan.index))

Out\[17\]:

id 0.000000

member_id 0.000000

loan_amnt 0.000000

funded_amnt 0.000000

funded_amnt_inv 0.000000

\...

tax_liens 0.098195

tot_hi_cred_lim 100.000000

total_bal_ex_mort 100.000000

total_bc_limit 100.000000

total_il_high_credit_limit 100.000000

Length: 111, dtype: float64

In \[28\]:

loan.index

Out\[28\]:

RangeIndex(start=0, stop=39717, step=1)

In \[ \]:

*#missinng Value check*

In \[42\]:

loan.isnull().sum(axis**=**1)

Out\[42\]:

0 56

1 56

2 56

3 54

4 55

..

39712 60

39713 60

39714 60

39715 60

39716 60

Length: 39717, dtype: int64

In \[55\]:

loan.info()

\<class \'pandas.core.frame.DataFrame\'\>

RangeIndex: 39717 entries, 0 to 39716

Columns: 111 entries, id to total_il_high_credit_limit

dtypes: object(111)

memory usage: 33.6+ MB

In \[60\]:

loan.loc\[:, \[\'desc\', \'mths_since_last_delinq\'\]\].head()

Out\[60\]:

  ------- ------------------------------------------- ----------------------------
          **desc**                                    **mths_since_last_delinq**

  **0**   Borrower added on 08/30/10 \> thank         NaN
          you\<br/\>                                  

  **1**   Borrower added on 01/14/10 \> Green city    NaN
          hous\...                                    

  **2**                                               NaN

  **3**   Borrower added on 11/10/11 \> Consolidate   NaN
          all\...                                     

  **4**   Borrower added on 06/29/11 \> thanks for    21
          the \...                                    
  ------- ------------------------------------------- ----------------------------

In \[64\]:

*#dropping two columns*

​

loan **=** loan.drop(\[\'desc\', \'mths_since_last_delinq\'\],
axis**=**1)

In \[65\]:

loan.isnull().sum(axis**=**1)

Out\[65\]:

0 56

1 56

2 56

3 54

4 55

..

39712 60

39713 60

39714 60

39715 60

39716 60

Length: 39717, dtype: int64

In \[71\]:

column_unique **=** loan.nunique()

print(column_unique)

id 39717

member_id 39717

loan_amnt 885

funded_amnt 1042

funded_amnt_inv 8205

\...

tax_liens 1

tot_hi_cred_lim 0

total_bal_ex_mort 0

total_bc_limit 0

total_il_high_credit_limit 0

Length: 109, dtype: int64

In \[72\]:

loan\[\'term\'\].value_counts()

Out\[72\]:

36 months 29096

60 months 10621

Name: term, dtype: int64

In \[ \]:

*#\<matplotlib.axes.\_subplots.AxesSubplot at 0x23999eef8e0\>*

In \[75\]:

loan\[\'int_rate\'\].plot.box()

Out\[75\]:

\<Axes: \>

![](vertopal_746f1f891c4f434eb4ac18aef4cb883b/media/image1.png){width="5.559722222222222in"
height="4.129861111111111in"}

In \[76\]:

*#we can see some outlier values in int_rate column which needs to
analysed when we do univariate analysis*

​

loan\[\'grade\'\].value_counts()

Out\[76\]:

B 12020

A 10085

C 8098

D 5307

E 2842

F 1049

G 316

Name: grade, dtype: int64

In \[77\]:

loan\[\'sub_grade\'\].value_counts()

Out\[77\]:

B3 2917

A4 2886

A5 2742

B5 2704

B4 2512

C1 2136

B2 2057

C2 2011

B1 1830

A3 1810

C3 1529

A2 1508

D2 1348

C4 1236

C5 1186

D3 1173

A1 1139

D4 981

D1 931

D5 874

E1 763

E2 656

E3 553

E4 454

E5 416

F1 329

F2 249

F3 185

F4 168

F5 118

G1 104

G2 78

G4 56

G3 48

G5 30

Name: sub_grade, dtype: int64

In \[ \]:

*\# Drop additional columns we don\'t need these as these are mostly
nulls.*

​

columns_drop_list1 **=**
\[\"desc\",\"mths_since_last_delinq\",\"mths_since_last_record\",\"next_pymnt_d\",\"tot_hi_cred_lim\"\]

loan.drop(labels **=** columns_drop_list1, axis **=**1,
inplace**=True**)

columns_drop_list2 **=**
\[\"mths_since_last_major_derog\",\"total_bal_ex_mort\",\"total_bc_limit\",\"total_il_high_credit_limit\"\]

loan.drop(labels **=** columns_drop_list2, axis **=**1,
inplace**=True**)

columns_drop_list3 **=**
\[\"member_id\",\"url\",\"emp_title\",\"zip_code\",\"tax_liens\"\]

loan.drop(labels **=** columns_drop_list3, axis **=**1,
inplace**=True**)

In \[90\]:

loan\[\'loan_amnt\'\].describe()

Out\[90\]:

count 39717

unique 885

top 10000

freq 2833

Name: loan_amnt, dtype: object

In \[91\]:

sns.boxplot(loan.loan_amnt)

Out\[91\]:

\<Axes: \>

![](vertopal_746f1f891c4f434eb4ac18aef4cb883b/media/image2.png){width="5.7in"
height="4.129861111111111in"}

In \[92\]:

sns.boxplot(loan.total_pymnt)

Out\[92\]:

\<Axes: \>

![](vertopal_746f1f891c4f434eb4ac18aef4cb883b/media/image3.png){width="5.7in"
height="4.129861111111111in"}

In \[93\]:

sns.boxplot(loan.annual_inc)

Out\[93\]:

\<Axes: \>

![](vertopal_746f1f891c4f434eb4ac18aef4cb883b/media/image4.png){width="5.340277777777778in"
height="4.279861111111111in"}

In \[94\]:

sns.boxplot(loan.int_rate)

Out\[94\]:

\<Axes: \>

![](vertopal_746f1f891c4f434eb4ac18aef4cb883b/media/image5.png){width="5.559722222222222in"
height="4.129861111111111in"}

In \[97\]:

*\# Univariate Analysis - Unordered Categorical Variables - Home
Ownership*

​

plt.figure(figsize**=**(10,6),facecolor**=**\'b\')

ax **=**
sns.countplot(x**=**\"home_ownership\",data**=**loan,hue**=**\'loan_status\',palette**=**\'GnBu_d\')

ax.legend(bbox_to_anchor**=**(1, 1))

ax.set_title(\'Home Ownership\',fontsize**=**14,color**=**\'w\')

ax.set_xlabel(\'Home Ownership\',fontsize**=**14,color **=** \'w\')

ax.set_ylabel(\'Loan Application Count\',fontsize**=**14,color **=**
\'w\')           

plt.show()

​

*\# Observations :*

*\# Below plot shows that most of them living in rented home or
mortgazed their home.*

*\# Applicant numbers are high from these categories so charged off is
high too.*

![](vertopal_746f1f891c4f434eb4ac18aef4cb883b/media/image6.png){width="8.779861111111112in"
height="5.559722222222222in"}

In \[98\]:

*\# Univariate Analysis - Ordered Categorical Variables- Loan Paying
Term*

​

plt.figure(figsize**=**(10,6),facecolor**=**\'b\')

ax **=**
sns.countplot(x**=**\"term\",data**=**loan,hue**=**\'loan_status\',palette**=**\'GnBu_d\')

ax.set_title(\'Loan Paying Term\',fontsize**=**14,color**=**\'w\')

ax.set_xlabel(\'Loan Repayment Term\',fontsize**=**14,color **=** \'w\')

ax.set_ylabel(\'Loan Application Count\',fontsize**=**14,color **=**
\'w\')           

ax.legend(bbox_to_anchor**=**(1, 1))

plt.show()

![](vertopal_746f1f891c4f434eb4ac18aef4cb883b/media/image7.png){width="8.779861111111112in"
height="5.559722222222222in"}

In \[ \]:

​
