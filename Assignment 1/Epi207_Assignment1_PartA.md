/*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*/
/*	Author: Tahmineh Romero*/
/*	Paper: Association between sarcopenia level and metabolic syndrome*/
/*	Su Hwan Kim, et, al*/
/*	Published: March 19, 2021*/
/*	https://doi.org/10.1371/journal.pone.0248856*/
/*	Data: https://doi.org/10.1371/journal.pone.0248856.s001*/
/*	purpose: Assignmet 1-PartA*/

/*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*/

libname A1 "C:\Users\tahminehromero\Box\Epi-PHD Course work\Winter2022\Epi207\Assignments\Epidem207-2022--winter\Assignment 1";


proc import datafile="C:\Users\tahminehromero\Box\Epi-PHD Course work\Winter2022\Epi207\Assignments\assignment1_data\journal.pone.0248856.s001.xlsx" dbms=xlsx out=dat replace;
run;

proc contents data=dat varnum;
run;
proc format;
value bmi_fmt
1="Underweight"
2="Normal"
3="Overweight"
4="Obesity";
run;

proc means data=dat mean;
class sex;
var Ht_m;
run;


data dat2;
set dat; 
if 0< bexam_BMI<18.5 then BMI_cat_tr=1;else
if 18.5=< bexam_BMI=<22.9 then BMI_cat_tr=2;else
if 23< bexam_BMI=<24.9 then BMI_cat_tr=3;else
if 25=< bexam_BMI then BMI_cat_tr=4;
format BMI_cat_tr bmi_fmt.;

run;
