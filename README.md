# stratscript-language README

This is the StratScript extension that enables code autocomplete and syntax highlighting of 41103T's implementation of the StratScript for the Over Under Season


### 1.0.0

Initial release

# StratScript Documentation

The stratscript system itself is not a programming language but a framework for reading and interpreting code from an SD card, the functions and their subsequent actions that they complete are entirely customisable by the user. The following is 41103T's current implementation and use of the StratScript system for use in the 2023-24 Vex Over Under season.

## General Functions

### Defining a Strategy

> A strategy is defined by a `:` followed by a strategy name. The stratgey also takes 2 parameters, both a boolean type value (1 or 0). A strategy is then ended with the `end` keyword.
>
> #### Parameters
>
> `autoType` - Whether the strategy is for a game (0) or skills (1)\
> `useable` - This does not stop the strategy from being selected however if a value of 0 is selected a warning sign will appear no the screen notifying the user not to select this strategy
>
> #### Usage
> ```
> :Defense 0 0
>
> ...
>
> end
> ```
> This represents a strategy called "Defense", this is a strategy that would be used in a game and will not display a warning on the screen.

### ```repeat```
> The repeat function acts similar to a for loop, however the iterable varbiable cannot be accessed. It repeats the code from ```x```, lines above the function ```y``` number of times. It should be noted that ```repeat``` actions are not additive and not multiplicative.
> #### Parameters
> ```x``` - The number actions back from the repeat action to repeat\
> ```y``` - The number of times to repeat these actions
> #### Usage
> ```
> wait 500
> cataCycle
> repeat 2 5
>```
> This implementation of the ```repeat``` function repeats the 2 actions before the function call, 5 times, therefore it would run the ```wait 500``` and ```cataCycle``` actions 5 times.

### ```wait```
> This function defines an amount of time, in msec, the robot should delay before continuing with the next action.
> #### Parameters
> ```delay``` - The time to delay in msec
> #### Usage
> ```wait 500``` - This action instructs the robot to wait 500msec before moving onto the next action

## Driving
### ```goto```
> The ```goto``` function is used to tell the robot to move to a coordinate on the field (center of the field is (0,0)). This function **DOES NOT** contain functional pathfinding between points, so the route must be preprogrammed. This function is currently only able to drive the robot from the front, where the front of the robot is the intake side. The timeout parameter is used for goto commands that have a high likelihood of failure, such as asking the robot to goto a goal to score a triball, the robot my never reach the desired location so a timeout is necessary. This function has an accuracy of 10cm.
> #### Parameters
> ```x``` - The x coordinate of the desired coordinate\
> ```y``` - The y coordinate of the desired coordinate\
> ```timeout``` - **Optional** - The timout of the function in msec
> #### Usage
> ```goto 600 -750```

### ```turn```
> This tells the robot to turn to an absolute heading of the field, however this is determined by the team selected, e.g. If the team is red and the robot is instructed to turn to 0°, it will face north, however if the team is blue and 0° is targeted the robot will face nouth. This function has an accuracy of 2°.
> #### Parameters
> ```heading``` - The absolute heading for the robot to turn to in degrees
> #### Usage
> ```turn 45```

### ```reverse```
> This function does not have any parameters, only commanding the robot to drive backwards for 500msec. This function is used to back the robot out of goals after scoring a triball.

### ```cDrive```
> This function simply commands the robot to drive continuously forward. **This is not a blocking function**

### ```stop```
> Stops all drivetrain motors

### ```tDrive```
> This is a time based function that tells the robot to drive at a given speed for a given amount of time in msec. **The robot will brake after this time is up.**
> #### Parameters
> ```time``` - The time to drive for in msec\
> ```speed``` - the speed of the robot between -127 & 127
> ### Usage
> ```tDrive 500 127```

## Intake
### ```collect```
> The ```collect``` function lowers the intake turns on the intake motors and runs the motors until a triball is detected

### ```expel```
> This function raises the intake before spinning the intake backwards. **NOTE:** The intake will continue to spin until the ```stopIntake``` command.

### ```stopIntake```
> Stops all intake motors regardless of any previous functions.

### ```raise```
> Raises the intake to expose the pushing bar on the robot.

### ```lower```
> Lowers the intake.

## Catapult/Slapper
### ```cataCycle```
> ```cataCycle``` completes a series of moves, first it primes the arm before then waiting for a triball to be present for 250msec, before then advancing the motor and launching the arm.

### ```cataPrime```
> Pull the catapult back for traversal under the barrier, this is functionally the same as ```cataCycle``` without the wait for triball and colour.

### Deprecated - ```cataStart```
> Run the catpult motor forward. **This is a non-blocking function**

### Deprecated - ```cataStop```
> Stop the catapult motor