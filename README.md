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

*Iterable = datasplitter(input_data:Iterable, num_parts:int)* 

Given that the implementation is a generator, the more common way to use it would 
be in code like this:

```python
num_parts = 20
my_pids = set()

for part_of_input in datasplitter(input_data, num_parts):
    pid = os.fork()
    if not pid:
        do_something(part_of_input)
        os._exit()
    else:
        my_pids.add(pid)
```

Then, you can use a wait loop to collect the results.

```python
while mypids:
    child_pid, status, _ = os.wait3(0)
    mypids.remove(child_pid)
    print(f"{child_pid=} has completed with {status=}")
```
