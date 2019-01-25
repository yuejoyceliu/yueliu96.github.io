---
title: Newton-X on Hyak
date: 2018-12-30 20:30:09
tags:
- Hyak
- ComputChem
- software
categories:
- Turecek Lab Tutorial
---

*[Newton-X](http://www.newtonx.org) is a general-purpose program package for excited-state molecular dynamics, which is used to simulate absorption spectrum with GAUSSIAN09 in our group.*

*Input-file setup and output analysis are introduced here or could be found on its website. A fast setup could be achieved by [my python script](#pscript). Scripts attached here can run both in python2 and in python3.*

# Newton-X Setup

## Procedures

### 1. geometry and normal mode input

In the working directory prepare two files: one is the optimized geometry in gaussian input format and the other is the normal mode calculation output file (gaussian frequency log file, usually calcuated with b3lyp method):

`opt.gjf  freq.log`

### 2. load newton-x environment

To work in the newton-x environment on Hyak, run `module load contrib/newtonX` or `module load contrib/newton-x`. Their difference is that newton-x contains other package like gaussin09. 

We can check if we load successfully by command `$NX`, which should produce an info `-bash: /sw/contrib/newtonX/NX-2-B17/bin: Is a directory`. Or run `module list` to see all packages availabe to use.

### 3. convert optimized geometry into newton-x format

Convert optimized geometry (opt.gjf) into xyz format first, could be achieved by script [gjfcom2xyz.py](https://raw.githubusercontent.com/yueliu96/scripts_for_lab/master/gjfcom2xyz.py): `python gjfcom2xyz.py opt.gjf`. opt.xyz could be produced.

`$NX/xyz2nx < opt.xyz` generates newton-x geometry file named *geom*, whose second column is the atomic number, the following three columns are x, y and z coordinates in atomic units (*Bohr*) and the last one contains the atomic masses.

### 4. newton-x working directory

Creat a new directory *TDDFT_SPEC* in the working directory, copy/move *geom* to it, copy/move *freq.log* to it with a new name *freq.out*: 

```
mkdir TDDFT_SPEC
mv geom TDDFT_SPEC
cp freq.log TDDFT_SPEC/freq.out
```

### 5. energy and transition moment input

Move to the directory *TDDFT_SPEC* and create a new subdirectory called *JOB_AD*. Move into *JOB_AD* and prepare two files named, *basis* and *gaussian$.$com*. 
*basis* contains the basis set information, like `6-31+g(d,p)`. *gaussian$.$com* is same with the very first optimized geometry file *opt.gjf* but with different link command lines and route card, like (%rwf and %nosave could be deleted):

```
%mem=100gb
%nprocshared=28
%rwf=gaussian
%nosave
%chk=gaussian
# TD(NStates=10) m062xd/6-31+g(d,p)  pop=none scf=(xqc,tight) Symmetry=None
```

Note that the subdirectory must be named with *JOB_AD* and the name of these two files must be *basis* and *gaussian$.$com* since Newton-X will search for them.

### 6. newton-x input

Back to the directory *TDDFT_SPEC*, use command `$NX/nxinp` and answer several quesitons by instructions to genetrate the newton-x input file *initqp_input*. Answers to the questions are `1; 2; numer of atoms; 300 (number of initial conditions); geom; 4; freq.out; 1; 310 (temperature); n; 1; 1 (ground state); number of states; 1; 100; 6.5; 0; 1; 7 (exit)`, respectively.

### 7. splitting jobs

This step is to split the job among several computers (nodes), could be skipped and go directly to run the newton-x by `$NX/initcond.pl > initcond.log`.

 To split the job, run `NX/split_initcond.pl` in the directory *TDDFT_SPEC*. Two questions will be asked, the first one is the number of directories to split the job and the second one is if the job run in a batch system. This program produces one file named *split_initcond.log* and a directory called *INITIAL_CONDITIONS*. If the answer to the first quesiton is 10, 10 subdirectories called *I1,I2,...,I10* are inside *INITIAL_CONDITIONS*, each one containing a complete set of input files but with 30 (300 $\div$ 10) initial conditions and iseed=-1 not 0.

 ### 8. submit newton-x job

In every directory containing a complete set of input files  (geom, freq.out, initqp_input and JOB_AD), create a sbatch file to submit the job to Hyak node.

```bash
#!/bin/bash
#SBATCH --job-name=???
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=28
#SBATCH --time=??:00:00
#SBATCH --mem=???G
#SABTCH --workdir=???????
#SBATCH --partition=???
#SBATCH --account=???

echo 'This job will run on' $SLURM_JOB_NODELIST
#set up time
begin=$(date +%s)

#load newtonx and gauss09 environment
module load contrib/newton-x

$NX/initcond.pl > initcond.log

end=$(date +%s)
echo 'Elapsed Time: '$(($end-$begin))'s'
```

## <jump id='pscript'>Scripts</jump>

  python script [newtonx.py](https://raw.githubusercontent.com/yueliu96/scripts_for_lab/master/newtonx.py) can do exactly what step 2 to step 8 do.

- *Usage*
  - `python newtonx.py geometry-gif-file freq-log`
- *Descriptions*
  - *TDDFT_SPEC* folder is created, which contains *geom*, *freq.log*, *initqp_input*, *split_initcond.log*, *newtonx$.$sh*, *JOB_AD*, *INITIAL_CONDITIONS*
  - *I1 I2 ...* in *INITIAL_CONDITIONS*, each subfolder containing a complete set input -- *geom*, *freq.out*, *initqp_input* (iseed=1234,2468,...), *JOB_AD* and a sbatch file -- *nx_submit.sh*
  - *nx_submit.sh* is the sbatch file same with what is listed in step 8, but with partition=ckpt, account=stf-ckpt.
  - *newtonx$.$sh* contains a list of bash command like: `cd absolute-path-of-I1; sbatch -p ckpt -A stf-ckpt --time=20:00:00 nx_submit.sh`
  - after satisfied with everything, run `bash newtonx.sh` to submit all jobs to hyak nodes; the final partition, account and time are decided by the setting in *newtonx$.$sh* even if *newtonx$.$sh* is different from *nx_submit.sh*
- *Note*
  - why ckpt?
    - increasing the number of splitting jobs speeds up the task greatly
    - [ckpt queue](https://wiki.cac.washington.edu/display/hyakusers/Mox_checkpoint) is a good choice to run short jobs that finish within 4 hours
  - why iseed=1234,2468,...,1234*n?
    - different iseed values guarantee no repeated jobs
    - iseed=-1 may generate a super large number not suit for ckpt queue
  
# Newton-X Result

## Procedures

### merge splitting jobs

After all sub-tasks finish, go to the directory *INITIAL_CONDITIONS* and run `$NX/merge_initcond.pl`. This program will ask the number of jobs to be merged and it will create a new directory called *I_merged* with merged results. All important data are in *final_optput.1.N* file, which contains transition information from state 1 to state *N*. 

### spectrum simulation

Move to this directory and proceed with the spectrum simulation by command `$NX/nxinp`. The answers to the questions it will ask are `5 (spectra); 1 (spectra); 1 (initial state); 2-N (array of final states); F (Absorption); 0 (no restriction); -1; local; 1 (random seed); lorentz; 0.1 (delta); 310 (temperature); 1; 0.005; 3; 7 (exit)`, among which delta contronls the width of the curve.

The simulated cross section using a Lorentzian line shape with phenomenological broadening $\delta=0.1eV$ is written to *cross-section.dat*, containing four columns of data -- DE/ev, lambda/nm, sigma/A^2 and +/-error/A^2.

## <jump id='pscript'>Script</jump>

All the above steps can be achieved by script [nxplot.py](https://raw.githubusercontent.com/yueliu96/scripts_for_lab/master/nxplot.py). 

- *Usage*
  - `python nxplot.py`
  -  run inside the directory *INITIAL_CONDITIONS*
- *Descriptions*
  - check if jobs completed
  - merge splitting jobs
  - spectrum simulation
  - extract the lamda and sigma columns if lamda within 0-1200nm from *cross-section.dat* and written to *cross-section.tsv*
  - plot *cross-section.tsv* if in python3 environment

