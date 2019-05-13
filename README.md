 # Table of contents

 * [Table of contents](#table-of-contents)
 * [create table of content](#create-table-of-content)
 * [restart to pdb](#restart-to-pdb)
 * [sshfs](#sshfs)
 * [float to int](#float-to-int) 

# create table of content
```js
console.log( '\n\n\n # Table of contents\n\n' + Array.from(document.querySelectorAll('h1 > a, h2 > a, h3 > a')).map((a) => ( {'H1':' * ','H2':' * ','H3':' - '}[a.parentNode.tagName] + `[${a.parentNode.innerText.trim()}](${a.hash})` )).join('\n') + '\n\n\n' );
```
# vmd
```
resid number means whatever written in the pdb file next to the amino acid
residue number means it will count the 1st amino acid in pdb as zeroth amino acid and it will count continuously no matter what is written next to each amino acid.
```
# SSHFS command 
```
sshfs arup.mondal@hpg2.rc.ufl.edu:/ufrc/alberto.perezant/arup.mondal Hipergator/
```
# space after 3 character
```
sed 's/.\{3\}/& /g' originalfile >newfile
```
# removing column
```bash
awk 'NF{NF-=1};1' <ec.txt >ec.dat
```
# replacing character
```
sed -i 's/old/new/g' myfile
```
# cutting some line

```
sed -i '12,100d' myfile
```




# restart to pdb
```bash
$AMBERHOME/bin/ambpdb -p cram.prmtop -c min_qmmm.rst > min_qmmm.rst.pdb 
```

# sshfs
```bash
sshfs jklsdjf@jkfjal
ajklsdfk
adfjkljasd
```
# float to int
```python
from __future__ import division
import matplotlib.pyplot as plt
import numpy as np
import sys
#import pandas as pd
from pylab import plot, ylim, xlim, show, xlabel, ylabel, grid
from numpy import linspace, loadtxt, ones, convolve
filename= 'contacts.dat'

f = open(filename, "r")
lines = f.readlines()
time=[]
energy =[]
#running_std=[]
for line in lines:
	line = line.strip()
	line = line.split(" ")
	line = [float(i) for i in line if i!=""]
	time.append(int(line[0]))
	energy.append(int(line[1]))
#	running_std.append(np.std(energy))
print(time)
print(energy)

file = open("testfile.dat","w") 

for i in range(len(time)):
    file.write('%d %d\n'%(time[i], energy[i]))

file.close() 
```
