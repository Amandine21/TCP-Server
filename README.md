# TCP-Server

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
&emsp;The else statement would execute the client-side. The domain was defined as IPv4, the
port number was defined as the passed port number, and the address was initialized as the
passed address. Then the connect function was called using the sockaddr_in struct, along with
the sock fd file descriptor. There was an error check associated with the connect function by
calling it in an if statement like the previous error checks.

