# pre requisite KB - As you aware 

  * Data Modelling Concepts like 
             Contextual Data based on Key field, 
             Header table , 
             Detail table, 
             Relationship ( 1:1 , 1:*, *:*)

  * ELT -- Extraction, Loading then Transformation ( using M-Code and DAX)
  
  * SSAS/DW Concepts :
           Dimension Table,
           Fact Table,
           Measure
           Calculated Column Vs Calculated Measure,
           Types of Measures ( Full Addititve, Semi Additive and Non Addititve)   
           Types of Dimension( Confirmed, Role playing, SCD (I,II,III), Junk, Infred....) 
   
   * DAX Concepts:

            DAX Syntax --> Understand the way to frame DAX with standard and readable

            Return Type ( Scalar and Table)
            
            Types of functions
             
            What is expression - An expression with a scalar result, which will be evaluated for each row of the table in the first argument.
            Filter
            Time Intelligence

   
# Data Modelling for Sales Example
 * Understand Power BI Data Model 1:* along with DAX Basics

Sales Header --> Order Number ( summary of Sales Relates with CustomerKey, OrderDateKsy , CurrencyKey )
Sales Details--> Order Number ( details of Sales Relates with ProductKey) --> Quanitity {Sold}

Product     --> ProductKey ( Context to ProdcutCode, ProductName, UnitCost, UnitPrice, Weight)
Other Tables --> Date and Customer

# DAX

* Excel Funcion - reusable understaing

	SUM, Average, Max, Min, Count can be used as Measure not as New column; 
	These functions return the value based on dynamic extraction like filters, slicers, ( Rows + Column + Value ) in Table
	
	* Syntax :
	[Measure Name] := Sum(tableName[Field Name])
	
	* Example:
	Exsum = sum(SalesDetail[Quantity]) // also be used in  AVG, Max, Min, Count

* A - Aggregate Function 
    works in AverageA, CountA, MaxA, MinA
    
    handles non-numeric data types according to the following rules:

    1. It support Logical values; Logical value TRUE count as 1 &  FALSE count as 0 (zero).
    2. Values that contain non-numeric text count as 0 (zero).
    3. Empty text (“”) counts as 0 (zero).

  * Syntax : [Measure Name] := AverageX(TableName[Field Name])

  * Example : ExAverageA = AVERAGEA('Product'[ProductKey]) 

