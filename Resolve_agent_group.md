This JOBI can be used to perform dynamic resolution of agent groups. It is useful in situations where one cannot determine ahead of time whether an agent or agent group will be used. 

#### Overview ####
1. Set the variable `&AGENT_OR_AGENTGROUP#` to the name of an agent or agent group.
2. Run `UC4.RESOLVE_AGENT_GROUP.JOBI` using the `:INCLUDE` command.
3. Agent group resolution is performed (if necessary) as follows:
   * If `&AGENT_OR_AGENTGROUP#` is set to the name of an agent, no resolution is necessary
   * If `&AGENT_OR_AGENTGROUP#` is set to the name of an agent group, this agent group will be resolved to an agent.
 5. A test is performed to make sure the agent is up. (Additional variables can be set to control error handling.)
 6. The result (an agent name) is passed in the `&AGENT#` variable.

To use the JOBI, just include a few lines in the pre-process tab of the job (or the process tab of the parent workflow).

#### Example 1. Pre-process tab of OS job ####
~~~~
:SET &AGENT_OR_AGENTGROUP# = "WINSRV1"
:INCLUDE UC4.RESOLVE_AGENT_GROUP.JOBI
:PUT_ATT HOST = &AGENT#
~~~~

#### Example 2. Pre-process tab of file transfer job ####
~~~~
:SET &AGENT_OR_AGENTGROUP# = "WINSRV1"
:INCLUDE UC4.RESOLVE_AGENT_GROUP.JOBI
:PUT_ATT FT_SRC_HOST = &AGENT#
:SET &AGENT_OR_AGENTGROUP# = "UNIXSRV1"
:INCLUDE UC4.RESOLVE_AGENT_GROUP.JOBI
:PUT_ATT FT_DST_HOST = &AGENT#
~~~~

#### Example 3. Pre-process tab of OS job, with error handling ####
By setting some adidtional variables, handling of errors (e.g., no agent up) can be controlled. In this example, the job will be marked ENDED_SKIPPED, and the post-processing of the job will be executed even though the job did not run.
~~~~
:SET &AGENT_OR_AGENTGROUP# = "WINSRV1"
:SET &Run_PostProc_on_Error# = "YES"
:SET &Stop_on_Error# = "NO"
:SET &Stop_Message_Num# = 0
:INCLUDE UC4.RESOLVE_AGENT_GROUP.JOBI
:PUT_ATT HOST = &AGENT#
~~~~
