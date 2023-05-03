Download Link: https://assignmentchef.com/product/solved-cs2123-data-structures-assignment-6-simulating-traffic-in-java-and-c
<br>
<h1>2      Assignment files</h1>

For this assignment you’ll be simulating traffic in city. Specifically you need to complete “trafficSimulator.c”, “trafficSimulator.h’, “road.c”, “road.h”, “car.h”, and “event.h”. You can change any of the other files or create new files but you will need to also submit them as well as your updated makefile. Here is brief description of the functionality of your simulation:

<strong>3        Intersections, Cars, and Traffic Lights</strong>

<h1>Intersections and Roads</h1>

<ul>

 <li>Intersections are the vertices of your graph.</li>

 <li>Each vertex is represented by a unique integer value.</li>

 <li>These range from 0 to <em>size </em>− 1 where <em>size </em>is the number of vertices.</li>

 <li>The roads connecting them are edges of graph.</li>

 <li>Each directed edge is represented by a triple of integers. · The first integer is the starting vertex.</li>

 <li>The second integer is the ending vertex.</li>

 <li>The third integer is the weight of the edge (i.e, the length of this road).</li>

 <li>Cars traverse the edge based on order of arrival (i.e., no passing). You should use an array to represents the current contents of the road. During each time step every car with an empty space in front of it moves forward one position. Example:</li>

</ul>

Suppose that − is an empty space on the road and the numbers represent 3 cars on the road.

<table width="128">

 <tbody>

  <tr>

   <td width="28">−</td>

   <td width="24">1</td>

   <td width="28">−</td>

   <td width="24">2</td>

   <td width="24">3</td>

  </tr>

 </tbody>

</table>

After one time step only cars 1 and 2 are able to move forward. Car 3 is blocked from moving due to car 2.

<table width="128">

 <tbody>

  <tr>

   <td width="24">1</td>

   <td width="28">−</td>

   <td width="24">2</td>

   <td width="28">−</td>

   <td width="24">3</td>

  </tr>

 </tbody>

</table>

<h1>Traffic Lights and Road Length</h1>

<ul>

 <li>An intersection permits cars from its adjacent roads to pass through at a time.</li>

 <li>Each road has traffic light associated with it. When the light is green, the car on the front of the road may attempt to pass through the intersection towards its destination.</li>

 <li>The times in which the light is green/red and allows traffic through is specified in the input (we omit yellow lights for the sake of simplicity). The light operates on a cycle and repeats the specified pattern for the duration of the simulation. This is specified with the following three int inputs (see also Section 6):</li>

 <li>&lt;green on&gt; – The cycle the light turns green (light starts as red)</li>

 <li>&lt;green off&gt; – The cycle the light turns back to red</li>

 <li>&lt;cycle resets&gt; – The cycle resets goes back to 0</li>

 <li>The order the roads should be processed in is same as the order in which they were added to the graph. <strong>Hint: </strong>It will be useful to store the roads in an array based on this order.</li>

 <li>The length of a road also denotes the maximum number of cars which can be on it (see Section 4 for an important addition to this).</li>

 <li>A car can only pass through the intersection if the next road on its shortest path has an empty space on the end of its array.</li>

</ul>

<h1>Cars</h1>

<ul>

 <li>The destination of each car is an intersection.</li>

 <li>A car is removed from the simulator once it moves off the front of the road at its destination.</li>

 <li>Cars always follow a shortest path to their destination.</li>

 <li>Note that this shortest path is based on the lengths of the roads and</li>

</ul>

<strong>not </strong>on how many cars are currently on the roads.

<ul>

 <li>You should call the graph.c function “getNextOnShortestPath” to find the next intersection on a shortest path.</li>

 <li>You will want to track the number of time cycles the car took to reach its destination in order to report your results at the end of the simulation.</li>

</ul>

<h1>4     Events</h1>

It is recommended that you store the events in a priority queue based on the time step it is supposed to occur on.

<h1>Event – Adding Cars</h1>

<ul>

 <li>The input file will also specify time steps in which more cars should enter the simulation.</li>

 <li>Print the following on the time step this event occurs:</li>

 <li>“CYCLE <em>X </em>– ADD CAR EVENT – Cars enqueued on road from <em>Y </em>to <em>Z</em>”</li>

 <li><em>X </em>is the time step this event occurred on. The road of the event is from <em>Y </em>to <em>Z</em>.</li>

 <li>These cars should be added to the end of a queue associated with the specified edge (<strong>Hint: </strong>the merge function in queue.c may come in handy here). For each time step remove the first car in the queue and place it at the end of the road array of the edge if possible.</li>

</ul>

<h1>Event – Printing Road Contents</h1>

<ul>

 <li>The input file will also specify time steps in which the contents of all of your roads should be printed. See provided output for examples of what this will look like.</li>

 <li>Print the following on the time step this event occurs:</li>

 <li>“CYCLE <em>X </em>– PRINT ROADS EVENT – Current contents of the roads:”</li>

 <li><em>X </em>is the time step this event occured on.</li>

</ul>

<h1>5      Output</h1>

<ul>

 <li>Once a car reaches its destination you should print the following:</li>

 <li>“CYCLE <em>W </em>– Car successfully traveled from <em>X </em>to <em>Y </em>in <em>Z </em>time steps.”</li>

 <li><em>W </em>is the time step the car reached its destination. <em>X </em>and <em>Y </em>are respectively the starting intersection and destination of this car. <em>Z </em>is the number of time steps since the car was added to the simulation.</li>

 <li>The simulation ends once all of the cars reach their destination and there are no more events left to process. You should print the following:</li>

 <li>“Average number of time steps to the reach their destination is <em>X</em>.” · “Maximum number of time steps to the reach their destination is <em>Y </em>.”</li>

 <li><em>X </em>is average number of time steps taken by the cars to reach their destination. <em>Y </em>is maximum timesteps taken by any car to reach its destination.</li>

 <li>Alternatively, if the simulation goes through a full cycle of every traffic lights with no car being able to move then the city is in gridlock and the simulation halts (<strong>Hint: </strong>to determine this it will helpful to track the longest traffic light cycle as well as when a car was last able to move).</li>

 <li>Output “CYCLE <em>Z </em>– Gridlock has been detected.” · <em>Z </em>is the current time step.</li>

</ul>

<h1>6      Input File Format</h1>

&lt;# of vertices&gt; &lt;# of edges&gt;

&lt;TO: 1st vertex&gt; &lt;number of incoming roads&gt;

&lt;FROM: 1st vertex&gt; &lt;length&gt;                                   &lt;green on&gt; &lt;green off&gt; &lt;cycle resets&gt;

&lt;FROM: 2nd vertex&gt; &lt;length&gt;                                 &lt;green on&gt; &lt;green off&gt; &lt;cycle resets&gt;

…

&lt;FROM: last vertex&gt; &lt;length&gt;                                  &lt;green on&gt; &lt;green off&gt; &lt;cycle resets&gt;

&lt;2nd vertex&gt; &lt;number of incoming roads&gt;

<table width="535">

 <tbody>

  <tr>

   <td width="252">&lt;FROM: 1st vertex&gt; &lt;length&gt;</td>

   <td width="283">&lt;green on&gt; &lt;green off&gt; &lt;cycle resets&gt;</td>

  </tr>

  <tr>

   <td width="252">&lt;FROM: 2nd vertex&gt; &lt;length&gt; …</td>

   <td width="283">&lt;green on&gt; &lt;green off&gt; &lt;cycle resets&gt;</td>

  </tr>

  <tr>

   <td width="252">&lt;FROM: last vertex&gt; &lt;length&gt;</td>

   <td width="283">&lt;green on&gt; &lt;green off&gt; &lt;cycle resets&gt;</td>

  </tr>

 </tbody>

</table>

…

&lt;last vertex&gt; &lt;number of incoming roads&gt;

<table width="535">

 <tbody>

  <tr>

   <td width="252">&lt;FROM: 1st vertex&gt; &lt;length&gt;</td>

   <td width="283">&lt;green on&gt; &lt;green off&gt; &lt;cycle resets&gt;</td>

  </tr>

  <tr>

   <td width="252">&lt;FROM: 2nd vertex&gt; &lt;length&gt; …</td>

   <td width="283">&lt;green on&gt; &lt;green off&gt; &lt;cycle resets&gt;</td>

  </tr>

  <tr>

   <td width="252">&lt;FROM: last vertex&gt; &lt;length&gt;</td>

   <td width="283">&lt;green on&gt; &lt;green off&gt; &lt;cycle resets&gt;</td>

  </tr>

 </tbody>

</table>

&lt;# of “add car” commands&gt;

//1st add car command

&lt;“from” of starting edge&gt; &lt;“to” of starting edge&gt; &lt;timestep to perform “add car” on&gt;

&lt;number of cars to add to this edge&gt;

&lt;dest. vertex of 1st car&gt; &lt;dest. vertex of 2nd car&gt; … &lt;dest. vertex of last car&gt; //2nd add car command

&lt;“from” of starting edge&gt; &lt;“to” of starting edge&gt; &lt;timestep to perform “add car” on&gt;

&lt;number of cars to add to this edge&gt;

&lt;dest. vertex of 1st car&gt; &lt;dest. vertex of 2nd car&gt; … &lt;dest. vertex of last car&gt; …

//last add car command

&lt;“from” of starting edge&gt; &lt;“to” of starting edge&gt; &lt;timestep to perform “add car” on&gt;

&lt;number of cars to add to this edge&gt;

&lt;dest. vertex of 1st car&gt; &lt;dest. vertex of 2nd car&gt; … &lt;dest. vertex of last car&gt;

&lt;# of “print road” commands&gt;

&lt;cycle # to print roads on&gt; &lt;cycle # to print roads on&gt; … &lt;cycle # to print roads on&gt;

<h1>7     Simulation</h1>

Below is the order of operations that your program should go through for each time step:

<ul>

 <li>Dequeue and execute any and all events associated with the current time step.</li>

 <li>For each road, attempt to move the first car on it through the intersection and to the end of the next road on its shortest path. Cars that have reached their destination intersection are removed from the simulation.</li>

 <li>For each road, cars which had empty spaces in front of them at the start of this time step move forward one space.</li>

 <li>For each road, Attempt to move a car from the add car queue for that road onto the last position on the road.</li>

</ul>

Repeat the above until all events have finished and either all cars have reached their destination or gridlock has occurred.

<strong>8     Deliverables:</strong>

Your solution should be submitted as “trafficSimulator.c”, “trafficSimulator.h’, “road.c”, “road.h”, “car.h”, and “event.h”. Also include any other files you’ve created to solve the problem (including possibly a new “makefile”).

Upload these file to Blackboard under Assignment 6. <strong>Do not zip your files</strong>.

To receive full credit, your code must compile and execute. You should use

valgrind to ensure that you do not have any memory leaks.


