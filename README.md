# Banking-and-Finance-for-DA
This repo will help new DA folks to re use code to get a better analysis report related to banking and finance.
## Common Banking and Finance Terminologies
### - Customer Identification Number (CIN)
      A CIN (Customer Identification Number), also known as CIN ID, is an X- length alphanumeric unique 
      identifier used by banks to identify customers and store their personal information.
### - Account Number
      A bank account number is a unique set of digits assigned to the account when you open a bank account.
      Financial institutions will assign such numbers to each account you hold. Businesses and banks use these numbers to identify your account.
### - Account Opening Date
      The account opening date is the date on which the account has been made active and it means that the account opened in the system
      is connected to the bank server. It may be after one day or two days in the case of intervening holiday if any.
### - Account Close Date
      A closing date is when your billing cycle ends and a new “statement period” begins. Again, the bank will also account for any
      interest from hanging balances on your closing date.
### - Account Opening Balance
      An opening balance is the amount in an account at the start of an accounting period. 
### - Account Closing Balance
      In banking, the closing balance simply refers to the bank balance at the end of a day, month, or year. This includes both credit and debit amounts.
## Data frame column format (String)
## Group by in detail
   Group by is one of the most frequently used SQL clauses. It allows you to collapse a field into its distinct values. 
   This clause is most often used with aggregations to show one value per grouped field or combination of fields.
   ![image](https://github.com/MartandCV/Banking-and-Finance-for-DA/assets/114132628/c6c033fa-e5b5-4725-8a1c-1951e17d3eb3)

   We can use an SQL group by and aggregates to collect multiple types of information. For example, an SQL group by can quickly tell us the number of countries on each continent.

   How many countries are in each continent?

      select
      continent
      , count(*)
      from
      countries
      group by 
      continent

![image](https://github.com/MartandCV/Banking-and-Finance-for-DA/assets/114132628/f201ab2d-0e6b-4d77-aff3-735ee71fa552)

Keep in mind when using SQL GROUP BY:

Group by X means put all those with the same value for X in the same row.
Group by X, Y put all those with the same values for both X and Y in the same row.
Analytics adoption has stalled; only infused analytics can help

Learn more
More Interesting Things About SQL GROUP BY
1. Aggregations Can Be Filtered Using The HAVING Clause
You will quickly discover that the where clause cannot be used on an aggregation. For instance:

select 
  continent
  , max(area)
from
  countries
where 
  max(area) >= 1e7
group by 
  1
will not work, and will throw an error. This is because the where statement is evaluated before any aggregations take place. The alternate having is placed after the group by and allows you to filter the returned data by an aggregated column.

Using having, you can return the aggregate filtered results!

2. You Can Often GROUP BY Column Number
In many databases, you can group by column number as well as column name. Our first query could have been written:

select
  continent
  , count(*)
from 
  base
group by 
  1
and returned the same results. This is called ordinal notation and its use is debated. It predates column based notation and was SQL standard until the 1980s. 

It is less explicit, which can reduce legibility for some users. 
It can be more brittle. A query select statement can have a column name changed and continue to run, producing an unexpected result.
On the other hand, it has a few benefits.

SQL coders tend toward a consistent pattern of selecting dimensions first and aggregates second. This makes reading SQL more predictable.
It is easier to maintain on large queries. When writing long ETL statements, I have had group by statements that were many, many lines long. I found this difficult to maintain.
Some databases allow using an aliased column in the group by. This allows a long case statement to be grouped without repeating the full statement in the group by clause. Using ordinal positions can be cleaner and prevent you from unintentionally grouping by an alias that matches a column name in the underlying data. For example, the following query will return the correct values:
-- How many countries use a currency called the dollar?
select
  case when currency = 'Dollar' then currency
    else 'Other'
  end as currency --bad alias
  , count(*)
from
  countries
group by
  1
Currency count table
But this will not, and will segment by the base table’s currency field while accepting the new alias column labels:

select
  case when currency = 'Dollar' then currency 
    else 'Other' 
  end as currency --bad alias
  , count(*)
from 
  countries
group by 
  currency
Dollar and others chart
This is ‘expected’ behavior, but remain vigilant.

A common practice is to use ordinal positions for ad hoc work and column names for production code. This will ensure you are being completely explicit for future users who need to change your code.

3. The Implicit GROUP BY
There is one case where you can take an aggregation without using a group by. When you are aggregating the full table there is an implied SQL group by. This is known as the <grand total> in SQL standards documentation.

-- What is the largest and average country size in Europe?
select
  max(area) as largest_country
  , avg(area) as avg_country_area
from 
  countries
where 
  continent = 'Europe'
Largest country table
4. GROUP BY Treats Null as Groupable Value, and that is Strange.
When your data set contains multiple null values, group by will treat them as a single value and aggregate for the set.

This does not conform to the standard use of null, which is never equal to anything including itself.

select null = null
-- returns null, not True
## Break a dataframe containing array
## Explode function in detail
## Break a dataframe containing structure
## Convert and dataframe column to list
## Search one column data into another
## Things to remember while performing join
## Difference between spark and pyspark coding style
## Create and data analysis report for client
## Different type of files you will come across (delta, parquet,csv,xlsx)
## Common functions used during data analysis.
## Difference and percentage rate calculation for two columns in a dataframe.
## Importance of creating tempview for a dataframe.
## GDA, MDA, CDA
