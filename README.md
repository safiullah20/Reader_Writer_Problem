# Reader_Writer_Problem
#DESCRIPTION:
In the readers-writers problem, there is a critical section that both reader and writer
can access. Reader only reads from the data while writer can both read and write to
the data. More than one reader can read at the same time. A writer cannot access
the data while a reader is reading. No other thread can access the memory while a
writer is accessing the data.

PROPOSED SOLUTION:
To solve this situation, a writer should get exclusive access to an object that is:

If one of the people tries editing the file, no other person should be reading or
writing at the same time, otherwise changes will not be visible to him/her.
However if some person is reading the file, then others may read it at the same
time.

From the above problem statement, it is evident that readers have higher priority
than writer. If a writer wants to write to the resource, it must wait until there are no
readers currently accessing that resource. Here priority means, no reader should
wait if the share is currently opened for reading.
Some problem parameters to acknowledge include:

One set of data is shared among a number of processes
Once a writer is ready, it performs its write. Only one writer may write at a time
If a process is writing, no other process can read it
If at least one reader is reading, no other process can write
Readers may not write and only read
ALGORITHM USED:
WRITER FUCNTION:
do {
// writer requests for critical section
wait(wrt);
// performs the write
// leaves the critical section
signal(wrt);
} while(true);P age | 3
READER FUNCTION:
do {
// Reader wants to enter the critical section
wait(mutex);
// The number of readers has now increased by 1
readcnt++;
// there is atleast one reader in the critical section
// this ensure no writer can enter if there is even one reader
// thus we give preference to readers here
if (readcnt==1)
wait(wrt);
// other readers can enter while this current reader is inside
// the critical section
signal(mutex);
// current reader performs reading here
wait(mutex);
// a reader wants to leave
readcnt--;
// that is, no reader is left in the critical section,
if (readcnt == 0)
signal(wrt);
// writers can enter
signal(mutex); // reader leaves
} while(true);
