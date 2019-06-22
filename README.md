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
# replace a character 
```
:n-line/m-lines/old/new/g
```
# meld restart after time out
```bash
prepare_restart --prepare-run (#then submit the jobscript again)
```
# meld adding frame
```python
import pickle
import shutil
from meld.system import restraints

# backup old files
shutil.copy("remd_runner.dat", "remd_runner.dat.before_extend")
shutil.copy("system.dat", "system.dat.before_extend")

# add an extra 500 ns
runner = pickle.load(open("remd_runner.dat", "rb"))
runner._max_steps += 10000
pickle.dump(runner, open("remd_runner.dat", "wb"))
#this script should be run in Data/Backup directory
```
# meld extract last trjectory
```bash
extract_trajectory extract_last last (#will be saved last.00.pdb , last.01.pdb..)
```

# minimization
```bash
relax.static.linuxgccrelease -database /ufrc/alberto.perezant/arup.mondal/Source/Rosetta/rosetta_bin_linux_2019.14.60699_bundle/main/database -s S_00000937.pdb -relax:fast
```
# fargment picking
```bash
fragment_picker.static.linuxgccrelease -in::file::vall /ufrc/alberto.perezant/arup.mondal/Source/Rosetta/rosetta_bin_linux_2019.14.60699_bundle/main/database/sampling/filtered.vall.dat.2006-05-05.gz -in::file::fasta seq.fa -frags::ss_pred seq.ss2 psipred

```
# Extracting pdb from silent file
```bash
extract_pdbs.static.linuxgccrelease -in::file::silent default.out -in::file::tags S_00000025
```
# 2d scatter plot 
```python
import numpy as np
import os
import pandas
import matplotlib
matplotlib.use('Agg')
from matplotlib import pyplot
aa = np.loadtxt('trimer_matrix.txt')
num = np.loadtxt('trimer_modified_clean.txt')
pyplot.figure()
pyplot.imshow(aa,cmap='Greys',alpha=0.8,vmin=0)
pyplot.scatter(num[0],num[1],c=num[2],cmap='cool',s=num[2])
pyplot.savefig('trimer.png')
```
# list to matrix
```python
import numpy as np
from pandas import DataFrame as df
import sys
aa = np.loadtxt('pdb_modified_clean.txt')
aa.shape
out_matrix = np.zeros( (443,443) )
for i in aa[:,:3]:
    if float(i[2]) > 0:
        out_matrix[int(i[0]),int(i[1])] = i[2]
        out_matrix[int(i[1]),int(i[0])] = i[2]
np.savetxt('out_matrix.txt',out_matrix)
```

# ignoring nearby contacts
```python
import numpy as np
from pandas import DataFrame as df
import sys
num = np.loadtxt('pdb_modified.txt')
sys.stdout=open("pdb_modified_clean.txt","w")
for i in num[:,:3]:
    if abs(i[0]-i[1]) > 3:
        print(int(i[0]),int(i[1]),float(i[2]))
sys.stdout.close()

```
# add a constant integer
```python
import numpy as np
import sys
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
