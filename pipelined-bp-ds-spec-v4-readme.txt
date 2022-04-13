1.) Want concurrent execution on different functional units.
2.) Need to bypass results to both ROB and the correspnding reservation station
3.) WB microinstructions dont execute in the EX phase, and they get broadcasted back to the EX phase in the WB phase

Microinstructions

- multiple operand loads possible (as many as there are data read ports)
- multiple EX phase instructions, corresponding to different outputs
- multiple write backs possible (as many as there are data write ports)


Structural Hazards

- in ID phase, if in the EX phase there is a reservation station broadcasting with the same address as in the ID phase.
- in the ID phase, if the WB phase is writing to memory or broadcasting to EX phase with the same address
  as in the ID phase.
- in the ID phase, if the WB phase is changing an alias that corresponds to the one to be used in the ID phase

Note 1 : the WB phase microinstructions dont execute in the EX phase, and when they are scheduled to WB there won't be any 
	   structural hazards with the EX phase.
Note 2 : the structural hazards between the ID and WB phass, specifically those associated with alias hardware, can be mitigated by
	   checking to see if the addresses match, as the alias value used on the alias hardware bus in the WB stage corresponds to 
	   the address - might lose some cycles though as the alias might not be the current one.
Note 3 : the structural hazards between the EX phase and the ID phase can be mitigated by checking to see if the addresses match,
	   however because number of funcitonal units should be decoupled from the design and because we can't guess which will be
	   chosen by the arbitration hardware, need an extra conditions test for each functional unit. Last, since we don't know which
	   step in the EX phase will execute, we stop the entire EX phase when a hazard is detected - this will cost some clock cycles.


