Download Link: https://assignmentchef.com/product/solved-cop290-assignment6-descrete-events-simulation
<br>
<strong>Introduction:</strong> An <em>event-driven simulation</em> is a computer program that mimics the behavior of people or objects in a system in response to events that occur at certain times. The program must maintain a data object for each person or object (called an <em>actor</em>) and place it in a queue according to the time of its event. It then reads the queue in the order of the events and, for each event, causes the corresponding actor to do its actions scheduled for that time. The action of the actor may be to change its own state, change the state of the system, do something on behalf of another actor, or something else. Sometimes, the action will cause the actor to rejoin the event queue for a subsequent action. Sometimes, the action may add some other actor to the event queue or to another queue.

<strong>Assignment Description: </strong>

In this assignment, you will simulate customers arriving at a bank and standing in line in front of one of the tellers. People arrive at random intervals. Each person waits in his/her selected line until reaching the head of that line. When a person reaches the head of his line, the teller provides service for a random amount of time. After the service is completed, the person leaves the bank. The purpose of the simulation is to measure the average amount of time people spend between arriving at the bank and leaving the bank.

Assume that when there is a separate line for each teller, a newly arrived person joins the shortest line (or selects randomly among the set of equally short lines) and stays in that line until served. That is, no person leaves a line without being served, and no person hops from one line to another.

If a teller has finished serving a customer and there are no other customers waiting in its line, the teller selects the first customer from the line of another, randomly-chosen teller and serves that customer. If there are no customers waiting at all, the teller does other duties for a (small) random amount of time before checking the lines again.

The entire purpose of this simulation is to compare the performance of a single line serving all tellers <em>versus</em> separate lines for each teller.




<strong>Pre-requisites</strong><strong>:</strong> knowledge of Structures and function pointer




<h1>Implementing your program</h1>

Your program should be called <strong>qSim</strong>. It needs to do several things:–

<ul>

 <li>Get and interpret the program parameters from the command line.</li>

 <li>Create a structure variable for each customer indicating his/her arrival time at the bank. Arrival times are determined from a uniform random number generator and the input parameters of the simulation. Also create a structure variable for each teller, with a random idle time in the range 1-600 seconds. <em>All constants in this simulation must be defined symbolically.</em></li>

 <li>Create a single <em>event queue</em> in the form of a linked list. The members of the linked list may be customer events or teller events.</li>

 <li>Place each object in the <em>event queue</em> sorted according to the time of its event. That is, the event with the earliest time is at the head of the queue, and the event with the latest time is at the tail of the queue. Note: Your program instantiates all the customer-arrival objects at the beginning of the program; as it creates each one, the object is given a random arrival time (sometime during the day) and then put into the queue.</li>

 <li>Play out the simulation as follows: take the first event off the <em>event queue</em>, advance a simulated <em>clock</em> to the time of that event, and invoke the action method associated with that event. Continue until the event queue is empty.</li>

 <li>Print out the statistics gathered by the simulation.</li>

</ul>

For this assignment, you will need to play the simulation twice — once for a bank with a single queue and multiple tellers and once for a bank with a separate queue for each teller. Draw some comparison about the average time required for a person to be served at the bank under each queue regime.

Here are some of the actions that can occur when an <em>event</em> reaches the head of the <em>event queue</em>:

<ul>

 <li>If the event represents a newly arrived customer at the bank, add that person onto the end of a teller line — either the common line (in the case of a bank with a single line for all tellers) or to the shortest teller line. If there are several equally short teller lines, choose one at random.</li>

 <li>If the event represents a customer whose service at the bank has been completed, collect statistics about the customer: in particular, how long has the customer been in the bank, from arrival time to completion of teller service. After collecting the statistics, the customer leaves the bank and its <strong>Event</strong> object is deleted.</li>

 <li>If the event represents a teller who has either completed serving a customer or has completed an idle time task, gather statistics about that teller. If there is no customer waiting in any line, put a teller event back into the <em>event queue</em> with a random idle time of 1-150 seconds.</li>

</ul>

If there is a customer waiting in line, remove the first customer from its line, generate a random service time according to the input parameters of the program, and add <em>two</em> events to the event queue, sorted by time. One is a customer event and represents the completion of that service. The other event is a teller event representing completion of a service and to look for the next customer (or to idle).

<strong> </strong>

Implementation Details:

You must define one or more structures that allow you to represent <em>Events</em>,<em> Customers</em>, and <em>Tellers</em>. It is suggested that the most important structure of your simulation should be <strong>Event</strong>. How you distinguish between events associated with customers and events associated with tellers is your choice.

Two methods of an <strong>Event</strong> are to add it to the <strong>event</strong> <strong>queue</strong> and to remove it from the <strong>event</strong> <strong>queue</strong>. In addition, each <strong>Event</strong> has an <strong>action</strong> method that is to be invoked when an <strong>Event</strong> is removed from the <strong>event</strong> <strong>queue</strong>. The <strong>action</strong> method should somehow distinguish between <em>customers</em> and <em>tellers</em> and invoke the appropriate <em>action</em> function for that kind of event. These should perform the appropriate action for a customer or teller.

Each line in front of a teller should be implemented as a variable of a structure <strong>tellerQueue</strong>. Implement this structures using a linked list. You will need to write methods to add customers to the end of the linked list and to remove them from the head of the list. In addition, include a <em>static variable</em> in the <strong>tellerQueue</strong> class that indicates which line (i.e., instance of the <strong>tellerQueue</strong> class) is the shortest. If more than one line is equally short, select one at random.

The <strong>eventQueue</strong> itself should also be implemented by a linked list. You will need to write a

method to add an <strong>Event</strong> to the <strong>eventQueue</strong> in time order. This method should iterate through the list until it finds an <strong>Event</strong> with a time greater than the <strong>Event</strong> being inserted, and then it should insert the new <strong>Event</strong> just before that <strong>Event</strong>. (Note: This implies that if two events happen to have the same time, the one added to the queue <u>second</u> goes <u>after</u> the event added first. Also, remember that it is possible that the event being added will become the new head of the queue.) You will also need a method to remove an <strong>Event</strong> from the <strong>event</strong> <strong>queue</strong> and invoke the <strong>action</strong> method of the event.

<strong>Every time a Function Pointer is called, it must be logged to show that you using function Pointer. </strong>







<h2>Input                                                              <em> </em></h2>

The command line of your program should be of the following form:

<strong>./qSim #customers #tellers simulationTime averageServiceTime </strong>

The numbers of customers and tellers should be integers, and the simulation and average service times should be floating point numbers in units of minutes. E.g

<strong>./qSim 100 4 60 2.3</strong>

should be interpreted to mean that 100 customers and four tellers should be simulated over a

period of 60 simulated minutes. The service time for each teller is an <em>average</em> of 2.3 minutes.

<strong> </strong>

<h2>Random Number Generation</h2>

To generate random numbers, use the function <strong>rand()</strong>.

To generate random arrival times with a uniform distribution, the following is suggested:– <strong>float arrTime = simulationTime * rand()/float(RAND_MAX);</strong>

It is useful to generate all customer arrivals at the beginning of the program and put them into the <strong>event</strong> <strong>queue</strong> in order of arrival time.

To generate random service times, the following is suggested:– <strong>float serviceTime = 2*averageServiceTime*rand()/float(RAND_MAX); </strong>

<strong> </strong>

<h2>Output</h2>

After your simulation has completed for both types of queuing regimes, you should print out a summary with the following information:–

<ul>

 <li>Total number of customers served and total time required to serve all customers</li>

 <li>Number of tellers and type of queuing (one per teller or common)</li>

 <li>Average (i.e., mean) amount of time a customer spent in the bank and the standard deviation  Maximum wait time from the time a customer arrives to the time he/she is seen by a teller.  Total amount of teller service time and total amount of teller idle time.</li>

</ul>

The information that you need to print should determine the statistics that you gather during the simulations.

<strong>GNUPlot</strong>: plot a graph between average amounts of time a customer spent in bank versus number of tellers (assume number of queue = 1)