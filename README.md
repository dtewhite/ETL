Extract 
  The process started with defining out primary data sources. We settled on three from separate government agencies due to the 
  comprehensiveness and potentially interesting trends that could be found among them. 
  US Department of Health and Human Services - Health Insurance Coverage (Source)
  Center for Disease Control - Death in the United States (Source)
  Center for Disease Control - Tobacco Use - Adults Who Are Current Smokers for 1995-2010 (Source)

Transform 
  We had to adjust the raw data for all three sources to set the data up properly to be input into our database.

  Health Insurance Coverage: 
    This required primarily excel work to transform to a useable dataset. Initially every year was its own column which housed four 
    column within that. We transposed to rows so that we can reference the data across years and across states/type of coverage. This 
    was relatively manual but was the most efficient way to do this. 

    We then loaded this CSV to Pandas and filtered for just the percent of people who were uninsured between 2008 and 2010. Our final 
    data frame had the columns year, state and the rate of uninsured people. We exported this as a CSV.

  Death in the United States: 
    This was easiest to transform in python. We did primarily three transformations to this. Since the dataset was so large, every death 
    in the US, we had to filter the CSVs. So, we wrote a group by script that allowed us to count the amount of deaths that fell into a 
    given code. Then, each cause of death had its own count instead of every row being an individual death. 

    The second transformation was also done in python. We unioned of all of the CSVs. This required adding a column that accounted for 
    the year the CSV represented then joining them all together. 
  
    The final transformation to this set was adding in the actual name of the cause of death instead of using an ID. The Cause of Death 
    dataset uses a number to identify an individual's cause of death, 358-cause-recode. This needed to be mapped to the actual cause of 
    death so, when we get to the analysis part it would be useable. 
 
  Tobacco Use:
    This transformation took place in python.  We filtered this data set to match the available years that we had for both insurance and 
    cause of death in the United States. Along with this for data quality, we removed unnecessary columns keeping only Year,  State, and 
    % Smoking Adults.


Load
  Using psycopg2, we created each of these as separate tables in a brand new database, etl_db. We hosted this on a local Postgres 
  instance. 
