# Single server with infinite capacity (M/M/1):(oo/FIFO)
## Aim :
To find (a) average number of materials in the system (b) average number of materials in the conveyor (c) waiting time of each material in the system (d) waiting time of each material in the conveyor, if the arrival  of materials follow poisson process with the mean interval time 12 seconds, serivice time of lathe machine follows exponential distribution with mean serice time 1 second and average service time of robot is 7seconds.

## Software required :
Visual components and Python

## Theory:
Queuing are the most frequently encountered problems in everyday life. For example, queue at a cafeteria, library, bank, etc. Common to all of these cases are the arrivals of objects requiring service and the attendant delays when the service mechanism is busy. Waiting lines cannot be eliminated completely, but suitable techniques can be used to reduce the waiting time of an object in the system. A long waiting line may result in loss of customers to an organization. Waiting time can be reduced by providing additional service facilities, but it may result in an increase in the idle time of the service mechanism.

![image](1.png)

This is a queuing model in which the arrival is Marcovian and departure distribution is also Marcovian,number of server is one and size of the queue is also Marcovian,no.of server is one and size of the queue is infinite and service discipline is 1st come 1st serve(FCFS) and the calling source is also finite.

## Procedure :

![imAGE](2.png)



## Experiment:


 
## Program
```
import numpy as np
import math
import scipy.stats

L = [int(i) for i in input().split()]
N = len(L)
M = max(L)
X = []
f = []

for i in range(M + 1):
    c = 0
    for j in range(N):
        if L[j] == i:
            c = c + 1
    f.append(c)
    X.append(i)

sf = np.sum(f)
p_observed = []

for i in range(M + 1):
    p_observed.append(f[i] / sf)

mean = np.inner(X, p_observed)

p = []
E = []
xi = []

print("X   P(X=x)   Obs.Fr   Exp.Fr   xi")
print("--------------------------")

for x in range(M + 1):
    p.append(math.exp(-mean) * mean**x / math.factorial(x))
    E.append(p[x] * sf)
    xi.append((f[x] - E[x])**2 / E[x])
    print("%2.2f %2.3f %4.2f %3.2f %3.2f" % (x, p[x], f[x], E[x], xi[x]))

print("-------------------")

cal_chi2_sq = np.sum(xi)
print("Calculated value of chi square is %4.2f" % cal_chi2_sq)

table_chi2 = scipy.stats.chi2.ppf(1 - .01, df=M)
print("Table value of chi square at 1 level is %4.2f" % table_chi2)

if cal_chi2_sq < table_chi2:
    print("The given data can be fitted in poisson distribution at 1% LOS")
else:
    print("The given data cannot be fitted in poisson distribution at 1% LOS")
```

## Output :
<img width="809" height="352" alt="Screenshot 2026-03-09 102651" src="https://github.com/user-attachments/assets/2cef112e-f88e-4bca-874d-5002c1662ead" />


## Result :
The average number of material in the system and in the conveyor and waiting time are successfully found.

