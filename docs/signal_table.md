# Signal & Tag Reference

## FB_ConveyorZone — VAR_INPUT

| Signal | Type | Description |
|---|---|---|
| xEnable | BOOL | Zone enable command from HMI/PLC |
| xEmergencyStop | BOOL | Emergency stop — overrides all states |
| xSensorEntry | BOOL | Photoelectric sensor at zone entry |
| xSensorExit | BOOL | Photoelectric sensor at zone exit |
| rPackageWeight | REAL | Weight in kg from load cell |

## FB_ConveyorZone — VAR_OUTPUT

| Signal | Type | Description |
|---|---|---|
| xMotorRun | BOOL | Conveyor motor contactor output |
| xFault | BOOL | Fault indicator for HMI alarm |
| xZoneReady | BOOL | Zone available for next package |
| iCurrentState | INT | Current state number (0-4) |
| sFaultMessage | STRING | Diagnostic text for HMI display |

## State Machine Reference

| State | Value | Condition | Motor |
|---|---|---|---|
| IDLE | 0 | Zone waiting | OFF |
| RUNNING | 1 | Package in transit | ON |
| STOPPING | 2 | Package delivered | OFF |
| FAULT | 3 | Weight > 50kg or sensor error | OFF |
| EMERGENCY STOP | 4 | E-Stop actuated | OFF |

## Package_UDT Structure

| Field | Type | Description |
|---|---|---|
| PackageID | INT | Unique package identifier |
| Weight | REAL | Measured weight in kg |
| Destination | INT | Target lane (1=Sort, 2=Reject) |
| Timestamp | DATE_AND_TIME | Entry time into system |
| IsValid | BOOL | Package passed validation |
| FaultCode | INT | Error code if rejected |

## ProductBuffer_DB

| Variable | Type | Description |
|---|---|---|
| PackageBuffer | Array[0..9] of Package_UDT | 10-slot shift register tracking packages through conveyor zones |
