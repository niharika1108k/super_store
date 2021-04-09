# super_store
Author: Niharika Kwatra
/*import the dataset*/
proc import datafile="/home/u50469012/sasuser.v94/SampleSuperstore.xlsx" 
dbms=xlsx out=super_store replace;
run;
/*checking the output of imported dataset*/
proc contents data=super_store;
run;
/*to check for null values*/
proc means data=super_store nmiss;
run;
/*summary statistics*/
proc means data=super_store;
var Sales Quantity Discount Profit;
run;
/*Visualisation and checking for relation between variables*/
/*scatter plotting*/
proc sgscatter data=super_store;
plot Quantity*Sales;
run;
proc sgscatter data=super_store;
plot Region*Sales;
run;
proc sgscatter data=super_store;
plot Category*Sales;
run;
proc sgscatter data=super_store;
plot Segment*Sales;
run;
proc sgscatter data=super_store;
plot Region*Profit;
run;
proc sgscatter data=super_store;
plot Ship_mode*Profit;
run;
/*heat plot*/
proc sgplot data=super_store;
heatmap x=Sales y=Profit / nxbins=11 nybins=11;
run;
/*Histogram*/
proc univariate data=super_store;
histogram Sales Quantity Discount Profit;
run;
/*Bar graph*/
proc sgplot data=super_store;
vbar Ship_Mode;
proc sgplot data=super_store;
vbar Category;
proc sgplot data=super_store;
vbar Sub_Category;
proc sgplot data=super_store;
vbar City;
proc sgplot data=super_store;
vbar State;
run;
/*Stacked bar graph*/
proc sgplot data=super_store;
vbar Region /group = Profit;
run;
proc sgplot data=super_store;
vbar Segment /group = Profit;
run;
proc sgplot data=super_store;
vbar Sub_Category /group = Profit;
run;
proc sgplot data=super_store;
vbar Category /group = Sales;
run;
proc sgplot data=super_store;
vbar Ship_mode /group = Sales;
run;
/*checking for correlation*/
proc corr data=super_store plots = matrix ;
VAR Sales Profit Quantity Discount;
run;
/*Final summary:
   # It is the data set from US Superstore consisting of 49 states and 531 cities.
   # Total Sales=2297200.86, Total Quantity sold=37873, Total Profit=286397.0217
   # Max Sales & Profit: Region-West, Ship_mode-Standard Class, Category-Office Supplies, 
              Sub_Category-Paper, Segment-Consumer
   # Min Sales & Profit: Region-South, Ship_mode-Same Day, Category-Furniture, 
              Sub_Category-Bookcases & Machines, Segment-Home Office*/

/*Conclusion:
   # The correlation matrix shows positive relation between Sales & Quantity, Profit & Sales, 
     Quantity & Discount and Profit & Quantity.
   # It shows negative relation between Sales & Discount and Profit & Discount.*/
         
/*Solution to Problem Statement after EDA:
  The approach is to concentrate on areas where maximum profit is generated, keeping the quantity
  and discount in check as the relation suggests.
