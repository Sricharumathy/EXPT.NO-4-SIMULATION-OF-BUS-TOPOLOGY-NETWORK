# EXPT.NO 4 SIMULATION OF BUS TOPOLOGY NETWORK
# AIM

To create and monitor Bus Topology and effective data transmission using NS2 Software.

# APPARATUS REQUIRED

PC System with Linux OS, NS2 software.

# ALGORITHM

STEP 1: Start the program.<br>
STEP 2: Declare the global variables ns for creating a new simulator.<br>
STEP 3: Open the network animator file in the write mode.<br>
STEP 4: Open the trace file in the write mode.<br>
STEP 5: Transfer the packets in network.<br>
STEP 6: Create the capable no of nodes.<br>
STEP 7: Create the duplex-link between the nodes including the delay time, bandwidth and dropping queue mechanism.<br>
STEP 8: Set a tcp connection for source node.<br>
STEP 9: Set the destination node using tcp sink.<br>
STEP 10: Set the window size and the packet size for the tcp.<br>
STEP 11: Set up the ftp over the tcp connection.<br>
STEP 12: Create the traffic generator CBR for the source and destination files.<br>
STEP 13: Define the plot window and finish procedure.<br>
STEP 14: In the definition of the finish procedure declare the global variables.<br<
STEP 15: Close the trace file and namefile and execute the network animation file. STEP 16: At the particular time call the finish procedure.<br>
STEP 17: Stop the program.<br>

# PROGRAM:
```
#Create a simulator object set ns [new Simulator] #Open the nam trace file set nf [open out.nam w]
$ns namtrace-all $nf #Define a 'finish' procedure proc finish {}
{
global ns nf
$ns flush-trace close $nf
#Execute nam on the trace file exec nam out.nam &
exit 0
}
#Create five nodes set n0 [$ns node] set n1 [$ns node] set n2 [$ns node] set n3 [$ns node] set n4 [$ns node]
#Create Lan between the nodes
set lan0 [$ns newLan "$n0 $n1 $n2 $n3 $n4" 0.5Mb 40ms LL Queue/DropTail MAC/Csma/Cd Channel] #Create a TCP agent and attach it to node n0
set tcp0 [new Agent/TCP]
$tcp0 set class_ 1
$ns attach-agent $n1 $tcp0
#Create a TCP Sink agent (a traffic sink) for TCP and attach it to node n3 set sink0 [new Agent/TCPSink]
$ns attach-agent $n3 $sink0
#Connect the traffic sources with the traffic sink
$ns connect $tcp0 $sink0
# Create a CBR traffic source and attach it to tcp0 set cbr0 [new Application/Traffic/CBR]
$cbr0 set packetSize_ 500
$cbr0 set interval_ 0.01
$cbr0 attach-agent $tcp0
#Schedule events for the CBR agents
$ns at 0.5 "$cbr0 start"
$ns at 4.5 "$cbr0 stop"
#Call the finish procedure after 5 seconds of simulation time
$ns at 5.0 "finish"
$ns run
```
 
# OUTPUT
<img width="1352" height="751" alt="image" src="https://github.com/user-attachments/assets/effbee36-8871-4bf2-a57c-e8c435e46eef" />



# RESULT

Thus the Bus Topology using NS2 software is created and monitored successfully.

