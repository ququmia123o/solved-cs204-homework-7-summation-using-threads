Download Link: https://assignmentchef.com/product/solved-cs204-homework-7-summation-using-threads
<br>
<h1>Introduction</h1>




In this homework, you are asked to write a <strong>multithreaded </strong>C++ program that reads numbers from a file and adds them up concurrently using threads. The program starts after taking some inputs from the keyboard and continues until all the numbers are added. In your program, you are going to display some verbose output about addition operations and threads. Please see “Details of the Program” section for details.

<strong> </strong>

<h1>Using Threads</h1>

<strong> </strong>

There will be <strong>five threads</strong> (other than main thread) in your program. <strong>All of them</strong> will wait their turn and add the next value. You must ensure that at a given time only one thread will make an addition operation to prevent race conditions and obtain a correct result in the end. For this, you are required to use <em>mutexes</em>. In the end, your threads must be joined properly, and your program must terminate without any complications.




<h1>Details of the Program</h1>

<strong> </strong>

Before the summation begins, three inputs are entered via keyboard. First, the file name which contains the numbers to be added, is entered. Then, the minimum and maximum waiting time before each addition operation for a thread are entered in seconds (two inputs).




After the inputs are entered, your program will read the numbers from the given file name and store them in a dynamic array. Each line in the file contains only one number. The first line contains the amount of numbers in the file; you can use this information, which is the size of the array, when creating your dynamic array. The remaining lines contain numbers to be added.




You may assume that all inputs are correct, including the file structure, so no input checks are necessary. That means you can assume that the entered file name exists, it has a correct structure, the min and max waiting times are entered as positive integer values and the first one is less than or equal to the second one.




In the next step, you can create and start the five threads. <u>The entry point of each of the threads will be</u> <u>the same function. That means, you will <strong>NOT</strong> write separate functions for the threads.</u>

<strong> </strong>

At the beginning of the summation, display a message that says that the summation has started and the time of start (see “Sample Runs” for examples).




For each thread, before each addition operation, the thread must wait a random amount of time (in seconds). Then a thread will try to enter the critical area marked by a mutex. If it succeeds to get the lock of the mutex, it will make the next addition operation and store its result in the shared sum. Then it will increment the shared index count and will exit the critical region. The total number of addition operation that a particular thread will make is not fixed; it depends on the total number of elements to be added, random waiting times of the threads and the scheduling of the threads. You have to implement the entry point function for the threads (remember, there will be only one thread function) in such a way that in the critical region the next value will be added to the sum. To do so, you have to keep a shared sum, as well as a shared index counter to track down the element to be added next. These shared sum and index count could be made as global.




The random waiting times before the addition operation are determined via a function that returns a random integer between (and including) a minimum and maximum values passed as parameters to the thread function from main. <strong>Do not use the</strong> <strong>RandGen</strong><strong> class from </strong>CS201 for random integer generation in multithreaded applications because it is not thread-safe. Instead, <strong>you must use the following thread-safe function, </strong><strong>random_range</strong><strong>, for generating random waiting times inside the threads</strong>. This function returns a random number between (and including) min and max parameters. In the threads, you can call it by passing minimum and maximum waiting times of the corresponding thread as arguments.




#include &lt;random&gt;

#include &lt;time.h&gt;




int random_range(const int &amp; min, const int &amp; max) {     static mt19937 generator(time(0));

uniform_int_distribution&lt;int&gt; distribution(min, max);     return distribution(generator);

}

To pause a thread for a certain amount of time, you should use the this_thread::sleep_for(chrono::seconds(<em>time_in_seconds</em>)) command; you need to include the thread and chrono libraries in your program for this to work. In order to get the current time and to display it, we have seen some codes in class; you may use them.




<strong>The thread function and consequently the program will end after all of the numbers are added and the summation result is obtained.</strong> At the end of your program, do not forget to join five threads properly. Moreover, display a message to specify that the summation has ended including the result and the ending time.




<h1>Use of global variables</h1>




You may use global variables in this homework. Actually, it would be miserable not to use them in a program that has several threads. However, we kindly request you not to exaggerate the global usage since after a certain point you may lose control over your program (as the famous Turkish proverb says

“azı karar, coğu zarar”).

<strong> </strong>

<strong> </strong>

<strong> </strong>

<h1>Sample Runs</h1>




Some sample runs are given below, but these are not comprehensive, therefore you have to consider all cases, to get full mark.




Due to the probabilistic nature of the homework and due to the scheduling of threads, same inputs may yield different outputs for your code. However, the order of the events must be consistent with the homework requirements and the given inputs.




Sample input files are given together with homework document in the zip file.




The inputs from the keyboard are written in <strong><em>boldface and italic</em></strong>.

<strong> </strong>

<strong>Sample Run 1: </strong>

<strong> </strong>

Please enter the file name.

<strong><em>input1.txt </em></strong>

Please enter the wait range of threads.

<h2>1 3</h2>




Starting reading the array at 17:54:52

Array stored in the memory. Starting the summation at 17:54:52

Thread 2 added number index 0 to the total sum at 17:54:53

Current sum: 3

Thread 5 added number index 1 to the total sum at 17:54:53

Current sum: 8

Thread 1 added number index 2 to the total sum at 17:54:54

Current sum: 14

Thread 3 added number index 3 to the total sum at 17:54:54 Current sum: 18

Thread 2 added number index 4 to the total sum at 17:54:54

Current sum: 21

Thread 4 added number index 5 to the total sum at 17:54:55 Current sum: 29

Thread 1 added number index 6 to the total sum at 17:54:55 Current sum: 38

Thread 5 added number index 7 to the total sum at 17:54:56 Current sum: 137

Thread 1 added number index 8 to the total sum at 17:54:56 Current sum: 143

Thread 3 added number index 9 to the total sum at 17:54:57

Current sum: 150




Adding finished at 17:54:59

Sum: 150

<strong> </strong>

<strong>Sample Run 2: </strong>

<strong> </strong>

Please enter the file name.

<strong><em>input1.txt </em></strong>

Please enter the wait range of threads.

<h2>2 2</h2>




Starting reading the array at 18:02:31

Array stored in the memory. Starting the summation at 18:02:31

Thread 1 added number index 0 to the total sum at 18:02:33 Current sum: 3

Thread 2 added number index 1 to the total sum at 18:02:33

Current sum: 8

Thread 3 added number index 2 to the total sum at 18:02:33 Current sum: 14

Thread 4 added number index 3 to the total sum at 18:02:33 Current sum: 18

Thread 5 added number index 4 to the total sum at 18:02:33 Current sum: 21

Thread 1 added number index 5 to the total sum at 18:02:35 Current sum: 29

Thread 2 added number index 6 to the total sum at 18:02:35

Current sum: 38

Thread 3 added number index 7 to the total sum at 18:02:35 Current sum: 137

Thread 4 added number index 8 to the total sum at 18:02:35

Current sum: 143

Thread 5 added number index 9 to the total sum at 18:02:35

Current sum: 150




Adding finished at 18:02:37

Sum: 150

<strong> </strong>

<strong>Sample Run 3: </strong>

<strong> </strong>

Please enter the file name.

<strong><em>input1.txt </em></strong>

Please enter the wait range of threads.

<h2>3 8</h2>




Starting reading the array at 18:00:55

Array stored in the memory. Starting the summation at 18:00:55

Thread 5 added number index 0 to the total sum at 18:01:00 Current sum: 3

Thread 1 added number index 1 to the total sum at 18:01:01 Current sum: 8

Thread 3 added number index 2 to the total sum at 18:01:01 Current sum: 14

Thread 2 added number index 3 to the total sum at 18:01:02

Current sum: 18

Thread 4 added number index 4 to the total sum at 18:01:03 Current sum: 21

Thread 5 added number index 5 to the total sum at 18:01:03

Current sum: 29

Thread 2 added number index 6 to the total sum at 18:01:06 Current sum: 38

Thread 4 added number index 7 to the total sum at 18:01:06

Current sum: 137

Thread 5 added number index 8 to the total sum at 18:01:06 Current sum: 143

Thread 1 added number index 9 to the total sum at 18:01:08

Current sum: 150




Adding finished at 18:01:14

Sum: 150




<strong>Sample Run 4: </strong>

<strong> </strong>

Please enter the file name.

<strong><em>input2.txt </em></strong>

Please enter the wait range of threads.

<h2>1 9</h2>




Starting reading the array at 18:05:59

Array stored in the memory. Starting the summation at 18:05:59

Thread 2 added number index 0 to the total sum at 18:06:00 Current sum: -4

Thread 3 added number index 1 to the total sum at 18:06:01 Current sum: -11

Thread 4 added number index 2 to the total sum at 18:06:02

Current sum: -12

Thread 5 added number index 3 to the total sum at 18:06:06 Current sum: -2

Thread 2 added number index 4 to the total sum at 18:06:06

Current sum: -10

Thread 3 added number index 5 to the total sum at 18:06:06 Current sum: -12

Thread 5 added number index 6 to the total sum at 18:06:07

Current sum: -7




Adding finished at 18:06:13

Sum: -7

<strong>Sample Run 5: </strong>




Please enter the file name.

<strong><em>input2.txt </em></strong>

Please enter the wait range of threads.

<h2>1 1</h2>




Starting reading the array at 18:07:38

Array stored in the memory. Starting the summation at 18:07:38

Thread 1 added number index 0 to the total sum at 18:07:39 Current sum: -4

Thread 2 added number index 1 to the total sum at 18:07:39

Current sum: -11

Thread 3 added number index 2 to the total sum at 18:07:39 Current sum: -12

Thread 4 added number index 3 to the total sum at 18:07:39

Current sum: -2

Thread 5 added number index 4 to the total sum at 18:07:39 Current sum: -10

Thread 1 added number index 5 to the total sum at 18:07:40

Current sum: -12

Thread 2 added number index 6 to the total sum at 18:07:40

Current sum: -7




Adding finished at 18:07:41

Sum: -7

<strong>Sample Run 6: </strong>




Please enter the file name.

<strong><em>input2.txt </em></strong>

Please enter the wait range of threads.

<h2>1 2</h2>




Starting reading the array at 18:04:59

Array stored in the memory. Starting the summation at 18:04:59

Thread 2 added number index 0 to the total sum at 18:05:00 Current sum: -4

Thread 4 added number index 1 to the total sum at 18:05:00 Current sum: -11

Thread 1 added number index 2 to the total sum at 18:05:01 Current sum: -12

Thread 3 added number index 3 to the total sum at 18:05:01 Current sum: -2

Thread 5 added number index 4 to the total sum at 18:05:01

Current sum: -10

Thread 2 added number index 5 to the total sum at 18:05:01 Current sum: -12

Thread 1 added number index 6 to the total sum at 18:05:02

Current sum: -7




Adding finished at 18:05:03

Sum: -7


