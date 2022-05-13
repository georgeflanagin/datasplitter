# datasplitter
Generator to divide a large group of data into N smaller ones of the same type.

To varying degrees, many programs are naive about parallel processing.
Faculty and their research students frequently cut a large data file into 
several smaller ones, and run N copies of a program on the nodes of the 
cluster. 

There is nothing wrong with the approach, but it does lead to a JOBID 
for each running process, and separate tombstone (output) files that
must be examined at the end.

Thus the **datasplitter** was born. 

## Use

Iter
