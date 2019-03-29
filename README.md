# ROTF
Restaurant of the Future

# Electronics and control
## Process brief
<ol>
<li>Image Input from the overhead cameras on the restaurant are processed and path is planned using Image Processing and Dijkstra Algorithm.</li>
<li>Path send to Arduino using Wifi Module</li>
<li>Omni chasis based traversal on the given path of the bot to reach the desired table.</li>
<li>Chatbot starts interacting with the the customer and takes the order while recognising face and emotion of the customer.</li>
<li>After taking order, Bot traverses back to the initial position, waits for the order to be kept on its serving trays.</li>
<li>Bot traverses back to the customer on the same path and serves using a 3-tray serving mechanism</li>
</ol>


### Path Planning and Navigation
<ol>
<li><a href =" ">Image</a> is resized to (300 * 300) pixels (<a href = " ">sample resized</a>) and edge detection is deployed on grey image (<a href = " ">sample</a>).</li>
<li>Closed objects are assigned white pixel value. Fractal concept deployed for the same(<a href = " ">sample</a>).</li>
<li>Image is smoothened(<a href = " ">sample</a>).</li>
<li>Divided into a (n*n) grid with grid size (d*d), here n = 30, d= 10 (<a href = " ">sample Grids.txt</a>). </li>
<li>Each grid is declared as an obstacle(value =0) or a path(value =1) depending of the threshold value of the white pixel count.</li>
<li>Grid generated is written in a file and is the input to the shortest path planning - Dijkstra Algorithm(<a href = " ">src code</a>). Each unit of the grid in considered as the vertic and adajent vertics are analysed of each unit to generate a matrix of all vertices. </li>
<li>"Srcdest.txt" file stores the planned path in the form of vertices to traverse on(<a href = " ">sample</a>).</li>
<li>Path string, for instance R2F2B1L1, meaning to move 2 step to the right, 2 step forward, 1 step backward, 1 step Left, is generated by reading vertices.  </li>
<li>Path string is send using the urllib library of python on the url of the esp8266 Wifi module, obtained by connecting PC and Module on the same network.</li>
</ol>
<img src="https://github.com/Prachi0141/ROTF/blob/master/Path%20Planning/Sample%20intermediate%20pics/all_in_one.png" width="1604">

### Omni chasis based motion control
<ol>
<li>Path is received using an ESP module in form of string giving units of motion in each direction. The end of path is detected by adding a letter 'e' at end of each string.</li>
<li>Each unit length of string is mapped with some unit on ground using an encoder.</li>
<li>A gyro and PID is used to avoid any rotation about its axis. Encoders and PID are used to avoid any drift.</li>
<li>Once reached the destination, it sends a signal to the head and head motion starts.</li>
<li>After getting signal from the head a "reverse" function reverses the string and adds an 'e' at the end to make the bot retrace the path back.</li>
<li>Cytron motor drivers are used for all three motors of the chassis.</li>
</ol>

### Interaction Aspect
Raspberry Pi act as a central processing system for the bot to recognise customers face and align the head accordingly using servo motors, greet and take order using Chatbot API.


### 3-Tray Serving Mechanism
<ol>
<li>After reaching the customer in mode 2, the tray motion gets activated.</li>
<li>The lifting mechanism uses dc motors and encoders, whereas the front-back motion uses stepper motor.</li>
<li>Using encoders we map the units with distance it has to traverse to reach each of the trays.</li>
<li>On reaching the tray, the front-back mechanism gets activated.</li>
<li>The number of units the stepper have to move in front and back is mapped using the standard Stepper motor library.</li>
<li>The lifting mechanism is carried by DC motors and Cytron motor driver whereas the front-back motion is supported by the stepper motors and the NEX motor driver.</li> 
</ol>

# Mechanical Aspects
## HEAD
### Function
<ul>
<li>To make the robot look more customer friendly and increase interaction with customer we needed a multifunctional head.</li>
<li>The head which is able to align in the direction of customer sitting on table, able to nod when greeting customer and whose eyes blink according to the mood of customer.</li>

### Design
First, a neck was designed. A base was required to mount it on the body of robot named* as ‘base’. Base also contained slot to fit servo motor. Another half of neck was having a gear embedded on itself named ‘upper neck gear’. Neck contained a pair of gears with ratio 1:2. Smaller gear mounted on servo motor. Slot provide the servo ability to slid in and out to perfectly align with other gear. Both parts of the neck were held with a rod with the help of bearings, which also provided smooth moment to neck.
Another part named ‘upper base plate’ to hold mechanism for head rotation. 
So to make head rotate side ways we built a revolute joint named ‘revolute 1’ mounted on base plate with the help of a 6mm bolt. 
Another revolute was provided to make it rotate up and down named ‘support stand’ it was mounted inside ‘revolute 1’ with the help of a 6mm bolt. The ‘support stand’ also worked as a stand to hold the hollow shell named ‘head shell’ i.e. face. 
To make these revolute rotate we used mechanism similar to Crank Shaft with 2 servo motors mounted on ‘upper base plate’ and 2 links attached to the head via support stand joining it with servo head. When both the servos are rotated in opposite direction from same starting reference angle the head moves up and down. And when one servo is rotated in any one direction the head tilts accordingly. To provide flexibility to the links for rotation on a curve path we used small pieces of rubber belt at the end of links. 
Slot to mount LED eyes and camera to detect face were provided on ‘head shell’. 
All parts were 3-D Printed with PLA.
**named :- all names are of their solidworks file. 


### Drawbacks
<ol>
<li>Link mechanism is only able to provide less rotation to the revolute joints. </li>
<li>Avoid big 3-D prints as it will consume large amount of material which is expensive. </li>
<li>Slots in 3-D prints are not accurate in dimensions, so provide clearance for the same.</li>
</ol>
 


 
# ROTF
Restaurant of the Future

# Electronics and control
## Process brief
<ol>
<li>Image Input from the overhead cameras on the restaurant are processed and path is planned using Image Processing and Dijkstra Algorithm.</li>
<li>Path send to Arduino using Wifi Module</li>
<li>Omni chasis based traversal on the given path of the bot to reach the desired table.</li>
<li>Chatbot starts interacting with the the customer and takes the order while recognising face and emotion of the customer.</li>
<li>After taking order, Bot traverses back to the initial position, waits for the order to be kept on its serving trays.</li>
<li>Bot traverses back to the customer on the same path and serves using a 3-tray serving mechanism</li>
</ol>


### Path Planning and Navigation
<ol>
<li><a href =" ">Image</a> is resized to (300 * 300) pixels (<a href = " ">sample resized</a>) and edge detection is deployed on grey image (<a href = " ">sample</a>).</li>
<li>Closed objects are assigned white pixel value. Fractal concept deployed for the same(<a href = " ">sample</a>).</li>
<li>Image is smoothened(<a href = " ">sample</a>).</li>
<li>Divided into a (n*n) grid with grid size (d*d), here n = 30, d= 10 (<a href = " ">sample Grids.txt</a>). </li>
<li>Each grid is declared as an obstacle(value =0) or a path(value =1) depending of the threshold value of the white pixel count.</li>
<li>Grid generated is written in a file and is the input to the shortest path planning - Dijkstra Algorithm(<a href = " ">src code</a>). Each unit of the grid in considered as the vertic and adajent vertics are analysed of each unit to generate a matrix of all vertices. </li>
<li>"Srcdest.txt" file stores the planned path in the form of vertices to traverse on(<a href = " ">sample</a>).</li>
<li>Path string, for instance R2F2B1L1, meaning to move 2 step to the right, 2 step forward, 1 step backward, 1 step Left, is generated by reading vertices.  </li>
<li>Path string is send using the urllib library of python on the url of the esp8266 Wifi module, obtained by connecting PC and Module on the same network.</li>
</ol>

### Omni chasis based motion control
<ol>
<li>Path is received using an ESP module in form of string giving units of motion in each direction. The end of path is detected by adding a letter 'e' at end of each string.</li>
<li>Each unit length of string is mapped with some unit on ground using an encoder.</li>
<li>A gyro and PID is used to avoid any rotation about its axis. Encoders and PID are used to avoid any drift.</li>
<li>Once reached the destination, it sends a signal to the head and head motion starts.</li>
<li>After getting signal from the head a "reverse" function reverses the string and adds an 'e' at the end to make the bot retrace the path back.</li>
<li>Cytron motor drivers are used for all three motors of the chassis.</li>
</ol>

### Interaction Aspect
Raspberry Pi act as a central processing system for the bot to recognise customers face and align the head accordingly using servo motors, greet and take order using Chatbot API.


### 3-Tray Serving Mechanism
<ol>
<li>After reaching the customer in mode 2, the tray motion gets activated.</li>
<li>The lifting mechanism uses dc motors and encoders, whereas the front-back motion uses stepper motor.</li>
<li>Using encoders we map the units with distance it has to traverse to reach each of the trays.</li>
<li>On reaching the tray, the front-back mechanism gets activated.</li>
<li>The number of units the stepper have to move in front and back is mapped using the standard Stepper motor library.</li>
<li>The lifting mechanism is carried by DC motors and Cytron motor driver whereas the front-back motion is supported by the stepper motors and the NEX motor driver.</li> 
</ol>

# Mechanical Aspects
## HEAD
### Function
<ul>
<li>To make the robot look more customer friendly and increase interaction with customer we needed a multifunctional head.</li>
<li>The head which is able to align in the direction of customer sitting on table, able to nod when greeting customer and whose eyes blink according to the mood of customer.</li>

### Design
First, a neck was designed. A base was required to mount it on the body of robot named* as ‘base’. Base also contained slot to fit servo motor. Another half of neck was having a gear embedded on itself named ‘upper neck gear’. Neck contained a pair of gears with ratio 1:2. Smaller gear mounted on servo motor. Slot provide the servo ability to slid in and out to perfectly align with other gear. Both parts of the neck were held with a rod with the help of bearings, which also provided smooth moment to neck.
Another part named ‘upper base plate’ to hold mechanism for head rotation. 
So to make head rotate side ways we built a revolute joint named ‘revolute 1’ mounted on base plate with the help of a 6mm bolt. 
Another revolute was provided to make it rotate up and down named ‘support stand’ it was mounted inside ‘revolute 1’ with the help of a 6mm bolt. The ‘support stand’ also worked as a stand to hold the hollow shell named ‘head shell’ i.e. face. 
To make these revolute rotate we used mechanism similar to Crank Shaft with 2 servo motors mounted on ‘upper base plate’ and 2 links attached to the head via support stand joining it with servo head. When both the servos are rotated in opposite direction from same starting reference angle the head moves up and down. And when one servo is rotated in any one direction the head tilts accordingly. To provide flexibility to the links for rotation on a curve path we used small pieces of rubber belt at the end of links. 
Slot to mount LED eyes and camera to detect face were provided on ‘head shell’. 
All parts were 3-D Printed with PLA.
**named :- all names are of their solidworks file. 


### Drawbacks
<ol>
<li>Link mechanism is only able to provide less rotation to the revolute joints. </li>
<li>Avoid big 3-D prints as it will consume large amount of material which is expensive. </li>
<li>Slots in 3-D prints are not accurate in dimensions, so provide clearance for the same.</li>
</ol>
 


 

