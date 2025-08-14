# Operational-Efficiency-in-Claims-Processing
## Project Goal:
The operational efficiency department wants to identify sources of claims processing times delay and make some decisions to improve it.
<a href="https://github.com/Leonel-web-byte/Operational-Efficiency-in-Claims-Processing/blob/main/Cleaned_Data.xlsx">Dataset</a>
## Questions (KPIs):
-	What is the average processing time (Days)?
-	What is the percentage of claims processed after 30 days?
-	Total Claims Volume
-	Which is the payer with the highest Avg Processing Time?
-	Which is the procedure with the highest Avg Processing Time?
-	Percentage of claims processing after 30 days vs within 30 days
-	Which are months with the highest Avg Processing Time?
-	Dashboard Interaction <a href= "https://github.com/Leonel-web-byte/Operational-Efficiency-in-Claims-Processing/blob/main/Claims_P.png">Dashboard</a>
## Process:
## Step 1: Validating and cleaning dates
-	I verified that for every claim, the Processed Date was equal to or later than the submitted date, which is a logical requirement. This check confirmed that the dates in the dataset are consistent and accurate, so no corrections were necessary.
- I used this Excel formula to check it:
IF([@[Processed Date]]>=[@[Submitted Date]],"Accurate”, “No Accurate")
## Step 2: Handling missing Denial Reasons
In the dataset, some claims with status “Denied” had missing values in the Denial Reason column. To prepare the data for analysis, I created a new column called “Denial reason2” to fill these missing values with a placeholder value “Unknown” only for denied claims.
- I used this excel formula to do it:
  IF(OR([@Status]="pending",[@Status]="Paid"),"",IF(AND([@Status]="Denied", ISBLANK([@[Denial Reason]])),"Unknown",[@[Denial Reason]]))


## Step 3: Create new field
- I created a new column called “Processing Time”, which is the number of days between the day a claim was submitted and the day it was processed for “Paid” and “Denied” claims status only.
- I used this excel formula to do that:
  IF(OR([@Status]="paid",[@Status]="Denied"),[@[Processed Date]]-[@[Submitted Date]],"")

-	I created a second field called “Claim over 30”, which categorize the claim over 30.
- I used this Excel formula:
  IF(OR(ISBLANK([@[Processing Time]]),[@[Processing Time]]=""),"",IF([@[Processing Time]]>30,"Processing after 30 days","Processing within 30 days")).
- Created Pivot tables according to the questions asked
- Merge all charts into one dashboard and applied slicer to make it dynamic
## Dashboard
<img width="549" height="279" alt="Claims_P" src="https://github.com/user-attachments/assets/2c4be2ac-369f-4dc5-87bb-0f503cd25d05" />

## Project Insight:
- Two Payers, Blue Cross and Humana, have the highest Avg Processing Time
-	53.83% of claims are processed after 30 days
-	99214 and 99213 have the highest Avg processing Time among the procedures 
-	Between January and March 2023, the average processing time per claim increased, older cases required more time to be processed.
-	From April to May 2023, this average slightly increased again
-	From June to September 2023, the average processing time remained stable then increased in October before decreasing again.

## Recommendations:
- To improve the claim processing time an intern strategic plan consists to train again medical biller team because the procedure 99213 and 99214 had the highest processing time and the main reason of denial for these procedures were “No Authorization” and “Unknown”. The Biller team must investigate why some payers didn’t give the reason for some Denial claims, which is slowing down the claim processing time. It could be a data entry issue too.
  
- Also, before submitting any claim to Blue Cross and Humana, always make sure that the documentation was performed correctly.
- Based on observed spikes in processing time, it would be beneficial to allocate additional staff in March, May, and October to manage the backlog effectively.

