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
# add a constant integer
```python
import numpy as np
import sys
aa = np.loadtxt('out.txt')
sys.stdout=open("1stcolumn.txt","w")
aa = np.loadtxt('out.txt')
sys.stdout=open("1stcolumn.txt","w")
for i in aa[:,:3]:
    if int(i[0]) > 33:
        i[0] = i[0]+18
        
        print(int(i[0]),int(i[1]),float(i[2]))
        
    else:
              
        i[0]=i[0]
        
        print(int(i[0]),int(i[1]),float(i[2]))
        
sys.stdout.close()
bb = np.loadtxt('1stcolumn.txt')
sys.stdout=open("2ndcolumn.txt","w")
for i in bb[:,:3]:
    if int(i[1]) > 33:
        i[1] = i[1]+18
        
        print(int(i[0]),int(i[1]),float(i[2]))
        
    else:
              
        i[1]=i[1]
        
        print(int(i[0]),int(i[1]),float(i[2]))
        
sys.stdout.close()
cc = np.loadtxt('2ndcolumn.txt')
sys.stdout=open("1stcolumn1.txt","w")
for i in cc[:,:3]:
    if int(i[0]) > 360:
        i[0] = i[0]+22
        
        print(int(i[0]),int(i[1]),float(i[2]))
        
    else:
              
        i[0]=i[0]
        
        print(int(i[0]),int(i[1]),float(i[2]))
        
sys.stdout.close()
dd = np.loadtxt('1stcolumn1.txt')
sys.stdout=open("2ndcolumn1.txt","w")
for i in dd[:,:3]:
    if int(i[1]) > 360:
        i[1] = i[1]+22
        
        print(int(i[0]),int(i[1]),float(i[2]))
        
    else:
              
        i[1]=i[1]
        
        print(int(i[0]),int(i[1]),float(i[2]))
        
sys.stdout.close()
```

# change datashape from matrix to list
```python 
import numpy
aa = numpy.loadtxt('contact.dat')
aa
aa.shape
for i in range(464):
    for j in range(464):
        print(i,j,aa[i,j])
	aa>0
```
	
# using rosetta
#exporting path
```
export PATH="$PATH:/ufrc/alberto.perezant/arup.mondal/Source/Rosetta/rosetta_bin_linux_2019.14.60699_bundle/main/source/bin"
```
#to get score of a pdb
```
score.static.linuxgccrelease -in:file:s *****.pdb -in:file:fullatom
```
#to replace HIE with  HIS
```
for a in unique.c*.pdb;
do
sed 's/HIE/HIS/g' $a >TEMP/$a;
done
```
#to get 2nd column
```
awk '{print $NF,$2}' default.sc > my_score.txt
```
#to cut some line from below after a xxxx line
```
head -xxxx unique.c0.pdb |tail
```
#to cut some lines in starting upto a certain line YYYY (as well as from below)
```
head -xxxx unique.c0.pdb |tail -(xxxx-yyyy) |head
```
#to do that in a script
```
for a in unique.c*.pdb ;
do 
head -2757 $a |tail -2613 > TEMP2/$a;
done
```
# open a .tgz file
```bash
tar xvzf file.tgz
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
