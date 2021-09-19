# 3.7 Call, Jump Statement and Subprograms

If an entire large-scale robot operation is created as one job program, the program becomes large and complex, making it difficult to add functions or find and solve problems.

For the program’s maintainability, it is preferable to divide the unit operations that make up the entire program into subprograms. For example, when routines, such as a routine performs communication with a sensor, a routine that calculates the target position of the tool tip with the received data, and a routine that generates an appropriate message when an error occurs, are turned into individual subprograms and allow the main program to call them, it will be easier to grasp the overall structure of the program. It will also be useful to reuse divided subprograms in other projects.





