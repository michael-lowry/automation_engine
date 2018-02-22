[UC4.GET_OBJ_SUBTYPE.VARA_SEC_SQLI](https://github.com/michael-lowry/automation_engine/blob/master/UC4.GET_OBJ_SUBTYPE.VARA_SEC_SQLI.xml) can be used to look up the subtype of the currently-executing task.

#### SQL query ####
```sql
select OH_HostAttrTypeDst
from OH
where OH_OType = ?
and OH_Name = ?
```

#### Bind parameters ####
1. &$OBJECT_TYPE#
2. &$NAME#

#### Example ####
~~~~
:PRINT "Object name    : &$NAME#"
:PRINT "Object type    : &$OBJECT_TYPE#"
:SET &OBJ_SUBTYPE# = GET_VAR(UC4.GET_OBJ_SUBTYPE.VARA_SEC_SQLI)
:PRINT "Object subtype : &OBJ_SUBTYPE#"
~~~~

#### Sample output ####
~~~~
U00020408 Object name    : UC4.GP_SQL.JOBS
U00020408 Object type    : JOBS
U00020408 Object subtype : SQL
~~~~
