<h3 style="text-align: center;">H3 that is center aligned</h3>

&emsp; This programming assignment aims to implement the TCP request channel to replace
the FIFO channel. This code was based on the third programming assignment and uses
threading. The client-side and server-side ends of a TCPRequestChannel will reside on different
terminals.\
&emsp; When implementing the code, the client was modified by replacing the FIFO channels
with TCP request channels and their constructors. Next, the cases for “a” and “r” were added to
the getopt() loop. For case “a”, a variable was created to hold the IP address for the passed
argument. For case “w”, a variable was created to hold the port number.\
&emsp; Then the server was modified by replacing the FIFO channels with TCP request
channels. Then the getopt() loop was modified, but only adding the case “r”, which was added
for the port number. An infinite while loop was then added which takes a server file descriptor
and calls the function to accept. Then the first client connection request in the pending request
returns another socket file descriptor that will describe the client's connection.\
&emsp; The TCP request channel class consisted of two constructors, a destructor,
accept_conn(), cread, and crwite functions. The cread and cwrite function used the read and
write functions. The accept_conn() used the sockaddr_storage structure and used the accept()
function. The destructor used the close function with the socket file descriptor being passed.
There were two constructors that were implemented in the class. One of the constructors took a
socket file descriptor and assigned it to the member variable sckfd. The other constructor took in
a passed-in IP address and port number. Then it assigned the sockfd member variable to the
socket constructor to create the socket, and also created a struct known as sockaddr_in which
held important information. There was an if-else statement that made up the rest of the code,
and the condition for the if statement as if the passed IP address was an empty string it would
execute the server-side. The domain was defined to be an IPv4, the address was set to
INADDR_ANY which could be a variety of IP addresses, and the port was initialized as the
passed-in port. Then the bind() function was called using the structaddr_in information, with
error checking. Finally, the listen() function was called, and the backlog was set to 30 to account
for a large load that could be queued up. There was also error checking associated with the
function.\
&emsp; The else statement would execute the client-side. The domain was defined as IPv4, the
port number was defined as the passed port number, and the address was initialized as the
passed address. Then the connect function was called using the sockaddr_in struct, along with
the sock fd file descriptor. There was an error check associated with the connect function by
calling it in an if statement like the previous error checks.

<p align="center">
  <img src=GraphTCP.PNG>
</p>
<h2 style="text-align: center;">Insight </h2>
&emsp; Engineering tends to be about tradeoffs, and the purpose of this assignment was to
change the incoming FIFO request channels from PA3 into TCP channels. the TCP is going to
have a slower amount of time compared to the FIFO IPC method since the workload needs to
go through a network. The FIFO is restricted to the local machine, but using TCP the workload
has the potential to run on multiple machines connected through a network\
&emsp; The graphs show some interesting results that could be explained by a few factors. The
graphs for workers vs time make sense from parts b and c because the more worker threads the
program has the faster it can get the workload done. The histogram did not seem to have any
correlation, which can be assumed the argument will not affect the output time just like PA3.
According to the graph from part c, the buffer size will cap at around 512 which is less than the
cap from PA3.\
&emsp; The point of diminishing return is going to be around when the worker thread argument is
set to the value of 150. Anything after the point of diminishing return, the time calculated is
asymptotically going to be around the lower seven-second mark. This number is going to be
much larger than the value calculated from PA3. The maximum number of connections that can
be created is around 4092 connections, which is larger than PA3. This was done with a couple
of computers because in my code it would take forever to process the number of worker
threads. Around 4092 I received a bad file descriptor which is where I met the limit.\

<p align="center">
  <img src=BadFileDescriptorImage.PNG>
</p>

&emsp; Some other thing I thought was unique about this assignment is how random the data
could be when I ran the same test multiple times. Sometimes I got numbers that would often
show a different pattern from their overall behavior. I ran these tests at least 5 times and took
their average to get a reliable estimate. I think some of the error that contributes to the uncertain
timing events, would be the fact that the data is going through a connection and It will depend
on how reliable the connection is to get an accurate time. This is unlike IPCS which everything
is done locally.\
&emsp; It is also important to point out that FIFO is being performed locally which means it is
limited to how much RAM the system has. With TCP ideally, using multiple machines, the
workload isn’t limited to just one machine’s RAM capability for running both the server and client
but is limited to the machine with the lowest RAM available which could either be the server or
client.


