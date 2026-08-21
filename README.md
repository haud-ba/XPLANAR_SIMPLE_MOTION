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
 - Use bCycleReset to get to defined state, if movers are in range (75mm) of one of the three positions the movers are enabled.
 - Use bCycleStart to activate the MC movement.
 - Use bCyclePause to move a mover iteratively to Positions[1]
 - If a mover is in standstill at a position you can activate the ext setpoint generator and run the g-code file
 
 
 - After G-code executes, send E_MOVER_CTRL.MOVER_EXT_STOP and the mover moves back to the initial position.
 - executing E_MOVER_CTRL.MOVER_EXT_STOP is vital to continue with the demo.
### ----------------------------------------------------------------------------------------------------------------
 - XPLN_MC_NCI project
 - MC function blocks only
 - a mover moves always in X and Y (during transport movement)

 - the cyclic wrapper extends the base class and adds the external setpoint connection

 - *MAIN._bCycleStart:* activates movement of both movers to the 3 positions
 - *MAIN._bCyclePause:* when active the sequence is halted after one mover did its movement.
 - *MAIN._bCycleReset:* quits errors on movers and searches for them in a 75mm range around one of the three positions

 - Positions[1] is intended where the activation of the extern setpoint generator may be started.
    - If mover is at Positions[1] you can start commanding the mover to activate the setpoint generator from the NCI
 - How to get the mover in ext setpoint mode:
    - use the following E_MOVER_CTRL in sequence:   
      - MOVER_EXT_ENABLE_AXIS, 
      - MOVER_EXT_SET_POSITION, 
      - MOVER_EXT_START
 - then make the NCI ready (this you have to do in the IDE), BuildGroup, set channel override, load GST_TEST_LONG.nc into the Interpreter, start the Interpreter

 - the NCI is used by hand, so setting the 3D Group, Loading the *.nc file is done manually in the IDE
      - go to "Group 4/3D-Online" set the axis assignement
      - go to "Channel 2/Override" set the axis override to 100%
      - go to "G0 Interpreter/Editor" load GST_TEST_LONG.nc into the NCI
 

### ---------------------------------------------------------------------------------------------------------------
   - NOTE: no recovery programmed, so if you remove a mover from the table, 
           you have to do the redetection of the movers manually in the XPlanarProcessingUnit
### --------------------------------------------------------------------------------------------------------------

