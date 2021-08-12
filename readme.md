# AnselSebastian README<br/>
<br/>
Create a new environment and pip install the modules mentioned in requirements.txt<br/>
<br/>
##<br/>
Run the script "Minicomp_AnselSebastian.py"<br/>
<br/>
When you run the script, it will ask you for the holdout data file (it expects a csv file)<br/>
<br/>
##<br/>
Additional Store info is supposed to be found at data/Store.csv<br/>
<br/>
<br/>
## Features used in the final model<br/>
<br/>
### Original variables:<br/>
SchoolHoliday<br/>
Promo2<br/>
<br/>
### engineered variables (one-hot-encoding):<br/>
<br/>
PublicHoliday&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;          uses StateHoliday<br/> 
Easter&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                 uses StateHoliday<br/>
Christmas&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;              uses StateHoliday<br/>
storetype_a&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;            uses StoreType<br/>
storetype_b&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;            uses StoreType<br/>
storetype_c&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;            uses StoreType<br/>
storetype_d&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;            uses StoreType<br/>
assort_a &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;              uses Assortment<br/>
assort_b &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;              uses Assortment<br/>
assort_c &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;              uses Assortment<br/>
dow_1 - dow_7 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;         uses DayOfWeek<br/>
m_12  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                 Dummy for December (other dummies are dropped)<br/>
<br/>
### engineered variables (mean-encoded)<br/>
Sales_avg_store &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;        Average Sales for each store. This variable is merged into the Store.csv and then saved as a new feature of the stores for predictions<br/>

### engineered variables (more complex)<br/>
DayOfWeek_recode&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       just changed the sequence so that Sunday is the new 1, this can reflect the actual linear relationship between performance throughout week<br/>
logDistance &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;           logarithmic competition distance (in order to devaluatte extreme high numbers)<br/>
City_center  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;          low competition distance (<500) and long time competition (>10 years) indicates that the shop is placed in a crucial spot<br/>


date_delta  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;           0 for first day of dataset, then counts up each day until the end of dataset. Visual checking showed some stores had upwards trending data Sales (while i found no downward trends.)<br/>
monthstart             Dummy that is one for the first couple of days of a month. Visual checking indicated higher sales.<br/>
firstdaysweek13        Dummy identifies first and third week of month. Visual checking indicated that the first and thrid week of any month have higher average sales.<br/>
Fortnight_Days         first day of each month is 1 and counts up to 14, then starts again at 1.<br/>


prstart                Dummy that is 1 after the Promo2 campaigns startet<br/>
pr_campaign            Dummy that is 1 if a campaign is running. a campaign is running if the month is mentioned in "PromoInterval" and the date is<br/>
                        after the overall start of the campaign indicated in the variables 'Promo2SinceWeek' and 'Promo2SinceYear'<br/>
                       
Reopening              Dummy that is 1 on a day the shop was open , and that was precedet by at least 5 days of the shop being closed<br/>
<br/>
<br/>
<br/>
<br/>
## Model used<br/>

XGBoost with<br/>
    'n_estimators': [1000],<br/>
    'learning_rate' : [0.1],<br/>
    'colsample_bytree': [0.7],<br/>
    'max_depth': [5],<br/>
    'reg_alpha': [1.1],<br/>
    'reg_lambda': [1.3],<br/>
    'subsample': [0.9]<br/>
.. the rest are default parameters. <br/>

We used 10-fold cross-validation.<br/>



