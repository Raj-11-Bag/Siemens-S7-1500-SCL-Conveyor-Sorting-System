# State Machine Diagram — FB_ConveyorZone

```
                    ┌─────────────────┐
           ─────►  │   STATE 0: IDLE  │ ◄──── Reset after fault
                    └────────┬────────┘
                             │ xEnable=TRUE
                             │ AND NOT xEmergencyStop
                             ▼
                    ┌─────────────────┐
                    │ STATE 1:RUNNING │
                    │  xMotorRun=TRUE │
                    └──┬──────────┬───┘
                       │          │
          rWeight>50kg │          │ xSensorExit=TRUE
                       ▼          ▼
             ┌──────────────┐  ┌──────────────────┐
             │ STATE 3:     │  │ STATE 2: STOPPING │
             │ FAULT        │  │ xMotorRun=FALSE   │
             │ xFault=TRUE  │  └────────┬──────────┘
             └──────────────┘           │ NOT xSensorExit
                                        ▼
                                   STATE 0: IDLE

        xEmergencyStop=TRUE (from ANY state)
                       │
                       ▼
             ┌──────────────────────┐
             │ STATE 4: E-STOP      │
             │ xMotorRun=FALSE      │
             │ xFault=TRUE          │
             │ Requires HW reset    │
             └──────────────────────┘
```
