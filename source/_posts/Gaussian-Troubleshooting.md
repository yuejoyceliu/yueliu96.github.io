---
title: Gaussian Troubleshooting
date: 2019-01-22 20:05:42
tags:
- software
categories:
- Turecek Lab Tutorial
---

Troubleshooting about: [FormBX had a problem](#formbx) | [Negative Frequency](#nfreq) | [Freq job never stops calculating vectors](#vecfreq) | [Transformation cannot fit in the specified MaxDisk](#maxdisk) | To be continue ...


# <jump id='formbx'>FormBX had a problem</jump>

If get error message like:

```txt
 GradGradGradGradGradGradGradGradGradGradGradGradGradGradGradGradGradGrad
 Berny optimization.
 Using GEDIIS/GDIIS optimizer.
 Bend failed for angle    33 -    87 -    81
 Tors failed for dihedral    32 -    33 -    87 -    81
 Tors failed for dihedral    34 -    33 -    87 -    81
 Tors failed for dihedral    86 -    33 -    87 -    81
 Tors failed for dihedral    15 -    81 -    87 -    33
 FormBX had a problem.
 Error termination via Lnk1e in /sw/contrib/gaussian/g16/B01/g16/l103.exe at Tue Jan 22 12:58:22 2019.
```

That means the angle formed by atom 33, 87 and 81 is 180$^\circ$. So, modify it manually and start over optimization again.

# <jump id='nfreq'> Negative Frequency </jump>

Gaussian optimization algorithm uses the gradient descent to find the closest minmum ($f'(x)=0$). However, the gradient of a local maximum point is also 0, which corresponds to a transition state. A transition state should have one negative/imaginary frequency.

Frequencies can be visualized after loading the output file into GaussView. What we should do is locate the imaginary frequency, move the atom/atom group in the direction of this vibration, reoptimize this modified structure and calculate the frequency again.

# <jump id='vecfreq'> Freq Job Never Stops Calculating Vectors</jump>

Gaussian uses two different algorithms to do a frequency calculation (solving the CPHF equations) The  standard one uses a lot of RAM memory but is very fast. However, when RAM memory is not enough or the number of CPHF  equations exceeds 5000 by default, gaussian uses another algorithm, this tries to save RAM memory  by storing intermediate results on a hard disk. This takes very long making the calculations practically  inactive.

If limited by RAM memory, increase it by linkwords `%mem=xxx`. If  CPHF equations exceed 5000 and there is enough memory available, add an extra keyword: `CPHF(MaxInv=10000)` on the route card. This puts the maximum number of  CPHF equations for the basic algorithm to 10,000.

# <jump id='maxdisk'>Transformation cannot fit in the specified MaxDisk</jump>

We will get this error when specifying `maxdisk=xxx` and the disk is not enough to finish the current job.

The MaxDisk keyword specifies the amount of disk storage available for scratch data. But some jobs, like CCSD, CCSD(T), QCISD(T), and BD(T) energies have fixed disk which cannot be limited by MaxDisk. In this case, if the disk storage is not enough, we will get error information like:

```txt
 Semi-Direct transformation.
 ModeAB=           4 MOrb=            51 LenV=   26834989397
 LASXX=   3675829080 LTotXX=  3675829080 LenRXX=  7405142880
 LTotAB=  3729313800 MaxLAS=  4334140395 LenRXY=           0
 NonZer= 11080971960 LenScr= 22248854016 LnRSAI=  4334140395
 LnScr1=  8702274560 LExtra=   897554704 Total=  43587966555
 MaxDsk= 13421772800 SrtSym=           T ITran=            4
 Transformation cannot fit in the specified MaxDisk.
 Error termination via Lnk1e in /sw/contrib/gaussian/g16/B01/g16/l804.exe at Wed Dec 19 01:05:37 2018.
 Job cpu time:       0 days  7 hours 19 minutes 44.3 seconds.
 Elapsed time:       0 days  0 hours 15 minutes 43.2 seconds.
 File lengths (MBytes):  RWF=  63349 Int=      0 D2E=      0 Chk=     16 Scr=      1
```

Where, `MaxDsk=13421772800` means I uses `maxdisk=100G` ($\frac{13421772800\times8}{1024^3}$); `Total=43587966555` means the minimum disk should be 325G ($\frac{43587966555\times8}{1024^3}$).

For Hyak, there is around 100G storage space for one node. So we can locate the largest scratch file (read and write file) to `/gscratch/scrubbed/username/` like:

```bash
%rwf=/gscratch/scrubbed/yueliu96/test.rwf
%nosave
```