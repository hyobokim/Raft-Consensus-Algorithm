# cs3700-proj6
## High-Level Approach:
We used the starter code from the class, which communicates to
the CS3700 server using sockets and receives data in the
form of JSON objects. The first task was to implement the 
election process, which is done by storing the state of each
replica as a field. The timeout is randomized, so each 
replica will initiate an election at a random time to avoid
two candidates at the same time, and will send out request 
votes. The replicas communicate to each other using these
sockets as well, and will request votes through sends. 

Similarly, to request commits from the replicas, the leader
will send request_entries through the socket, and once
a majority is reached, it will append to the dictionary
log, and notify all replicas to do the same. If there
is a disagreement, the disagreeing replica, assuming
the term is lower, will replace its log with the leader's
log. 

## Challenges
Debugging was a long process, since there are so many
print messages being sent out, that it's difficult to
isolate a single problem. A lot of the log doesn't even fit
into the terminal, and some of the history is lost after 
I finish running it. The runtime also nears 30 seconds for 
a lot of the tests, which makes debugging difficult. To
circumvent this, I used print statement with a lot of 
newlines to distinguish debugging. 

## Good Features
I think the handler method is a good feature, as it organizes
all of the message types into one function. This way, the
code is a lot cleaner and to add functionality for a new
message type, all that's needed is to add a new if statement
and add a handler method for that type. 

## Testing
Testing the code was done through writting debugging lines, 
as well as using time.sleep() to isolate specific edge cases.
I wasn't sure if there was conflict between the replicas,
so I isolated a specific event and told the program to sleep
if that occurred, and ended up figuring out that the logs
weren't being matched properly along the replicas. 

Debugging lines were very helpful too, as I wrote print
statements with a lot of new lines to help distinguish specific
events within a massive log. 