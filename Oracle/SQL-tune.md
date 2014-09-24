## DBMS_XPLAN ##

Found at [Kerry Osborne Blog](http://kerryosborne.oracle-guy.com/2010/02/gather_plan_statistics/):

*Starts column is the actual number of times the operation was executed,
not the number of times that the optimizer thinks it will be executed.*

*The A-Rows are cumulative while the E-Rows are not.
You have to multiply the E-Row by Starts (or divide A-Rows by the number of executions)
in order to compare apples to apples.*

