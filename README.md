# Fitting Poisson  distribution
# Aim : 

To fit poisson distribution for the arrival of objects per minute from the feeder

# Software required :  

Python and Visual component tool

# Theory:

The Poisson distribution is the discrete probability distribution of the number of events occurring in a given time period, given the average number of times the event occurs over that time period.

![image](https://user-images.githubusercontent.com/104613195/166248326-fd042076-8b0b-40c4-8b11-1d8e8fcb74db.png)

 Conditions for Poisson Distribution:

1. An event can occur any number of times during a time period.
2. Events occur independently. I
3. The rate of occurrence is constant.
4. The probability of an event occurring is proportional to the length of the time period. 
 
# Procedure :

![image](https://user-images.githubusercontent.com/104613195/166251988-d0c53205-6080-4f7b-ae4c-398178586637.png)

# Program :
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
            c += 1
    f.append(c)
    X.append(i)

sf = np.sum(f)

p = []
for i in range(M + 1):
    p.append(f[i] / sf)

mean = np.inner(X, p)

p = []
E = []
xi = []

print("X   P(X=x)  Obs.Fr  Exp.Fr  xi")
print("--------------------------------")

for x in range(M + 1):
    px = math.exp(-mean) * mean**x / math.factorial(x)
    p.append(px)

    expected = px * sf
    E.append(expected)

    chi_term = ((f[x] - expected) ** 2) / expected
    xi.append(chi_term)

    print("%2d  %.3f   %4d   %.2f   %.3f" % (x, px, f[x], expected, chi_term))

print("--------------------------------")

cal_chi2_sq = np.sum(xi)
print("Calculated Chi-square = %.4f" % cal_chi2_sq)

df = M
table_chi2 = scipy.stats.chi2.ppf(1 - 0.01, df=df)
print("Table Chi-square (1%% LOS) = %.4f" % table_chi2)

if cal_chi2_sq < table_chi2:
    print("Result: Data fits Poisson distribution at 1% LOS")
else:
    print("Result: Data does NOT fit Poisson distribution at 1% LOS")
```

 

# Output : 
<img width="702" height="482" alt="{2B4B368A-D2C5-485C-B26C-6C02DB128B43}" src="https://github.com/user-attachments/assets/e13278fb-db6b-4ae9-a3a9-b874ee05a457" />




# Results

The Poisson distribution is fitted for the objects arrived from feeder per minute and the data is tested using Chi-square test. 
 
