Team 2337 2012 Rebound Rumble Code

For the first time, Team 2337 is open-sourcing our competition code for 2012. Any comments and questions are welcome.

For more information on the robot and performance: http://www.team2337.com/robots.html
The robot CAD can be found on FRC-Designs: http://www.frc-designs.com/html/CAD_2012.html

A quick robot overview:
-----------

* A 4CIM, 8WD dual-speed drivetrain using pneumatic tires designed to minimize chain use
* Two KOP-wheel shooter, fixed hood, no turret. Powered by two Banebot 550s through a Cimulator gearbox.
* A 33 and 148-inspired 'dingus', large pneumatic cylinder, used successfully for triple and co-op balances
* Bridge manipulator and external intake with CD7-related design, pneumatically powered, with throttle motors to direct the ball side to side
* Intake and ball containment system designed to hold just three balls, powered by two AndyMarks and a Fisher Price


A code overview
-----------

* An **autonomous** that reads scripts (with its own language) placed via FTP on the cRIO.
	-There is an overarching structure that manages commands based on their parameters outlined in the script
	-Possible autonomous functions reference already written code in Periodic Tasks.vi
	-An autonomous script is selected by the driver controller while the robot is disabled
* All logic is contained inside the **Periodic Tasks.vi**, with control data passed to Periodic Tasks via local variables
	-This means all code is consistently executed (no depending on DS packets affecting how fast commands are updated)
	-Teleop.vi is used to assign joystick commands into robot commands, each with its own local variable
	-Autonomous scripts reference these robot commands
* **Simple** shooter speed control
	-A proximity sensor is mounted to detect one rising edge per revolution of the shooter wheel, managed by the WPI Counter class
	-A well-tuned PI loop, with quick ramping up to speed and precision of +/- 5 RPM at normal key shooting speeds
* A **basic vision** program mostly copied from the Rectangular Target Processing example
	-'Auto-targeting' program moves wheels to line up robot with target
	-Auto-targeting is still not well-tuned, not very functional
	-A very low camera exposure is used to limit the amount of possible colors interfering with the mask
* **'Cheesy drive'** - a form of arcade drive - provided by FRC 33 (which was based on work done by FRC 254)
	-First year of non-mechanum, non-Lunacy wheel drive for 2337
	-Custom ramping on the joystick input to reduce quick, potentially hazardous movements
*An **intake logic** system used to suck balls in one at a time, and queue balls out one at a time
	-Three eye sensors indicate whether balls are in their appropriate positions

As an offseason project, the 'brogrammming' team is also working on a Java port of our code. When finished, it will also be open-sourced.