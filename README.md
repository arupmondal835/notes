# create table of content
```js
console.log( '\n\n\n # Table of contents\n\n' + Array.from(document.querySelectorAll('h1 > a, h2 > a, h3 > a')).map((a) => ( {'H1':' * ','H2':' * ','H3':' - '}[a.parentNode.tagName] + `[${a.parentNode.innerText.trim()}](${a.hash})` )).join('\n') + '\n\n\n' );
```

# how to transfter data between two remote server
```
1. log in to a server where you want to copy the data
2. scp -r arup.mondal@hpg2.rc.ufl.edu:/ufrc/alberto.perezant/arup.mondal/move.sh chemistry/
use -r for for another remote server, then use the server name and path for the file and then in the end the 
desitination in the currect logged in server
```


# convert a color pdf to b/w pdf
```bash
gs \
 -sOutputFile=output.pdf \
 -sDEVICE=pdfwrite \
 -sColorConversionStrategy=Gray \
 -dProcessColorModel=/DeviceGray \
 -dCompatibilityLevel=1.4 \
 -dNOPAUSE \
 -dBATCH \
 input.pdf
 ```

# extracting energy values from post analysed file in amber
```bash
awk -f get_energy.awk file

##file is

BEGIN{
    s = 0
}
{
    if ($0 ~ /^ BOND/) {
        s += $3 + $6 + $9
    }
    if ($0 ~ /^ VDWAALS/) {
        s += $3 + $6 + $9
    }
    if ($0 ~ /^ 1-4 VDW/) {
        s += $4 + $8 + $11
        printf "%f \n", s
        s = 0 
    }
}


```

# black line after each line
```
sed -e 'G' a.dat
```

# swap two column
```
%s/\v^(\S+)\s+(\S+).*$/\2 \1/
```

# delete all blank line
```
:g/^$/d
```

# gnuplot
```bash
module load gnuplot
gnuplot
plot "trial_4_res_87_300K/topten.dat" ,  "trial_4_res_87_350K/topten.dat" , "trial_4_res_87_400K/topten.dat" , "trial_4_res_350_300K/topten.dat" , "trial_4_res_350_350K/topten.dat" , "trial_4_res_350_400K/topten.dat" , "trial_4_res_700_300K/topten.dat" , "trial_4_res_700_350K/topten.dat" , "trial_4_res_700_400K/topten.dat"
```

# 
```
cut -d ' ' --complement -f -10 paste.dat
```
# deleting some space separated column
```
cut -d" " -f1,2 T0968s2_ECs.txt >contacts.dat
```
# appending files columnwise
```
paste rmsd.txt p.dat | column -s $'\t' -t
```

# visualizing replica exchange
```
analyze_remd visualize_trace
analyze_remd visualize_fup
```
# extracting the last pdb from traj
```

extract_trajectory extract_last last  #it will save pdbs as last.00.pdb.........last.30.pdb
```

# meld with NMR data
# getting rmsd using cpptraj
```bash
trajin step4_1.nc 1 500 1
parm clean_update.pdb
reference clean_update.pdb parm clean_update.pdb
autoimage :1-170
rms reference :3-165.CA :3-165.CA out rmsd_test.plo
rms reference :100.CA :100.CA nofit out rmsd_test2.plo
trajout testrmsd.pdb onlyframes 500
run
quit
```


# deleteing any common thing from a vi file globally
```
:%s/_[A-Z]//g
```
# checking resoures available for group
```
sacctmgr show qos alberto.perezant format="Name%-16,GrpSubmit,MaxWall,GrpTres%-45"
```
# space separated to tab 
```
sed 's/ /\t/g' test.log
```
# deleting few tab sepated column
```
cut -f1,2 tab_ec.txt   #it will keep column 1 and 2 and will dlt everything else
```
# tab sep to space sep
```
sed 's/\t/ /g' test_ec.txt
```
# adding prefix and suffix
```
sed 's/^/I am a /; s/$/ 128... [}/' file.txt
```

# add multiple linux account
```
go to users and then allow it to be chane by hitting unlock button then click on add user.
```
# checking the priority oof submitted job
```
squeue -o "%.18i %.9P %.8j %.8u %.2t %.10M %.6D %R %p %Q" |egrep "lijun|arup|alberto"
squeue -o "%.18i %.9P %.8j %.8u %.2t %.10M %.6D %R %p %Q" |egrep "lijun|arup|alberto" |grep " R "  |wc -l
```

# deleting blank space in the begining of lines in vi file
```inside vi file
:%s/^ \+//g        # space after ^ is important. depneding on number of space you need to dlt, in command oyu should use that many space, and for selected area say line m to n....:m,ns/^ \+//
```

# login to desktop from mac
```
ssh arup@am.yyrcd.com
```
# installing sshfs in mac
```
xcode-select --install
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" < /dev/null 2> /dev/null ; brew install caskroom/cask/brew-cask 2> /dev/null
brew cask install osxfuse
brew install sshfs
```

# removing space from .png and adding multiple png file
```
convert input.png -trim output.png

convert +append 1st.png 2nd.png final.png
```
# making a column from a string and nmber them
```bash
for a in `cat binary.txt `
do echo $a
done                    #for numberig just do nl myfile
```

# adding a constant integer to all number of a vi file
```inside file command
ctrl-v to and drag mouse to select all the numbers(those numbers you want to add integer to)
shift+colon
#some <> sign will show there and it s=hould be erased
then add :%s/\d\+/\=submatch(0)+1/g   #1 because I wanted to add 1

```
# jnb in hipergator
```
ssh -L 2018:localhost:2018 arup.mondal@hpg2.rc.ufl.edu
```

# installing vmd in ubuntu
```
#download vmd file from official site
cd Downloads
tar xvf ......tar.gz #eventhouth it's .gz, it is not a zip file
cd vmd-1.9.3
./configure LINUXAMD64  #before this sometime we might need to do $install_bin_dir and $install_library_dir
cd src
sudo apt-get update #for 1st time, other wise 'make' can not be installed
sudo apt-get install make 
sudo make install
```
# space after one character in vi file
```
:%s/\(.\)/\1 /g      #apace after 1 is important and one . is for one spacing after 1 character
```
# seach and repalce a string
```bash
:s/[A-Z]/new/g   # for replacing all character not number
```
# regular expression with python
```python
import re 
text="MNQSRRILRTVYLSLFLIGLFMLINDIFSSNILSSKSSDKEVQFDLNKSFDDNEMSSVKSNSFNLINKSQDIIVETGIYVATFSTFKGNLVSLKLKNHLNLEKNPTDLINIDRKNETFFDISFDYFVDDLFLYKKIDDFNHEFKAYFKNNGKTYEYVKKYTFSKKDEYLMQFKVTVNGLEDYNLFDFDSYKIIFSSEIERLSDKAKLQYNNYLSQIIYYDNKLKYGKDGLRINNPRWIGSSTKYFGVLVSKENMEVEFKKERGTLKSFIINNVRNKKNISDEFFIYAGPKDNRYLDVFDKRDDNTFGLFDIFFGMSVEKSFWYLIQVPMQMVMQVFYDVIPNWGLSIIFLTIVVRILIFPLTFKGFRATAELSKLQPKMKELQAKFKHDPKKLNEEMGRLYKEEGVNPLGGCLPVILQLPIFFALYSLVNNLFLLRGASFIPGWIDDLSIGDSVYHFGYKLYFVSWTDIRILPFIMMFTQLGSTIVSSNMDLKNLGAQQKFLYFGMPIMFFFILYNMPSGLLIYWITTNIFTILQQYYIKMHLS"
result = re.findall(r"L[A-Z]{1,5}Q[A-Z]{1,5}K$", text)
print(result)
```

# Search a motif:: regular expression
```sublime text
K[A-Z]{1,5}X[A-Z]{1,5}P  #crtl+f then select regex then type this command
[K/R][A-Z]{1,5}[Y/F][A-Z]{1,5}[V/L] #CARC domain
[V/L][A-Z]{1,5}Y[A-Z]{1,5}[K/R] #CRAC domain
```
# reverse the order of all caharcter in all line 
```
sed '/\n/!G;s/\(.\)\(.*\n\)/&\2\1/;//D;s/.//' filename
```
# appending file
```
cat file.out >> CRAC_CARC.dat
```
# replace a character ina certain range of a vi file
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
# space after 3 character
```
sed 's/.\{3\}/& /g' originalfile >newfile
```
# removing column
```bash
awk 'NF{NF-=1};1' <ec.txt >ec.dat
```

# restart to pdb
```bash
$AMBERHOME/bin/ambpdb -p cram.prmtop -c min_qmmm.rst > min_qmmm.rst.pdb 
```

# sshfs
```bash
sshfs arup.mondal@hpg2.rc.ufl.edu:/ufrc/alberto.perezant/arup.mondal Mountpoint
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
