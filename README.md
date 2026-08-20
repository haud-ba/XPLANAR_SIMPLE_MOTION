# XPLANAR_SIMPLE_MOTION
Xplanar example project, shows basic MC functions and external setpoint generator
runs on a 2x3 APS4322 starter kit.
this example is MC only, tracks and collision avoidance are used in other examples.

## How To:
### startup project
 - Open and compile in XAE Shell
 - Use MAIN as first point of orientation
 - move your 2 APM4330 to positions 2 and 3.
 .
 - Use bCycleReset to get to defined state
 - Use bCycleStart to activate the demo.
 - Use bCyclePause to move a mover iteratively to Positions[1]
 .
 - Positions[1] is intended where the activation of the extern setpoint generator may be started.
 - If mover is at Positions[1] you can start commanding the mover to activate the setpoint generator from the NCI
 - How to get the mover in ext setpoint mode:
    - use the following E_MOVER_CTRL in sequence:   MOVER_EXT_ENABLE_AXIS, MOVER_EXT_SET_POSITION, MOVER_EXT_START
    - then make the NCI ready (this you have to do in the IDE), BuildGroup, set channel override, load GST_TEST_LONG.nc into the Interpreter, start the Interpreter
 .
 - After G-code executes, send E_MOVER_CTRL.MOVER_EXT_STOP and the mover moves back to the initial position.
 - executing E_MOVER_CTRL.MOVER_EXT_STOP is vital to continue with the demo.


