# Progression Test Videos

### -Lift Test:

https://user-images.githubusercontent.com/123998872/267706675-971f4d4e-ddfd-44a7-a783-cec726250a8b.mp4

### -Thrust + Obstacle Test:

https://user-images.githubusercontent.com/123998872/267707213-ec5f5f01-9190-4c4c-82a1-2882a500f8a7.mp4

### -Sensors + Turn Test


# Team members
<details open>
<summary></summary>

| Peter Kirill Granitski|
|-----------------|
| Ammar Sathar|
| Joshua Lafleur|
| Olivia Barbieri|
| Camille Granade|
| Lifu Zhang |

</details >

# 1. Abstract
This report serves to detail the development of an autonomous hovercraft (HC) with the objective of completing a designated track, provided by the ENGR 290 course competition rules [1]. It is based on the team’s initial design which was analyzed, modified, constructed and tested. This report will discuss the different requirements and design choices that have been adapted based on the previously submitted Preliminary Design Report [2], input from course supervisors, as well as trial-and-error research conducted by the team. This report also contains progress reports of the design process and the schedule followed to complete the project.

# 2. Document Purpose
The purpose of this document is to detail the process of our hovercraft design, design analysis, and implementation. This document outlines our mission objectives, goals, and serves as a justification for our choice of hovercraft design. 

### Document Scope
The general scope of this document includes the project’s goals, deliverables, acceptance criteria, and limitations. Briefly;

**Goals**: Design and construct an autonomous hovercraft that will complete a track given by the professor.

**Deliverables**: A thorough report detailing the entire autonomous hovercraft design and construction process.

**Acceptance Criteria**: The hovercraft must complete the given track in under 2 minutes while traversing three barriers measuring 1mm, 2mm, and 3mm respectively. There is a maximum of 3 attempts to complete the track.

**Limitations**: Teams are limited to using materials provided by Concordia University, which are listed in the ENGR 290 Tools, Hardware, and Materials Loan Agreement [3] and additionally in the Final Design Materials Request Form [4]. 

# 3. Mission Objectives
The mission of this project is to design an autonomous hovercraft that can successfully complete a track provided by our Professor as part of a competition. While completing the track, the hovercraft must pass over increasingly high barriers on the ground of 1mm, 2mm, and 3mm, respectively. In addition to completing the track, we must also aim to construct our hovercraft with the least amount of components possible in order to score higher in the competition.

### 3.1 Design Goals
This design aims to complete the given track in the shortest amount of time possible using 3 fans. Two of the fans used will be used to provide thrust and the third fan will be used to create lift. The use of 3 fans simplifies the design process slightly as the two thrust fans allow for a much simpler software implementation for steering, i.e. all that is needed is to control the difference in thrust levels between the two thrust fans.

By separating the implementation of the lift and thrust systems, additional lift can be generated to hover over the obstacles that the hovercraft will encounter in the track without increasing the forward speed of the hovercraft. Similarly, additional thrust can be produced to navigate corners without decreasing lift.

### 3.2 Technical Goals
The first technical goal our hovercraft aims to achieve is to lift 3mm from the baseboard to the ground, not including the height needed to maintain a smooth level of moving on an indoor ground. This can be achieved through the use of a  bottom that can generate a momentum curtain.

Secondly, the hovercraft must be autonomously maneuverable. In order to accomplish this, some core components are required. For example, an ultrasonic sensor (US), LIPO batteries, several fans, among others. In order to achieve autonomy, code must be created to support the autonomous function of the previously mentioned components.
 	
The third technical goal our hovercraft must accomplish is to finish the track in under 2 minutes. The track provided by the course administrators consists of four parallel straight segments. While completing the straight segment of the track, the craft shell of the hovercraft begins to accelerate at close to 100% of its propeller power. Before it approaches where a turn must be executed, about 55 to 60 cm from the front wall of the track, the hovercraft must decrease its velocity in order to prepare to brake at the ideal spot before executing the turn function. 

Regarding the objectives mentioned earlier, the team must install a minimum of two fans for each design, namely, a lift fan and a thrust fan. As the track includes walls, each design must be equipped with at least one sensor to detect them and navigate its way to the finish line. The sensor will determine the distance between the hovercraft and the surrounding walls. Depending on the design, the sensor must collect and transmit this information to the controller to ensure that the hovercraft takes the appropriate turn.

The hovercraft must independently complete the track within two minutes. Each team will only have three attempts during the competition. The track consists of three obstacles with varying heights between 1mm to 3mm. The track is 235 cm in length and has a width ranging from 50 to 55 cm, with a wall height of 15 cm.

The formula used to evaluate each design is d/(Nc x t), where d represents the distance covered, Nc denotes the number of components used, and t indicates the time taken by the hovercraft to complete the track. A higher score indicates a more efficient design, with a focus on using fewer components and less time to complete the track, setting it apart from other designs.

# 4. Hovercraft Design
The basis of our team’s hovercraft design stems from one of the three potential designs in the PDR. We decided to construct the second proposed design- the intermediate approach. This design originally consisted of a lift fan and a thrust fan controlled by a servo motor. After trial and error, it was decided that it was optimal to replace the servo motor with a second thrust fan. 


| Figure 1: Design Idea 2 Intermediate Approach   |
|---------------|
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://i.imgur.com/Pufgu2k.png">
  <source media="(prefers-color-scheme: light)" srcset="https://i.imgur.com/Pufgu2k.png">
  <img alt="Figure 1: Design Idea 2 Intermediate Approach " src="https://i.imgur.com/Pufgu2k.png">
</picture>  

### 4.1 Principles of Operation
The hovercraft consists of four main parts: the sensor system, the lift system, the thrust system and the mechanical system. The design of the hovercraft stems from a rectangular base with a lift fan placed in the center and a fully flexible skirt attached to the base. To produce thrust, two fans are attached perpendicular to the base, enabling fast movement as well as easy and efficient turning, which are guided through the use of forward distance measurements by the US sensor.



| Figure 2: Different views of the final solution   |
|---------------|
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://i.imgur.com/qaTcyKq.png">
  <source media="(prefers-color-scheme: light)" srcset="https://i.imgur.com/qaTcyKq.png">
  <img alt="Figure 1: Design Idea 2 Intermediate Approach " src="https://i.imgur.com/qaTcyKq.png">
</picture>  

### 4.2 Electrical and Sensor System Design
Our hovercraft’s sensor design comprises of two sensors, an ultrasonic sensor (US) and an infrared sensor (IR sensor). Both sensors function independently from one another. The ultrasonic sensor is used to determine how far a barrier is perpendicular to the trajectory of the hovercraft. The US has a very high polling frequency, meaning that we receive measurement reading very frequently (5-10 Hz). The US continues to measure how far the hovercraft is from a barrier continuously unless it is in the process of completing a turn. When the US reads that the hovercraft is about 55-60 cm away from an upcoming barrier, the hovercraft begins to turn by rotating forward in a budging manner instead of continuously rotating. 

The IR sensor is used in the turning process. It is placed perpendicular to the US on the body of the hovercraft. The IR sensor is used to judge how far from a parallel boundary the hovercraft is. It is essential that the IR sensor is able to detect an upcoming turn as quickly as possible to ensure that the hovercraft has enough space to complete the turn without colliding with a barrier. Therefore, the budging motion prevents the hovercraft from moving too far past the middle barrier of the track. This allows the hovercraft to stop at the necessary point, about 5-10 cm past the middle boundary, to start the turn and not hit the wall. 

### 4.3 Lift Design 


| Figure 3: Air flow diagram   |
|---------------|
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://i.imgur.com/ww2UBFW.png">
  <source media="(prefers-color-scheme: light)" srcset="https://i.imgur.com/ww2UBFW.png">
  <img alt="Figure 1: Design Idea 2 Intermediate Approach " src="https://i.imgur.com/ww2UBFW.png">
</picture>  

The lift system in our hovercraft consists of a lift fan which is placed in the center of our craft. 
The primary benefit of this design is that it ensures an even and continuous airflow under the hovercraft as well as even air pressure underneath the hovercraft. When the lifting fan is on, it creates higher air pressure than atmospheric pressure to allow the skirt to keep its shape, enabling the hovercraft to lift successfully.

Due to both competition requirements and our own calculations, only one lift fan is necessary in our design. Due to the principle of center of mass, the lift fan is placed in the center of our hovercraft.

The base of the hovercraft is a short rectangle, meaning that the length is only slightly longer than the width. In accordance with the shape of the base, the plenum was also designed as a rectangle as shown in the figure below. The surrounding holes on the skirt allow for air to flow evenly throughout the skirt. The combination of these design choices enable the skirt to properly inflate and hover.



| Figure 4: Lift fan placement  |
|---------------|
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://i.imgur.com/bHTbF0u.jpg">
  <source media="(prefers-color-scheme: light)" srcset="https://i.imgur.com/bHTbF0u.jpg">
  <img alt="Figure 4: Lift fan placement " src="https://i.imgur.com/bHTbF0u.jpg">
</picture>  

Through experimentation, our team decided that plastic taken from a garbage bag was best to construct the skirt. Four plastic sheets of the same dimensions were placed around the base hovercraft and fixed to the base with adhesive tape. This design  ensures uniform air pressure around the hovercraft and allows us to maintain a balanced altitude. Uniform sheets of plastic and tape fixation patterns at each of the four corners of the hovercraft reduces the unpredictable airflow caused by the hole in the skirt.

The components of our hovercraft, such as the sensor, battery, and fans, are not symmetrically placed on the square base. Our hovercraft is not an evenly weighted design due to the weight and location of each sensor, battery, and fan. Thus, the weight of the front and the rear of the hovercraft is heavier relative to the sides. According to our calculations, it was found that a hole in the skirt of size 13 by 20 cm is optimal.

Initially, holes in the skirt weren’t put in the skirt. The friction between the hovercraft and the ground was too high, which prevented the hovercraft from moving. After several trial and errors, as well as calculations, we found that a 13 by 20 cm hole can make the hovercraft float on the ground. The pressure flowing from the hole will not cause the hovercraft to lift too high, allowing us to accurately control the speed.

### 4.4 Propulsion Design

| Figure 5: Top view of the hovercraft  |
|---------------|
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://i.imgur.com/oRk8LjO.jpg">
  <source media="(prefers-color-scheme: light)" srcset="https://i.imgur.com/oRk8LjO.jpg">
  <img alt="Figure 5: Top view of the hovercraft " src="https://i.imgur.com/oRk8LjO.jpg">
</picture>  

One of the main adaptations we made to our initial hovercraft design was opting to use three fans instead of two fans and a servo motor. Through the use of three fans, the motion of the hovercraft is able to be controlled using skid steering. Essentially, skid steering functions by controlling the amount of power supplied to each of the two thrust fans. For example, when the hovercraft needs to complete a right turn, the power supplied to the left thrust fan will increase and the power supplied to the right fan will decrease until the turn has been completed.

There are several factors that were considered when deciding to modify our original design, however, in the end we decided to change our design based on several implementation advantages. Firstly, by avoiding the use of a servo motor, the code associated with the hovercraft’s movement is simpler to develop as only the amount of power supplied to each fan must be controlled. Additionally, it would have been more mechanically challenging to connect the servo motor to the hovercraft as a piece would have needed to be 3-D printed. The last factor that solidified the decision to use three fans was that both the initial and modified thrust fan designs use the same number of components, so there is no deduction in the competition associated with additional pieces.

### 4.5 Mechanical and Structure Design
The fans, sensors and batteries of the hovercraft are provided by the school, which simplifies the design of our selection of mechanical parts, but at the same time increases the difficulty. Due to the limitations of the mechanical design part, we need to constantly change the design and optimize the programming part.

With regard to the design of the lift fan, after continuous testing, we found that when the lift fan is at 94%, the hovercraft is at an appropriate height and saves battery power even more.

The fan design regarding the adjustment direction was the most difficult part of our project. We have proposed many solutions, but after continuous design, we finally decided to use the fan on one side at 100%, and the other side at 1% (close to 0). For example, when the hovercraft needs to turn right, the fan on the left side of the hoverbed is at 100%, and the fan on the right is at 0%. The advantage of this design is that the hovercraft can turn in a smaller distance.

When the hovercraft is moving forward, our thrust fan design is relatively simple, but at the same time it also encounters difficulties in actual experiments. We need to cover all the distances in under two minutes, so we set the fans in both directions to 100%. The difficulty we encountered when the hovercraft is moving forward quickly is that although the ultrasonic sensor located in front of the hovercraft has tested the front wall and stopped the hovercraft, due to the inertial force, the hovercraft will move forward for a certain distance, resulting in the required turning distance. too small. After continuous testing and improvement, we finally found that when the front is 100 cm away from the wall, the thrust fan stops working and the hovercraft will be in the position we need. At the same time, because we wanted the hovercraft to change direction correctly, we placed the infrared sensor on the side of the hovercraft. Because of the characteristic curve of the infrared sensor and the distance from the wall during the test, we set the infrared sensor to stop and change direction when it senses that the distance from the wall is 35cm.

https://i.imgur.com/5EEtucx.png

| Figure 6: Updated hovercraft layout |
|---------------|
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://i.imgur.com/5EEtucx.png">
  <source media="(prefers-color-scheme: light)" srcset="https://i.imgur.com/5EEtucx.png">
  <img alt="Figure 5: Top view of the hovercraft " src="https://i.imgur.com/5EEtucx.png">
</picture> 

| Figure 7: Top view of hovercraft |
|---------------|
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="http://imglin.com/ZZAhn7mHLe.png">
  <source media="(prefers-color-scheme: light)" srcset="http://imglin.com/ZZAhn7mHLe.png">
  <img alt="Figure 5: Top view of the hovercraft " src="http://imglin.com/ZZAhn7mHLe.png">
</picture>   

The structure of the hovercraft is the most important aspect of construction, all the design choices and code are based on the structure of the hovercraft. All the parts of the hovercraft are located on his body, and the shape of the body will directly change all our steps and designs, and will affect the final result.

We did a lot of research and discussion when choosing the body shape of the hovercraft, and finally we settled on a rectangular shape as the main body. The advantage of this design is that we can cut it more easily to get a rectangle. The advantage over a square shape is that the shorter body facilitates smoother turns. Then, after several experiments, we decided to use a lift fan and two propulsion fans, as presented earlier. In the first few experiments, we found that when the hovercraft was raised, it would find the deflection of direction and roll over. After investigation, we found that the lack of plenum was the cause of this problem. We re-determined the design and added plenum to achieve the balance of hovercraft operation.

Finally, based on battery considerations, we need to reduce the weight as much as possible without compromising the integrity of our design. However, after many improvements, the size has been reduced and the number of connecting parts has been reduced, and therefore the weight has been reduced. Thanks to this reduction in weight, the running speed of the hovercraft has been increased, and the excellent design of the structure allows our hovercraft to complete all the journeys more quickly.

### 4.6 Analysis of Design
Compared to the initial designs in the PDR, we have, for weighted objectives table (WOT) analysis:

| Table 1: WOT Table |
|---------------|
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://i.imgur.com/NVTqhoL.png">
  <source media="(prefers-color-scheme: light)" srcset="https://i.imgur.com/NVTqhoL.png">
  <img alt="Table 1: WOT Table " src="https://i.imgur.com/NVTqhoL.png">
</picture>   

### 4.7 Matlab Simulation

| Figure 8: Simulation of linear values vs time in MATLAB |
|---------------|
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://i.imgur.com/jsgoKyz.png">
  <source media="(prefers-color-scheme: light)" srcset="https://i.imgur.com/jsgoKyz.png">
  <img alt="Table 1: WOT Table " src="https://i.imgur.com/jsgoKyz.png">
</picture>   

Utilizing formulas provided by the Professor and the MATLAB software, we simulated our hovercraft to estimate the speed and time in which our hovercraft will complete the track. This simulation resulted in a time completion of around 15 seconds should the track be a straight line. However, as the actual track requires the hovercraft to turn, the hovercraft itself will not travel continuously at its maximum speed. Thus, the hovercraft will take significantly longer to complete the track in actuality.

| Figure 9: A 3-D CAD example of a possible final design |
|---------------|
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="http://imglin.com/sO71D7xv6G.png">
  <source media="(prefers-color-scheme: light)" srcset="http://imglin.com/sO71D7xv6G.png">
  <img alt="Figure 9: A 3-D CAD example of a possible final design " src="http://imglin.com/sO71D7xv6G.png">
</picture>   

# 6.0 Hovercraft Construction Plan

Our team decided to construct the hovercraft using various stages of implementation. After drawing up 3 mock designs, we selected the best one using different analysis tools such as SWOT, WOT and AHP. From there, the design was modified after various testing and calculations. The design was then constructed in several stages, including; construction of the electrical system, construction of the mechanical base, and development of the supporting code.

###6.1 Hardware Collection and Testing

The hovercraft system relies on hardware to enable the software to operate, making it a crucial component. The Department of ECE provided the hardware required to construct the hovercraft. These components included batteries, fans, capacitors, and sensors, more specifically the IMU breakout board, ultrasonic sensor, and infrared range sensor. To test the hardware, two technical workshops were conducted. The first workshop focused on testing the ultrasonic and infrared sensors, while the second workshop tested the IMU and servo motor to ensure the components were functioning properly and operational.
### 6.2 Integration, Implementation and Construction

Using the preliminary class assignments and the PDR, we began to develop the hovercraft. Through the use of various components, we began building the hovercraft in an iterative manner. Using repeated testing of the plenum and sensors, we designed the hovercraft efficiently.

### 6.3 Testing

The first development in the testing process occurred during the first workshop. The functionality of the ultrasonic and infrared sensors were tested by connecting them to the controller and taking different readings. To ensure that the sensors were functioning properly, three trials were conducted. The average values were calculated by dividing the distance read by the sensor by the ADC value. The next development in the testing process occurred during the second workshop, where the IMU and servo motor were connected to the controller to ensure that the servo-motor's arm was able to replicate the IMU yaw.

After spending a week in the lab, the chosen design was constructed and tested to determine if the hovercraft could lift itself. Minor adjustments were made to achieve the correct weight distribution. The team then worked on the coding aspect of the project by writing code for each component and combining them into one file after verifying that there were no syntax errors. The correct assignment of pins to ports and proper sensor functionality was then verified.

The most critical aspect of the project was the algorithm, which makes the hovercraft autonomous by checking sensor values and adjusting the hovercraft's position accordingly. Testing the code is essential, so the hovercraft was tested on the laboratory's test track to ensure that the algorithm worked correctly and that the hovercraft performed as intended.

# 7.0 Mission Operations

The mission operations of our hovercraft must fulfill in order for it to complete the requirements outlined in section 7.1 Competition Req. and Operations, include a working mechanical and electrical system, as well as a functioning code. The mechanical and electrical systems and the code work together to support the function of an autonomous hovercraft.

### 7.1 Competition Req. and Operations

As specified by the the ENGR 290 H/C Competition Rule [4], the four main objectives of the hovercraft competition are to:

1. Complete as much of the given track as possible autonomously. Track is shown in Figure 9.
2. Traverse three obstacles in the track measure 1, 2, and 3 mm respectively.
3. Complete the course in as little time as possible, with the maximum amount of time permitted to complete the track being 2 minutes.
4. Complete these requirements using as few mechanical and electrical parts as possible.

| Fig 10: The given track the hovercraft must complete |
|---------------|
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="http://imglin.com/Qx4Y0OscFG.png">
  <source media="(prefers-color-scheme: light)" srcset="http://imglin.com/Qx4Y0OscFG.png">
  <img alt="Fig 10: The given track the hovercraft must complete " src="http://imglin.com/Qx4Y0OscFG.png">
</picture>   

The distance of the straightway segment, x, is 235 cm. The track width, y, is between 50 and 55 cm, and the wall height, z, is 15 cm.

The score each hovercraft will receive in the competition is based on the following formula: 
**d<sub>**completed**</sub>  /(N<sub>**c**</sub> t<sub>**course**</sub>)**

Where:

- **d<sub>**completed**</sub>**  is the distance of the track completed autonomously by the hovercraft
- **N<sub>**c**</sub>**   is the number of components used (IMU not included)
- **t<sub>**course**</sub>** is the time (in seconds) to complete the track successfully 

# 8.0 Project Management

The prerequisite for successful teamwork is the communication among members and the completion of the schedule in accordance with the steps. We schedule weekly meetings before and after class to update each other on ideas and weekly progress, and to ask questions and discuss solutions to problems. We will also communicate through discord and communicate with each other at any time. In the first meeting, we decided on the leader of the team and got to know each other and the members of the team. In the following meeting, 3 designs were determined based on this, and the advantages and disadvantages of each design were determined through a large number of investigations and matlab analysis. Finally we settled on our plan. Start conducting investigations and writing reports. Finally, when the deadline was approaching, we held daily meetings and researched and experimented with our hovercraft, constantly improving our hovercraft design and coding. At the same time, the people not working on the hovercraft wrote the report.

### 8.1 Meeting Minutes

<details>
<summary>Monday April 10th, 2023</summary>

Present: Ammar, Peter

- Cut out foam board into square, with circular hole in the middle
- Hot glue the lift fan onto the surface
- Start thinking/discussing about ideas for skirt and other things
- Charge batteries
- Call it a day

</details >

<details>
<summary>Tuesday April 11th, 2023</summary>

Present: Ammar, Peter

- Implement skirt which based on [src]()
- Tested with lift fan at full thrust that skirt blows up (but not enough lift)

</details >

<details>
<summary>Wednesday April 12th, 2023</summary>

Present: Ammar, Peter

Present: Peter, Ammar, Josh, Shawn

- Plan out physical placement of sensors
- Cut holes in the bottom of the skirt to ensure there is actual lift (since there was too much friction)
- Test attaching and running thrust fans
- Running into problems where it doesn’t move forward
- Multiple different attempts to adjust the skirt until…
- IT WORKED!
- Marked specific placements of batteries and controller such that the forward mode actually goes forward with barely any drifting if any…
- Manages to surpass the test obstacles…
- We are gucci
- Write pseudocode skeleton code for navigation logic/control loops
- Reviewed with Ammar and Josh
- Seems like a good starting point
- Call it a day here,
- Got advice from victor
- One of our batteries is dead
- Get it replaced tomorrow at 4 pm as scheduled already for the meeting with christian
- Might have a loose connector on ground for one of the thrust fans so double check that too maybe?
- What do we aim for tomorrow?
- Report
- HC
- Go see christian at 4pm
- Replace a bloated battery?
- Did we overuse the batteries?
- We should probably be timing our usage so we keep track how long they are still good for..
- Other teams said they just kept using them till they died tho?
- Replace that one thrust fan for the one w/ loose GND wire?
- It seemed to be working fine for a while, did we inadvertently damage it due to poor handling?
- Forward drive mode regression test
- Left + right turn testing with IMU feedback

</details >


<details>
<summary>Thursday April 13th, 2023</summary>

Present: Ammar, Peter

- Present: peter, ammar, olivia, shawn, camille
- Each cell should be minimum 3V and max 4.2
- 12 - 16.8 V range
- After fully charging it was at 16.8 volts?
- Start building out turn left and right functions without sensors
- We seem to have regressed in terms of stable forward drive mode…
- Inconsistent results, needed to shift the batteries position and even then it wouldn’t drive forward too consistently
- But still sometimes?
- Created test sketch for getting USS values
- Final report started by everyone else

</details >

<details>
<summary>Friday April 14th, 2023</summary>

Present: Ammar, Peter, Shawn

1. Regression test forward drive
2. Place new components based on design change proposals
IR sensor in forward right corner facing right direction
Imu sensor (where???)
3. Retest forward drive with new weight displacement
Found that diagonal corners of skirt seem to blow more air therefore double checking leaks and shit over there

1. Program test mode where startLift() then turnRight() just to see how that works out the box on corners
2. Test again but for turnLeft()

1. Create test sketch for getting IMU values
2. Create test sketch for getting 
1. Test Ammar's new rudder idea
2. Possibly rebuild the skirt (because it’s been damaged due to wear and tear and testing stuff?)

Peter got all the 3D cad parts printed but at this point doesn’t look like we will use it afterall

</details >


<details>
<summary>Saturday April 15th, 2023</summary>
Present: Josh, Peter, Ammar
Josh

- Isolate working IMU code and commit single sketch
- Isolate working IR code and commit single sketch
- Put on hold while we test out new design where
- Integrate IMU pitch reading into thrust parameters adjustments for driveForward()
- 

Peter

- reCharge batteries
- Review working code from last night
- Test left run same way as right turn yesterday after stop
- Test toggle algorithm on whole track
- Test using IR to detect if turn left or right

- 2 AM recap
- Josh tried to get the IMU readings working but it didn’t pan out so we are not going to assume it will be ready for the project
- Peter tried to keep getting the HC to finish the track without IMU just with IR sensor and US. We got it working quite a few times but also lost consistency somewhere along the line. Part of the issue is that as the full charge (16.8V) depletes, the “100%” fan speed force goes down. So for example when we have a bit of an incline our HC struggles a lot more. So the simple solution is to keep the charge around 16-16.8V, try to run fans at max speeds and tailor the algorithms/threshold values to that
- We also got advice from someone that our HC size is so big it might get disqualified on the spot for not being able to possibly turn around on itself in the straight part of the track. So Ammar started building a new chassis/plenum/skirt. Didn’t actually start a new skirt because we were too tired at 2 AM so continue tomorrow.
- Peter will continue tomorrow to tweak the algorithms until it works
- Right now, when it does work, it seems to take too long on an uphill incline… so I will work out some sort of scaling solution to address that issue
- Actually retested on full charge seemed to work well besides being a bit slow sometimes… solved the practice maze twice in a row and even worked on the one outside
- Everyone else works on report

</details >

<details>
<summary>Sunday, April 17th, 2023</summary>

Present: Peter, Ammar, Josh, Shawn

- Continued work on HC in construction lab
- Seemed to get it to pass through and detect proper turning based on IR sensor readings
- Got news that our hovercraft design is too large and we might get disqualified for it
- So rebuild the same design but on smaller base (about 30 x 30 cm)
- Prepare skirt materials for building tomorrow in case we need it
- Everyone else works on report

</details >

<details>
<summary>Monday, April 18th, 2023</summary>

Present: Peter, Ammar, Camille, Josh, Olivia, Shawn

- Got news that our hovercraft design is too large and we might get disqualified for it
- So rebuild the same design but on smaller and go back to square one
- Regression test EVERYTHING
- Finally got something testable to bring to EV
- Don’t sleep and test/prepare all night
- Finish up report, and rest of deliverables

</details >


### 8.2 Schedule Gantt Chart

1. (As of 1 completion) Generate first CADs and 3D print body
2. (As of 2 completion) Assemble HC, develop simple idle hover state
3. (As of 3 completion) Validate simple idle hover state functionality
4. (As of 1 completion) Develop autonomous drive control logic based sensor feedback
5. (As of 4 + 5 completion) Validate autonomous drive control logic against practice track 


Note: dependency arrows are not shown but still explained by the list above.

| Figure 11: Gantt Chart |
|---------------|
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="http://imglin.com/zNji68T31P.png">
  <source media="(prefers-color-scheme: light)" srcset="http://imglin.com/zNji68T31P.png">
  <img alt="Figure 11: Gantt Chart " src="http://imglin.com/zNji68T31P.png">
</picture>   

# 9. Master Budget
|Table 2: Components and Points Table|
|---------------|

| Component| Name | Weight (g) | Number | 
|--------------|---------|-------------|------------|
| Thrust Fan | MEC0251V1-000U-A99 | 161.93 | 2|
| Lift Fan | AFB1212SH | 198.00 | 1|
| US Sensor |HSR04 | 8.5 | 1|
| IR Sensor | SHARP 2Y0A21 | 5.06 | 1|
| Batteries | GENS 450 | 27 | 2|
| Total|   | 400.49 | 7|

#10. Conclusion
 
In conclusion, the goal of this project was to design and construct an autonomous hovercraft that could complete a given track, passing over increasingly high obstacles. The design of the hovercraft was first detailed in the Preliminary Design Report, wherein three mock designs were evaluated using various tools such as SWOT, WOT, and AHP as well as simulations we later conducted in MATLAB. Ultimately, our team decided it was best to adopt design two, a square based hover craft with an ultrasonic sensor, a lift fan, and a thrust fan attached to a servo motor as its main components.
 
Over the past four months, our team had regular meetings to discuss progress and to test new modifications to our hovercraft. The entire process required much planning and communication amongst team members. Before the construction process could commence, we needed to complete tests on the sensors to ensure proper functionality. Once we confirmed that the parts supplied to us by the school were operational, construction commenced.
 
After much testing and discussion, our team modified the original design to have a rectangular body as well switched from using a thrust fan with a servo motor to using two thrust fans. This design choice led our hovercraft’s thrust to be controlled via skid steering. This entails controlling the amount of power supplied to the left and right thrust fans in order to activate turning motion. A primary reason for making this decision was because the code associated with skid steering was easier to develop than the code associated with a thrust fan controlled by a servo motor.
 
Further into the development of the hovercraft, our team decided to add an infrared sensor perpendicular to the ultrasonic sensor at the head of the hovercraft. The purpose of the infrared sensor was to gauge when turning motion needed to be activated. In order to facilitate the function of the infrared sensor and to ensure that it had enough time to measure when the hovercraft body was approaching an obstacle, our team decided to implement a budging motion when the hovercraft was travelling forward. The budging motion that was implemented prevented the hovercraft from moving too far forward once the infrared sensor determined that it was time to activate a turn.
 
Many changes were made throughout the entire construction process with the end goal of succeeding in the competition. Utilizing analysis tools we were taught throughout the course, we were able to adapt our design throughout the construction process to overcome obstacles that we encountered. In the end, our hovercraft complies with the requirements set out in the ENGR 290 H/C Competition Rule [5] and it is our goal that the hovercraft completes the track in the shortest amount of time possible.

# 11. References
[1]- Competition rules PDF from ENGR 290 Moodle Page
[2]- Preliminary Design Report
[3]- ENGR 290 Tools, Hardware, and Materials Loan Agreement 
[4] - Final Design Materials Request Form
[5] - ENGR 290 H/C Competition Rule 


