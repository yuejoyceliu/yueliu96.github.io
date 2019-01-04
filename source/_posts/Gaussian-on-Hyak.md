---
title: Gaussian on Hyak
date: 2018-12-16 20:54:49
tags: 
- Hyak
- ComputChem
- software
categories:
- Turecek Lab Tutorial
---

*Here introduces how to setup Gaussian input file, submit it to [Hyak](https://wiki.cac.washington.edu/display/hyakusers/WIKI+for+Hyak+users) (super computer server) and analyze the output file by my python scripts. Scripts attached here are not limited by python versions.*

# Gaussian 16 Input

[Gaussian 16 input](http://gaussian.com/input/) consists of a series of lines in an ASCII text file. In general, the input is free-format and case-insensitive; comments start with an exclamation point(!), could be anywhere on a line; spaces, commas, tabs and forward slashes are all considered as valid delimiters (multi spaces are treated as a single demiliter); keyword=option,kw(op),kw=(op1,op2,...) and kw(op1,op2) are all correct. The common suffixes of the input file are gjf and com. The basic structure includes several different sections:

## <font size=3>[Link 0 Commands](http://gaussian.com/link0/)</font>
- locate and name scratch files 
- not blank line terminated
- examples
  - %LindaWorker
    - add it when using 2 or more nodes on Hyak
  - %NProcShared=*N*
    - use up to N processors/cores on shared memory on one node
    - default: 28 on Hyak-mox, 16 on Hyak-ikt
  - %UseSSH
    - start linda workers by ssh instead of rsh(default)
    - rsh, remote shell, can execute command on another computer as another user
    - ssh: a more secure way to communicate between computers
    - some parallel jobs may mess up by using rsh
  - %Mem=*N*
    - set the dynamics of memory, can follow by MB,GB,etc. 800mb for g16 by default
    - some gaussian jobs will select the appropriate algorithm automatically based on the setting of %Mem and [MaxDisk](#maxdisk).
    - specifing more mem than availble will cause very poor performance; leave several GBs for operating system
  - %RWF=*file*
    - locate and name the  read-write file, a super huge file, used to [restart](http://gaussian.com/restart/) a job(not need for opt)
    - usually followed by *`%NoSave`*, everything before nosave will deleted if job completes normally
    - a suggested location  on Hyak is [`/gscratch/scrubbed/` ](https://wiki.cac.washington.edu/display/hyakusers/Hyak_disk_quota)
    - how to locate it if not include %RWF(Hyak version):
      - all scratch files are at [`/scr/`](https://wiki.cac.washington.edu/display/hyakusers/Managing+your+Files#ManagingyourFiles-HomeDirectories) of the local node ( `ssh nodenumber` to enter that node)
      - the scratch disk of that node will be cleaned up after walltime runs out 
      - general version and more about restarting opt and freq jobs: [*click  me*](http://gaussian.com/faq2/)
    - Related key word: [MaxDisk](#maxdisk)
  - %Chk=*file*
    - locate and name the checkpoint file
    - used to restart jobs(especially [opt](#rstopt)), [add more states for td](#addtd) and [visualize molecular orbitals for td](#vistd)
  - %OldChk=*file*
    - use with *`%Chk=newfile`*: copy *file* to *newfile* and then write new chk info to *newfile*

## <font size=3>[Route section (# lines)](http://gaussian.com/route/)</font>
- job type and method
- blank line terminated
- examples
  - print form
    - *`#N`*: normal print, by default if not specify
    - *`#P`*: print more info
    - *`#T`*: terse print 
  - job type
    - *[SP](http://gaussian.com/sp/)* : single point energy, by default if not specify
    - *[OPT](http://gaussian.com/opt/)* : geometry optimization
    - *[FREQ](http://gaussian.com/freq/)* : vibrational frequency and thermal information
    - *[TD(NStates=n)](http://gaussian.com/td/)* : calculate n excited transitions
  - other keywords
    - [POP](http://gaussian.com/population/)
      - charge and spin distribution
      - `pop=min` by default except guess=only
    - [SCF](http://gaussian.com/scf/)
      - control the functioning of the SCF procedure
      - `scf=tight` by default
      - `scf=xqc` is helpful for difficult conversion case
      - `NoSymm` or `Symmetry=None`: release orbital symmetry constraints
    - [SCRF](http://gaussian.com/scrf/)
      - in the presence of solvent, place solute in a cavity within the solvent reaction field.
       - `scrf=pcm` by default
       - ex: `scrf=(pcm,solvent=water)`
    - [CacheSize](http://gaussian.com/cachesize/)
      - the amount of cache per processor to use with various cache-blocking algorithms (in 8-byte words)
      - ex: from `/proc/cpuinfo` find the cache available(35840kb) and a good value is its 50% ( $35840\times1024\div8\times50\%=2293760$): `cachesize=2293760`
    - [<jump id='maxdisk'>MaxDisk</jump>](http://gaussian.com/maxdisk/)
      - the amount of disk storage available for [scratch data](https://gaussian.com/running/?tabid=6) 
      - disk space of one node on Hyak is ~100GB. `lsblk -d` or `df -h` can show physical disk info of linux system
      - the more disk space available, the faster the evaluation, especially for MP2. Some jobs have fixed or minimum disk requirments, click [me](http://gaussian.com/maxdisk/) for more info.

## <font size=3>Title section</font>
- any descriptions within 5 lines
- avoid special character: @  #  !  –  _  \  control characters (especially Ctrl-G)
- blank line terminated

## <font size=3>[Molecule specification](http://gaussian.com/molspec/)</font>
- charge, multiplicity, atoms and coordinates
  - multiplicity
    - number of possible spin orientations of the total spin
    - mp=2S+1, S($\alpha$ electron)=0.5, S($\beta$ electron)=-0.5
  - coordinates
    - x, y and z coordinates in angstrom
- blank line terminated

## <font size=3>Optinal additional sections</font>
- additional input
- blank line terminated

*Example:*

```
%mem=32GB
%nprocshared=28
%chk=guanosine.chk
# opt um062x/6-31+g(d,p) pop=min scf=(xqc,tight)

Complex guanosine

1 2
O       -3.094427        1.959361        0.291777
C       -4.011153        1.021154       -0.267210
C       -3.292860       -0.293751       -0.453718
O       -2.175288       -0.104229       -1.347075
...           ...             ...             ...
H       -1.180628        1.929546       -0.412585
H       -3.574938        2.742899        0.582770
H        1.100354        3.004366        0.220564
! a blank line must be here
```

# Submit to Hyak

Run ` ~/Hyak-Gaussian/gaussian-sub.py input_file`, will generate a sbatch file(suffix is sh):

```
#!/bin/bash
#SBATCH --job-name=???
#SBATCH --nodes=1

##needed if ckpt partition or  any partitions with 2 or more nodes
#SBATCH --ntasks-per-node=??

#SBATCH --time=???:00:00

##larger than %mem in input file
#SBATCH --mem=???

#SBATCH --workdir=??????
#SBATCH --partition=???
#SBATCH --account=???

##turn on email notification
#SBATCH --mail-type=ALL
#SBATCH --mail-user=???your email???

# load Gaussian environment
module load contrib/g16.b01

# debugging information
echo "**** Job Debugging Information ****"
echo "This job will run on $SLURM_JOB_NODELIST"
echo ""
echo "ENVIRONMENT VARIABLES"
set
echo "**********************************************" 

# run Gaussian
g16 ???input file???

exit 0
```

Run `sbatch *.sh` to submit it to hyak.

# Output & Analysis

## <font size=4>I. [OPT](http://gaussian.com/opt/)</font>

If key word `Tight` or `SCF` is in route card, Berny optimization will be used. This kind of output is dilimited by *GradGradGrad...*. The appearance of the following words marks completion of opt, and the final structure is displayed after that. We always want to extract the optimized standard structure for the next step calculation.

```
         Item               Value     Threshold  Converged?
 Maximum Force            0.000020     0.000450     YES
 RMS     Force            0.000004     0.000300     YES
 Maximum Displacement     0.001510     0.001800     YES
 RMS     Displacement     0.000199     0.001200     YES
 Optimization completed.
    -- Stationary point found
```

<jump id='rstopt'></jump>If `Stationary point found` is absent in log file, that means the opt job is ended earlier, maybe because of time limit. In this case, we need to write another restarted input file and submit it again to start from where it left, the route card of which should be `# opt=restart` plus the other keywords in the original input. For example: if the original route card is:`# opt ub3lyp/6-31+g(d,p) pop=min scf=(xqc,tight)` and the chk file is named as *test.chk*. The new input file is like: 

```
%UseSSH
%mem=32GB
%nprocshared=28
%chk=test.chk
# Opt=Restart ub3lyp/6-31+g(d,p) pop=min scf=(xqc,tight)
! a blank line must be here
```

### <font size=3>1. [optlog2gjfcom.py](https://raw.githubusercontent.com/yueliu96/scripts_for_lab/master/optlog2gjfcom.py)</font>

- *Usage*
  - `python optlog2gjfcom.py opt_log`
- *Descriptions*
  - Uses `Stationary point found` as a key to tell if opt finishes
  - If finished, locates `Standard orientation` after it, reads charge and multiplicity from the very end and then writes them to a new file in the form of gaussian input, named *test_opt.gjf* if original one is *test$.$com*.
  - If not  finished, checks if input file in the current directory, gets chk file name from input and then writes the restarted input file just as showed above named with *test_rst.gjf* if original one is *test.gjf*. If original input and chk files not found, it will just stop without doing anything.
- *Notes* 
  - The default route card for optimized file and link info for both optimized and restarted one are easily to change:
  
    ```
    LINK='%UseSSH\n%mem=32GB\n%nprocshared=28\n'
    ROUTE='# td(NStates=25) um062x/6-31+g(d,p) pop=min scf=(xqc,tight)'
    ```

  - A quick way to walk through all log files in one directory:
    ```
    for x in *log; do python optlog2gjfcom.py $x; done
    ```

### <font size=3>2.<jump id='hfenergies'></jump>[HFenergies.py](https://raw.githubusercontent.com/yueliu96/scripts_for_lab/master/HFenergies.py)</font>

Another important information in the output is optimized energy, which is easy to locate by key word *SCF Done*.

- *Usage*
  - `python HFenergies.py`
- *Descriptions*
  - Goes through all **.log* files in the current directory to extract energy
  - If `Stationary point found` is in the presence of log file, reads the energy after the last `SCF Done`; if not, returns energy=*NA*
  - Energies are sorted ascendingly and written to *HFenergies.csv* file with corresponding logfile name(without suffix)

## <font size=4>II. [FREQ](http://gaussian.com/freq/)</font>

*3N-6* frequecies can be found in the output file for nonlinear molecules (*3N-5* for linear molecules, *N* is the number of atoms), following by thermochemistry analysis at 298.15K, 1 atm.
Since the temperature in the Mass Spec is around 310K, we need to extrat all normal modes(frequencies), zero-point vibrational energy(ZPVE) and entropy(S) from the log file and calculate entropy and enthalpy(H) at 310K 1 atm. Also, we correct frequencies by a factor of 0.975.

*Note that the input of freq job should be the optimized structure optimized with the same method and basis set.*

### <font size=3>1.<jump id='freqthermal'></jump>[freq_thermal.py](https://raw.githubusercontent.com/yueliu96/scripts_for_lab/master/freq_thermal.py)</font>

- *Usage*
  - `python freq_thermal.py freq_log`
- *Descriptions*
  - Extracts frequencies from log file. If the first frequency is negative or freq not finished, raises error and stops.
  - Uses partition functions to calculate enthalpy, entropy and heat capacity and writes the result to file named with *test_freq.csv* if *test.log* is given.
  - *<font color=gray>explanations of calculation(to be writted)</font>*

### <font size=3>2.[CpExtractor.py](https://raw.githubusercontent.com/yueliu96/scripts_for_lab/master/CpExtractor.py)</font>

Sometimes, we only want to know the heat capacity at constant pressure. This scripts can extract Cp from all *freq.csv files.

- *Usage*
  - `python CpExtractor.py`
- *Descriptions*
  - Goes through all **_freq.csv* files in the working directory and writes the Cp and its file name into a new file *Cp.csv*
  - If Cp not found, *NA* will be there instead of a number
  
### <font size=3>3.[GibbsEnergy.py](https://raw.githubusercontent.com/yueliu96/scripts_for_lab/master/GibbsEnergy.py)</font>

After finish all opt and freq jobs, we can use energy file got from *HFenergies$.$py* and *ZPVE*, *H* and *S* from *freq_thermal$.$py* to calculate their free energies.

- *Usage*
  - `python GibbsEnergy.py energyfile`
- *Descriptions*
  - Needs energy($E_{elec}$) file got from [HFenergies.py](#'hfenergies') and corresponding *_freq.csv files got from [freq_thermal.py](#'freqthermal') in the same directory. The delimiter of all these files must be comma(by default, don't change it)
  - Reads structure's name(x) and energy from energy file. The frist row is considered as title, will be skipped. The structure with lowest energy is seen as reference.
  - Uses x find its freq file: x_freq.csv and reads its 9th row(thermal information); only reads 8th row(title info) for one **_freq.csv*.
  - $G=E_{elec}+ZPVE_{corr}+H(T)-T\cdot S(T)$ and $\Delta G=G-G_{ref}$ are used, the result in $kJ/mol$

## <font size=4>III. [TDDFT](http://gaussian.com/td/)</font>

The main output of tddft contains the excitation energies, oscillation strength(f, the intensity of that transition) and S\*\*2, listed below. A resonable transition should satisfy spin forbidden. For a doublet(multiplicity:2S+1=2) S=0.5, so S\*\*2=S(S+1)=0.75. What should be consider is that if not following that rule, the electron flips during the transiton, the total spin momentum S changes from 0.5 to 1.5, and S\*\*2=3.75. When running tddft job, the transition is a combination of these two situations, usually the more differ from what S\*\*2 should be, the less f is. In our lab, we only keep transitions whose S\*\*2<2.6, and use lorentzian equation to calcualte its absorption spectra.

```
 Excited State   1:  2.065-A      2.0123 eV  616.13 nm  f=0.0002  <S**2>=0.816
     62B -> 70B       -0.10013
     63B -> 70B       -0.16217
     63B -> 72B       -0.10120
     67B -> 70B        0.87674
     68B -> 70B        0.37169
```

<jump id='addtd'></jump>In experiment, we measure the action spectra from 210nm to 700nm, so we hope the theoritical one can cover that region. If the last transition energy cannot reach 210nm, we should add more states to it. For example, if the original route card is `# TD(Nstates=30) um062x/6-31+g(d,p) pop=none scf=(xqc,tight)` and its chk file is *test.chk* the new input file should be:

```
%mem=32GB
%nprocshared=28
%oldchk=test.chk
%chk=test_add.chk
# TD(add=10) Geom=AllCheck um062x/6-31+g(d,p) pop=none scf=(xqc,tight)
! a blank line must be here
```

### <font size=3>1.[tddft_lorentzian.py](https://raw.githubusercontent.com/yueliu96/scripts_for_lab/master/tddft_lorentzian.py)</font>

- *Usage*
  - `python tddft_lorentzian.py td_log`
- *Descriptions*
  - Reads all excitated frequencies, oscilation strength and S**2 from log file and checks if the last one is below 210nm.
  - If not, writes the new input file as shown above named with *test_add.gjf* if original input is *test.gjf*. The original input file and chk file must be in the same directory.
  - Otherwise, uses S**2=2.6 as a cutoff to choose frequencies and applies lorentzian equation to calculate absorption spectra. The results are written to *test_uvvis.csv* if log named with *test.log*.

### <jump id='vistd'></jump><font size=3>2.[cubegen.py](https://raw.githubusercontent.com/yueliu96/scripts_for_lab/master/cubegen.py)</font>

We can also visualize the molecular orbital if we have tddft chk file. We should first use [`formchk`](http://gaussian.com/formchk/) command to generate fchk file, and then use [`cubegen`](http://gaussian.com/cubegen/) to get the cube file, which can be visualized by Gaussian-View. To use cubegen, we also need to decide the molecular orbital number, for $\alpha$ orbital, like 68A, just set mo=68. But for $\beta$ orbital,like 72B, we should find the total number of $\alpha$ orbitals first. If one molecule has 70 $\alpha$ electrons(NAE) and 356 virtual $\alpha$ orbitals(NVA), set mo=498(70+356+72). 

If we run cubegen on the login node, it will take around 1 minutes. Usually we are interested in several orbitals in one or more excited states. In this way, this script comes out. 

- *Usage*
  - `python cubegen.py td_log num_excited_states`
- *Descriptions*
  - Finds the name of chk file from log file. If chk file not found, stops and does nothing. If its fchk file not found, writes formchk to a sbatch file. 
  - Finds NAE, NVA and unique molecule orbitals in the specified excited state. And writes corresponding cubegen to a txt file.
  - Loads parallel environment and cats tasklists( the txt file) to the sbatch file.
  - Submits it to ckpt partition. It should be finished in several seconds
- *Example*
  
   The transition of the first excited state is listed above. If its log is test.log, NAE+NVA=426. Run `python cubegen.py test.log 1`, we will get 2 files: t1_test.txt and t1_test.sh, and it will submit t1_test.sh to ckpt queue.
  
    *t1_test.txt*:

    ```
    cubegen 0 mo=488 test.fchk test_62B.cube 0 h
    cubegen 0 mo=489 test.fchk test_63B.cube 0 h
    cubegen 0 mo=493 test.fchk test_67B.cube 0 h
    cubegen 0 mo=494 test.fchk test_68B.cube 0 h
    cubegen 0 mo=496 test.fchk test_70B.cube 0 h
    cubegen 0 mo=498 test.fchk test_72B.cube 0 h
    ```

    *t1_test.sh*:

    ```
    #!/bin/bash
    #SBATCH --job-name=fchk_cube
    #SBATCH --nodes=1
    #SBATCH --ntasks-per-node=28
    #SBATCH --time=10:00
    #SBATCH --mem=100G
    #SBATCH --workdir=/gscratch/stf/yueliu96/test
    #SBATCH --partition=ckpt
    #SBATCH --account=stf-ckpt

    echo 'This job will run on' $SLURM_JOB_NODELIST
    #set up time
    start=$(date +%s)

    #load Gaussian environment
    module load contrib/g16.b01

    #use checkpoint file to generte formatted one
    formchk test.chk

    #load parallel environment
    module load parallel-20170722
    cat t1_test_opt.txt | parallel -j 28

    end=$(date +%s)
    echo 'Elapsed Time: '$(($end-$start))'s'
    ```
    After finish, we can get 6 cube files. Transfer them from hyak to your local work directory. We need to use *GaussView* to see how the orbital looks like:
    - open test.fchk with *GaussView*
    - click `Result`$\rightarrow$`Surfaces/Contours`$\rightarrow$`Cube Actions`$\rightarrow$`Load Cube`$\rightarrow$choose one of  your cube files$\rightarrow$highlight that cube$\rightarrow$`Surfacec Actions`$\rightarrow$`New Surface`
