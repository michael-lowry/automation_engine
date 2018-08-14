[UC4.GET_AGENTGROUP_MODE.VARA_SEC_SQLI](https://github.com/michael-lowry/automation_engine/blob/master/UC4.GET_AGENTGROUP_MODE.VARA_SEC_SQLI.xml) can be used to look up the mode of an agent group.

#### SQL query ####
```sql
select OHG_Mode
from OH left join OHG
on OH_Idnr = OHG_OH_Idnr
where OH_Name = ?
```

#### Bind parameters ####
1. &AGENTGROUP#

#### Example ####
~~~~
:PRINT "&AGENT_OR_AGENTGROUP# is an agent group. Checking AG mode..."
:SET &AG_Mode# = GET_VAR(UC4.GET_AGENTGROUP_MODE.VARA_SEC_SQLI)
:SWITCH &AG_Mode#
:CASE 'A'
:  SET &AG_Mode_Desc# = "any"
:CASE 'F'
:  SET &AG_Mode_Desc# = "first"
:CASE 'N'
:  SET &AG_Mode_Desc# = "next"
:CASE 'L'
:  SET &AG_Mode_Desc# = "load dependent"
:CASE 'X'
:  SET &AG_Mode_Desc# = "all"
:ENDSWITCH
:PRINT "&AGENTGROUP# mode is '&AG_Mode_Desc#' (&AG_Mode#)."
~~~~

#### Sample output ####
~~~~
U00020408 AE_NODES_BOTH is an agent group. Checking AG mode...
U00020408 AE_NODES_BOTH mode is 'all' (X).
~~~~
