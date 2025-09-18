<!--
author: Sebastian Zug (converted from Robert Ringel)
email: sebastian.zug@informatik.tu-freiberg.de
version: 1.0.0
language: en
narrator: US English Female

title: Data Log Processing with Python

logo: https://liascript.github.io/img/bg-showcase-1.jpg

comment: This LiaScript course demonstrates reading and processing data log files in Python with executable code examples. Original content by Robert Ringel, Faculty Informatics/Mathematics, HTWD - University of Applied Sciences.

import: https://raw.githubusercontent.com/liascript/CodeRunner/master/README.md

-->

# Data Log Processing with Python

> **Original Source Attribution:**  
> This course is based on the learning task "DataLog.md" by **Robert Ringel**, Faculty Informatics/Mathematics, HTWD - University of Applied Sciences.  
> Original material available at: [GitHub - LearningTasks4Programming](https://github.com/RobertRingel/LearningTasks4Programming/blob/main/Python/05_TextFiles/DataLog.md)  
> License: CC BY-SA 4.0

## Learning Task: Data log

The following Python program reads the data log file 'FreeFall.txt' of a physics experiment. The data that has been read will be plotted as a very basic chart.

First, let's examine the content of our log file to understand its structure:

```text FreeFall.txt
0.0;0.0;0.0
0.05;0.49050000000000005;0.012262500000000003
0.1;0.9810000000000001;0.04905000000000001
0.15000000000000002;1.4715000000000003;0.11036250000000003
0.2;1.9620000000000002;0.19620000000000004
0.25;2.4525;0.3065625
0.3;2.943;0.44145
0.35;3.4335;0.6008625
0.39999999999999997;3.924;0.7847999999999999
0.44999999999999996;4.414499999999999;0.9932624999999998
0.49999999999999994;4.904999999999999;1.2262499999999996
0.5499999999999999;5.395499999999999;1.4837624999999997
0.6;5.886;1.7658
0.65;6.376500000000001;2.0723625000000006
```

The data file contains three columns separated by semicolons representing:
- Column 1: Time (t) in seconds
- Column 2: Velocity (v) in m/s  
- Column 3: Distance (s) in meters

Now read the code below and run it to obtain an understanding. You should write comments to the code to demonstrate your understanding. Finally compare your comments with the solution provided.

### Initial Code (Without Comments)

Click the "Run" button to execute this Python program:

```python
import matplotlib.pyplot as plt   # import library for chart plotting

file_name = 'FreeFall.txt'
log_file = open(file_name, 'r')

data_log = []

while True:
    line = log_file.readline()
    line = line.strip('\n')
    if line == '':
        break
    data = line.split(';')
    for item in data:
        item = float(item)
        data_log.append(item)

log_file.close()

# --- plot chart ---
t = data_log[0::3]
s = data_log[2::3]

plt.plot(t, s)                   # plot the chart
plt.show()                       # display the plot
```
@LIA.python

### Your Task

1. **Understand the file content:** Examine the FreeFall.txt data structure
2. **Read and run the code:** Execute the Python program above
3. **Write comments:** Add your own comments to explain what each section does
4. **Compare with solution:** Check your understanding against the provided solution below

---

## Solution

Here's the same code with detailed comments explaining each step:

```python
import matplotlib.pyplot as plt   # import library for chart plotting

file_name = 'FreeFall.txt'        # define the file name
log_file = open(file_name, 'r')   # open the log file for reading

data_log = []                     # list of data

while True:                       # loop to read file line by line
    line = log_file.readline()    # read one line from the file
    line = line.strip('\n')       # remove line break from the line
    if line == '':                # line is empty -> end reading loop
        break
    data = line.split(';')        # split line items using ;
    for item in data:             # iterate all line items
        item = float(item)        #    convert to float
        data_log.append(item)     #    append to list of data

log_file.close()                  # close the log file

# --- plot chart ---
t = data_log[0::3]                # get sub-list of time values
s = data_log[2::3]                # get sub-list of s-values (distance)

plt.plot(t, s)                    # plot the chart
plt.show()                        # display the plot
```
@LIA.python

### Code Explanation

The program performs the following steps:

1. **Import matplotlib:** For creating charts and plots
2. **File operations:** Opens the data file in read mode
3. **Data storage:** Creates an empty list to store all data values
4. **File reading loop:** Reads the file line by line until end of file
5. **Data processing:** 
   - Removes newline characters
   - Splits each line on semicolons
   - Converts string values to floating-point numbers
   - Appends all values to a single flat list
6. **Data extraction:** Uses Python slicing to extract every 3rd element:
   - `data_log[0::3]` gets time values (positions 0, 3, 6, 9, ...)
   - `data_log[2::3]` gets distance values (positions 2, 5, 8, 11, ...)
7. **Visualization:** Creates a plot showing distance vs. time

---

## Learning Objectives and Metadata

| **Learning objective**                         | **Task type**   | **Complexity** |
| ---------------------------------------------- | --------------- | -------------- |
| understand reading text files into data structure | worked-out example | 3 - high       |

### Previous Knowledge Required

- **vcp-1, vcp-2:** print, variable, data type conversion  
- **str-2:** important string operations  
- **branch-1:** basic if statements  
- **loop-2:** while-break loop  
- **list-1, list-2:** basic list operations, slicing  
- **func-1, func-2:** function calls, import modules
- **file-1:** basic file reading  

### Learning Activities

1. Understand content of the text file
2. Read and run the given Python code
3. Write comments to the code to demonstrate understanding
4. Explain the code to another student or colleague

### Supporting Information

**Online Resources:**
- [GeeksforGeeks: Text Files in Python](https://www.geeksforgeeks.org/reading-writing-text-files-python/)
- [Python-Kurs.eu: Dateien](https://www.python-kurs.eu/python3_dateien.php)

**Books:**
- Matthes, E. (2019). Python crash course a hands-on, project-based introduction to programming (2nd edition). No Starch Press.: Chapter 10, pages 183-198  
- Theis, T. (2017). Einstieg in Python. In Rheinwerk Computing (5., aktualisierte Auflage). Rheinwerk Verlag GmbH.: Kapitel 8, Seiten 257-270

---

## Extended Exercise: Data Analysis

Try modifying the code to also plot velocity vs. time:

```python
import matplotlib.pyplot as plt

file_name = 'FreeFall.txt'
log_file = open(file_name, 'r')

data_log = []

while True:
    line = log_file.readline()
    line = line.strip('\n')
    if line == '':
        break
    data = line.split(';')
    for item in data:
        item = float(item)
        data_log.append(item)

log_file.close()

# Extract all three data series
t = data_log[0::3]  # time
v = data_log[1::3]  # velocity
s = data_log[2::3]  # distance

# Create subplot with two charts
fig, (ax1, ax2) = plt.subplots(2, 1, figsize=(8, 6))

# Plot distance vs time
ax1.plot(t, s, 'b-', label='Distance')
ax1.set_ylabel('Distance (m)')
ax1.set_title('Free Fall Experiment Data')
ax1.grid(True)
ax1.legend()

# Plot velocity vs time
ax2.plot(t, v, 'r-', label='Velocity')
ax2.set_xlabel('Time (s)')
ax2.set_ylabel('Velocity (m/s)')
ax2.grid(True)
ax2.legend()

plt.tight_layout()
plt.show()

# Print some statistics
print(f"Final velocity: {v[-1]:.2f} m/s")
print(f"Final distance: {s[-1]:.2f} m")
print(f"Total time: {t[-1]:.2f} s")
```
@LIA.python

---

**Course Credits:**  
Author: Sebastian Zug (converted from Robert Ringel's original work)  
Original Author: Robert Ringel, Faculty Informatics/Mathematics, HTWD - University of Applied Sciences  
Version: 1.0.0  
License: CC BY-SA 4.0