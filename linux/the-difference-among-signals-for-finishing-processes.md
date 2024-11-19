# The Difference among Signals for Finishing Processes

> There are such signals as `SIGINT`, `SIGTERM`, `SIGKiLL` for finishing process.  
> Those have the same goal but has some difference.

## SIGINT
SIGINT is `INTerrupt SIGnal` sent to processes when you press `Ctrl+C`.
It returns to a new prompt line when the operation is interrupted by SIGINT.

## SIGTERM
SIGTERM is `TERMinate SIGnal`, which can terminate a process gracefully or not.  
It gives graceful clean-up time first, which length depends on the system setting, 
and after that period SIGKILL is sent to the remaining processes.
  
It is the default for `kill` command.

## SIGKILL
SIGKILL is `KILL SIGnal` that forcefully terminates processes.
  
Note that SIGINT and SIGTERM can be caught or ignored but SIGKILL can not.

* * *
These signals do all not create `core dump`.
