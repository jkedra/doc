## DBMS_XPLAN ##

Found at [Oracle Scratchpad](http://jonathanlewis.wordpress.com/2006/11/09/dbms_xplan-in-10g/)

> The best bit of this function shows up when you look at the script that generates it
> (`$ORACLE_HOME/rdbms/admin/dbmsxpln.sql`) when you decide to find out how to use the format parameter.

> You have to be a little careful comparing the actual and estimated row counts.
> They are not supposed to be the same in all cases. The estimated values are estimates
> for each execution of a rowsource, the actual values are the cumulative counts.
> So, for example, it is perfectly reasonable in line 5 to see E-rows = 15 and A-rows = 225,
> because line 5 starts 15 times: so 225 Actual rows = 15 starts * 15 estimated rows per start.

I was struggling with the following particular weirdo a long time
before I found the following hint:

> A couple of odd notes – you’ll see that I set serveroutput off.
> If serveroutput is on when you call this function, the last statement
> you will have run  will be the (hidden) call to dbms_output
> that follows your execution of any other statement –
> so you won’t get the plan and statistics.

Found at [Kerry Osborne Blog](http://kerryosborne.oracle-guy.com/2010/02/gather_plan_statistics/):

> Starts column is the actual number of times the operation was executed,
> not the number of times that the optimizer thinks it will be executed.

> **The A-Rows are cumulative while the E-Rows are not.**
> You have to multiply the E-Row by Starts (or divide A-Rows by the number of executions)
> in order to compare apples to apples.*

