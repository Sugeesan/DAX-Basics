# pre requisite KB - As you aware 

  * Data Modelling Concepts like 
             Contextual Data based on Key field, 
             Header table , 
             Detail table, 
             Relationship ( 1:1 , 1:m , m:m, m:1)
             Cross Filter direction : Single/Both? --> Performance

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

          
# Before Framing DAX Query

  * While creating a Measure, Understand where you create DAX on top of which table?
  * DAX Query works only with the table Related in the model, otherwise explicitly need to use RELATED() and ALLCROSSFILTERED
    for Example, consider the DAX --> ExAverageA = AVERAGEA('Product'[ProductKey])  
      * This works only when created a measure on SalesDetails table to filter with all other table fields.
   
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

* A - Aggregate Function (works similar as Average = AverageA)
    works in AverageA, CountA, MaxA, MinA
    
    handles non-numeric data types according to the following rules:

    1. It support Logical values; Logical value TRUE count as 1 &  FALSE count as 0 (zero).
    2. Values that contain non-numeric text count as 0 (zero).
    3. Empty text (“”) counts as 0 (zero).

  * Syntax : [Measure Name] := AverageX(TableName[Field Name])

  * Example : ExAverageA := AVERAGEA('Product'[ProductKey])

* X - Aggregate funcation (works similar if single field, much helpful while doing another arithmetic operator inside this)

  * Syntax : [Measure Name] := SumX(refTable, refTable[FieldName] )
  * Syntax : [Measure Name] := SumX(refTable, refTable[Fiel1] * refTable[Fiel2]  )

  * Example : ExSumX = SumX( SalesDetail, SalesDetail[Quantity] * SalesDetail[Unit Price] ) 
              The measure is created in [Sales Header] table ref [Sales Details] table,  
              Here  we need to understand the DAX works based on relationship 
              which means the measure will return based on [Order Number] field.

  * Applicable for AverageX, CountAX, CountX, MaxX, MinX, SumX, ProductX             

* Calculated Column - A measure is evaluated in the context of the cell evaluated in a report or in a DAX query, whereas a calculated column is computed at the row level

  * Once measure is created, We cannot use that measure in calculated column.
  * Instead use the measure while creating calculated column as below:
    * column = 
      VAR measure = measure formula
      RETURN column formula

  * In our example, we can create SalesHeader[Total Amout] = sumx( RELATEDTABLE(SalesDetail), SalesDetail[Quantity] * SalesDetail[Unit Price]) 
  * And Find the Discount Percentage using existing Discount per bill ; DiscountPct = DIVIDE ( SalesHeader[TotalDiscount] , SalesHeader[Total Amount])
  * Finally find the discount for each product in [Sales Details] --> Discount = SalesDetail[Quantity] * SalesDetail[Unit Price] * RELATED(SalesHeader[DiscountPct])
