# Kickstarting with Excel

## Overview of Project

### Purpose

The purpose of this project was to provide Louise, an individual who is looking to raise money for her play, with insight into different Kickstarter campaigns based on their launch dates and funding goals. The first analysis will focus on visualizing campaign outcomes based on launch date.  Outcomes for this analysis include Kickstarter theater projects that were either successful or failed in obtaining their funding goals.  Additionally, projects that were canceled would be included in the analysis for further insight into prior fundraising campaigns.  The aim of this analysis to provide Louise with information regarding when is the best time to launch a Kickstarter fundraising project in order to increase its likelihood of success.  The second analysis will explore the percentage of successful, failed, and canceled Kickstarter campaigns for plays based on their funding goals.  The goal of this analysis is to provide Louise will a more detailed understanding of which fundraising goals were most likely to lead to a successful Kickstarter campaign.

## Analysis and Challenges

### Analysis of Outcomes Based on Launch Date

Kickstarter analysis of outcomes based on launch date was conducted using the data obtained from file named Kickstarter_Challenge.xlsx.  The spreadsheet contains the following relevant data on Kickstarter campaigns:

1. Funding Goal (Column D)
2. Outcomes: listed as successful, failed, live, and canceled (Column F)
3. Launched_at (Column J)
4. Category and Subcategory of campaign (Column N)

In order to obtain the year in which a campaign was launched, the “launched_at” column needs to be converted from Unix timestamps to proper dates including day, month, and year.  This is completed using the following formula:

```
=(((J2/60)/60)/24)+DATE(1970,1,1)
```

A new column, “Date Created Conversion” (Column R) was created and populated using the above formula and DATE function for all campaigns.  The equation was modified to include the relevant cells for each campaign.  It should be noted that for the purposes of this analysis “Date Created Conversion” and “Launch Date” will be used interchangeably.  An additional column was created to extract just the launch year (Column T).  It was populated using the following function:

```
=YEAR(R2)
```

This function was applied for each campaign adjusted for the relevant cell of each Kickstarter project.

Using the Category and Subcategory column, a new Parent Category column was created (Column O).  This was achieved using the following steps:

1. Select the “Category and Subcategory” column.
2. Copy and paste the column into the next available column. Rename column “Parent Category”.
3. Click Data tab.
4. Click the “Text to Columns” button.
5. When the “Convert Text to Columns Wizard” opens select “Delimited” and click “Next”
6. Uncheck the “Tab” box and select “Other”.  
7. Place a backslash symbol in the text box and select “Next”.  
8. Click “Text” from “Column data format.”  
9. Select Finish.

The “Parent Category” columns can now be populated with information just containing the parent category data from the “Parent and Subcategory” column.  Secondarily, a “Subcategory” column (Column P) has been created and populated with its relevant data as well.

Now that the data has been organized, a new pivot table was created using the following steps:

1. Select the “Insert” tab.
2. Click on “Pivot Table” button.
3. Select the whole table of data as Table/Range.
4. Choose to place the new pivot table in a new worksheet.
5. Label the new worksheet “Theater Outcomes by Launch Date”.
6. Filter the pivot table based on “Parent Category” and “Years”.
7. Place “Outcomes” in columns section.
8. Place “Date Created Conversion” in rows section.
9. Place “Outcomes” in the values section.
10. Filter the columns of the table to include only “successful”, “failed”, and “canceled” campaigns.
11. To present the first column in months instead of years, group the data in the column by highlighting the data. Right click the data and select “Group”.  Select “Months” in the pop-up window and click on the “OK” button.
12. Filter the “Parent Category” to show only data from “theater”.
13. Sort the campaign outcome in descending order so that “successful” campaigns are shown first, followed by “failed” campaigns and ending with “canceled” campaigns.

Using the formatted pivot table, a line chart was created comparing outcomes of Kickstarter campaigns against their month of launch.  The y-axis was the number of Kickstarter campaigns and the x-axis was the month in which the campaign was started.  Three individual lines were constructed to measure the number of campaigns that were successful, failed, or canceled for each month.  The title “Theater Outcomes Based on Launch Date” was added to complete the line chart.  The finished chart can viewed by following the link below:

(https://raw.githubusercontent.com/jbowman86/kickstarter-analysis/31d74d84419699e37657b7fe6db2de80c5a9a52e/Resources/Theater_Outcomes_vs_Launch.png)

### Analysis of Outcomes Based on Goals

Kickstarter analysis of outcomes based on fundraising goals was also conducted using the data obtained from file named Kickstarter_Challenge.xlsx.  The spreadsheet contains the following relevant data on Kickstarter campaigns:

1. Funding Goal (Column D)
2. Outcomes: listed as successful, failed, live, and canceled (Column F)
3. Subcategory of campaign (Column P)

The following steps were used to obtain results on campaign outcomes based on goals:

1. Create a new worksheet and label it “Outcomes Based on Goals.”
2. Create columns for each of the following data: Goal, Number Successful, Number Failed, Number Canceled, Total Projects, Percentage Successful, Percentage Failed, Percentage Canceled.
3. In the “Goal” column, add the following dollar-range amounts: 
    - Less than 1000
    - 1000 to 4999
    - 5000 to 9999
    - 10000 to 14999
    - 15000 to 19999
    - 20000 to 24999
    - 25000 to 24999
    - 25000 to 29999
    - 30000 to 34999
    - 35000 to 39999
    - 40000 to 44999
    - 45000 to 49999
    - 50000 or More
  
4. COUNTIFS() functions were used to populate the “Number Successful”, “Number Failed” and “Number “Canceled” columns.  Columns were filtered using “outcome” column and the goal amount ranges listed above in Step 3.  The “Subcategory” column was also used to filter only campaigns for plays.  The following is examples are the COUNTIFS() function that was used for this analysis:
a. Function for successful Kickstarter plays with fundraising goal of less than 1000
```
=COUNTIFS(Kickstarter!$F:$F,"successful",Kickstarter!$P:$P,"plays",Kickstarter!$D:$D,"<1000")
```
b. Function for successful Kickstarter plays with fundraising goal of between 1000 to 4999
```
=COUNTIFS(Kickstarter!$F:$F,"successful",Kickstarter!$P:$P,"plays",Kickstarter!$D:$D,">=1000",Kickstarter!$D:$D,"<5000")
```
The formula above was applied for all fundraising goals ranges between 5000 to 49999 replacing the relevant amounts in the filtered ranges. 

c. Function for successful Kickstarter plays with fundraising goal of 50000 or more

```
=COUNTIFS(Kickstarter!$F:$F,"successful",Kickstarter!$P:$P,"plays",Kickstarter!$D:$D,">50000")
```
All of the formulas above were repeated to the populate the “Number of Failed” and “Number of Canceled” columns.

5. SUM() function was used to populate the “Total Projects” column with total number of successful, failed, and canceled projects for each row.  An example formula for the first row is included below:

```
=SUM(B2:D2)
```

6. The percentage of successful, failed, and canceled Kickstarter q	campaigns was calculated for each row using the following formulas:
  - Formula for percentage successful Kickstarter plays with fundraising goal of less than 1000
		
    ```
	=B2/E2
	  ```

  - Formula for percentage failed Kickstarter plays with fundraising goal of less than 1000

     ```
     =C2/E2
     ```

  - Formula for percentage canceled Kickstarter plays with fundraising goal of less than 1000
       	
      ```
      =D2/E2
      ```
In order to present the above tabulations as a percentage, select the percentage button located along the “Home” toolbar.  Steps 6a to 6c were repeated for each fundraising goal range in order to populate the rest of the “Percentage Successful”, “Percentage Failed”, and “Percentage Canceled” columns.


7. A line chart was created by clicking the “Insert” Tab and selecting the line chart graphic.  Fundraising goal amount ranges were selected to be the x-axis and the y-axis was percentage of projects.  Three lines were created represented the percentage of successful, failed, and canceled projects for each fundraising goal range.  The finished chart can viewed by following the link below:

( https://raw.githubusercontent.com/jbowman86/kickstarter-analysis/31d74d84419699e37657b7fe6db2de80c5a9a52e/Resources/Outcomes_vs_Goals.png)


### Challenges and Difficulties Encountered

There were no difficulties encountered during this analysis; however, there are a few important aspects that need to be considered in order to reduce likelihood of errors.

1.	It may be difficult for some analysts to convert the Unix timestamps used in “launched_at” column (Column J) into a useable date if they are unfamiliar to this format.  The Unix timestamps present the time in seconds since midnight of January 1, 1970.  The equation used to convert the Unix timestamps into a date requires division of the cell value by 60 for seconds, divide from 60 again for minutes and finally divide by 24 to account for hours.  The Date formula is then used to take this calculated value and convert it to a date.  
2.	Some analysts may have difficulty in presenting the launch date in months rather than the default from the spreadsheet of years.  This requires an understanding of grouping data.  This issue can easily be resolved by highlighting the year data in the table then right clicking to open the option to group the data. The menu that pops up will allow for selection of years in a variety of intervals, one of which is months.  Selecting months will present the data in a monthly format.
3.	It is possible to believe that the line chart measuring outcomes based on goals is incorrect presenting canceled Kickstarter results despite accurately creating the chart.  This is due to there being no Kickstarter campaigns for plays being canceled.  The Percantage Canceled overlaps with the x-axis line and can appear to be hidden.

## Results

### Conclusions about Outcomes Based on Launch Date

Based on the analysis of outcomes in relation to launch date, it can be concluded that the best time to start a Kickstarter campaign for a theater project was during the month of May.  This can be attributed to the fact that May had the greatest totals number of successful campaigns.  Conversely, the worst month to start a theater Kickstarter campaign was during the month of October.  Although there were more total failed campaigns in May, a greater proportion of the Kickstarter campaigns started in October failed compared to those projects launched in May.

### Conclusion about Outcomes Based on Goals

Based on the analysis of outcomes with respect to fundraising goals, the campaigns that aimed to raise less than 1000 dollars had the highest success rate and those striving to raise between 1000 and 4999 dollars having the second highest rate of success.  

### Limitations of the Dataset

Some limitations in the current dataset include that there a very few Kickstarter campaigns that aimed to raise 25000 dollars or more.  This makes it difficult to ascertain truly accurate conclusions for funding goals in this range as inferences are derived from limited data.  For example, there was only one project that had a funding goal between 45000 and 49999 dollars.  It was unsuccessful thereby resulting in 100% of the plays that aimed to raise this range of funds being considered failures.  If a second campaign was launched in this fundraising goal category and was successful, our conclusion would be that 50% of campaigns would be funded dramatically changing our overall conclusions.  Additionally, this dataset only considers projects funded through Kickstarter.  There are multiple other crowdfunding companies and perhaps there is greater success or failure in reaching funding goals in one of these other platforms.  Lastly, the dataset possesses missing data with respect to canceled theater Kickstarter campaigns launched in October.  Conclusions related to campaigns launched in October are incomplete due to the absence of this data. 

### Additional Analyses 

Some additional analyses that could be performed in order to gain further insight into successful Kickstarter campaigns are comparing successful, failed, and canceled theater campaigns based on country, rate of success based on number of backers and average donation, and number of successful campaigns based on year campaigns were launched rather than just focusing on the launch month.  These analyses can help focus on trends that have led to successful past Kickstarter campaigns.
