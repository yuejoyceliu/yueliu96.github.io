---
title: Hyak Tips
date: 2018-12-31 13:41:04
tags:
- Hyak
categories:
- Turecek Lab Tutorial
---

Tips on: [file transfer](#scp) | [memory & disk space](#memdisk) | [python scripts](#pyscripts) | [Run python: No such file or directory](#nofile) | [squeue format](#squeue) | to be continue...

Hyak Mox Overview website: [click me](https://wiki.cac.washington.edu/display/hyakusers/Hyak+mox+Overview)

# <jump id='scp'>File Transfer</jump>

- from ikt to mox
  
  ```
  hyakbbcp myfile mox1.hyak.uw.edu:mydirectory
  hyakbbcp -r myfolder mox1.hyak.uw.edu:mydirectory
  ```

- from mox to ikt

  ```
  hyakbbcp myfile ikt1.hyak.uw.edu:mydirectory
  hyakbbcp -r myfolder ikt1.hyak.uw.edu:mydirectory
  ```
- into hyak
  
  ```
  scp myfile user@mox.hyak.uw.edu:path/of/destination
  ```
- out of hyak
  
  ```
  scp user@ikt.hyak.uw.edu:path/of/your/file .
  ```

- into or out of hyak by sftp
  
  ```bash
  sftp user@mox.hyak.uw.edu
  get myfile   #move myfile from hyak to local direcotry
  get -r myfolder 
  put myfile   #move myfile from local directory to hyak
  put -r myfolder
  ls           #list files and folders on hyak directory
  lls          #list files and folders on local directory
  ```

# <jump id='memdisk'>Memory and Disk Space</jump>

- Commonality
  - Place to hold data
  - Unit: bytes, kilobytes, megabytes, etc
- Difference
  - Memory is known as random access memory (RAM), which stores actively running programs on the computer. The more memory is, the more it is able to run complex programs and more programs at the same time.
  - Disk space is a spindle of magnetic discs to store files you download, install or save.
- Command
  - mem: `free -g` (g:GB,m:MB,k:KB)
  - disk space: 
    - `df -h`
    - Hyak has usage_report.txt available on every partition (e.g. /gscratch/stf/usage_report.txt) recording the disk space usage. One can quickly know the usage by writing a simple python scripts:
    
    ```python
    #!/usr/bin/env python

    PTT = ['stf','chem','ilahie','scrubbed']
    try:
        print('%-10s%-12s%-12s%-12s%-12s%-15s%-16s' % ('Name','Use(GB)','Quota(GB)','Limit(GB)','Files','FilesQuota','FilesLimit'))
        for p in PTT:
            f = '/gscratch/'+p+'/usage_report.txt'
            with open(f,'r') as fo:
                lines = fo.readlines()
            s = lines[2].split()
            print('%-10s%-12s%-12s%-12s%-12s%-15s%-16s' % (s[0],s[2],s[3],s[4],s[6],s[7],s[8]))
    except BaseException as err:
        print(err)
    ```

    If store it to [gscratch_space.py](https://github.com/yueliu96/scripts_for_lab/blob/master/gscratch_space.py) in the home directory and run this script as `~/gscratch_space.py`, we can get:
    
    ```txt
    Name      Use(GB)     Quota(GB)   Limit(GB)   Files       FilesQuota     FilesLimit      
    stf       24437       45500       50050       3064981     68250000       75075000        
    chem      8884        9000        9900        2327984     9000000        9900000         
    ilahie    29325       35500       39050       1522158     53250000       58575000     
    scrubbed  91518       200000      220000      12174263    200000000      220000000   
    ```

# <jump id='pyscripts'>Python Scripts</jump>

- It's a good choice to store useful python scripts in user's home directory, whose quotas are set to 10 GB with a limit of 5,000 files. 
- Python scripts starting with `#!/usr/bin/env python`, can be executed by `directory/pyfile ...` besides `python pyfile ...`. 
- Use `chmod u+x pyfile` if it isn't executable
- Batch operation of python scripts by bash command `for ...; do ...; done`
  - example: 
   
     If *xyz2gjf$.$py* (usage: `python xyz2gjf.py xyz-file` )is in a subdirecotry *myscripts* of home directory, run `chmod u+x ~/myscripts/xyz2gjf.py` first if it is not executable, move to a directory containing several xyz files and run `for i in *xyz; do ~/myscripts/xyz2gjf.py $i; done` to convert all *xyz files to gjf format.

# <jump id='nofile'>Run python: No such file or directory</jump>

If python scripts can be executed with `python script.py` but fails with `./script.py`:

- Make sure add `#!/usr/bin/env python` at the head of the script
- Make sure use `chmod u+x script.py` to make it executable

If it still fails:

- `vi scripts.py` to open it
- `:set ff=unix` to change it file format
- `:wq` to save it

# <jump id='squeue'>Squeue Format</jump>

add `export SQUEUE_FORMAT="the-format-you-like"` to ~/.bash_profile file and then run `source ~/.bash_profile`

- My own version:
  
  ```bash
  export SQUEUE_FORMAT="%.7i %9P %15j %.8u %.2t %.12M %.12L %.5C %.7m  %.4D %R"
  ```
    what is like:

    ```
      JOBID PARTITION NAME          USER ST         TIME    TIME_LEFT  CPUS MIN_MEM  NODE NODELIST(REASON)
     547841 chem      gN1_ccsd  yueliu96  R   1-23:14:00  10-12:46:00    28    245G     1 n2079  
    ```
- Note:
  - `%.`: align rigt
  - `%` withou dot: aligh left
  - integer: length of occupied space
  - different letters correspond to diffrent items, see [link](https://slurm.schedmd.com/squeue.html) for details

