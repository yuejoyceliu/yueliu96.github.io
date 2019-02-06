---
title: OligoNucleotide Papers
date: 2019-01-02 15:30:51
tags:
- oligo
categories:
- OligoReading
---

 ***Keyword***
  
 adenine |  cation radical |  cytosine | electron attachment | guanine | nucleotide | proton transfer | spectra | thymine |

# [UV–Vis Action Spectroscopy Reveals a Conformational Collapse in Hydrogen-Rich Dinucleotide Cation Radicals](https://pubs.acs.org/doi/abs/10.1021/acs.jpclett.7b01856)

- Why
  - DNA cation radicals are intermediates during the interaction of DNA with high energy particles
  - electron defect initially located in a nucleobase, migrates along the DNA backbone to reside on guanine
  - DNA behavior at atomic-level needed
- Goal
  - proton and electron transfer along a single strand in DNA and related cation radicals
  - use deoxyriboadenosine dinucleotide (dAA) and riboadenosine chimeras (pseudo-dAA)
- Intro
  - dication$\rightarrow$catrad: conformation collapse
  - dAA
    - intra proton migrations btw nucleobases
  - pseudo-dAA-catrad
    - zwitterionic structures
    - Coulomb stablization

the first time Turecek found combining UVPD with TDDFT can identify and distinguish isomeric peptide cation-radicals by ETD in [here](https://onlinelibrary.wiley.com/doi/full/10.1002/jms.3717)
  
## 1. Gaseous Protonated A

- N-1, N-3, N- 7, N-9, and NH2 (N-10) positions: potential protonation sites
- dA: N-3
  - H bond stablization
- dAA: N-1, N-1''
- psedo-dAA: N-3, N-3''
  - H bond stablization

## 2. Form Cation Radicals

- ETD dAA+2$H^+$: $[M-H]^+(m/z\ 565)$, $[M-H-A]^{+\cdot}(m/z\ 431)$, $w^+(m/z\  332)$
- M+CE/DBCE$\rightarrow$ESI$\rightarrow$ETD: $M^{+\cdot}$
- CE favors N-1 position

## 3. UV-Vis Action Spectrum 

- vis: broad band at 465nm; uv: 340nm, 260nm 
- channel: $w^+(m/z\ 332)$, $[w+H]^{+\cdot}(m/z\ 333)$, $[M-H-A]^{+\cdot}(m/z\ 431)$
- 260nm is same with [pccp_adenine1](#ap1) and [pccp_adenine2](#ap2)

## 4. Dinucleotide Cation Radical Structures

- if exothermic, isomerization driven by proton migrations will occur sponstaneously and driven by exotherimic energy provided by the electron attachment reaction. 
- electron not attach N-1
- hydrogen migration might face substantial energy barrier. [[A+H1](#l1) | [A+H2](#l2)]
- proton transfer (move radical position)$\rightarrow$optimize$\rightarrow$ more stable structures
- theoritical uvvis spectra and molecular orbital analysis $\rightarrow$ possible tautomers & spectra contributions $\pi_z \rightarrow \pi_z^*$

## 5. Adenine Ribonucleotide Chimeras

- uv-vis analysis: similiar band position to dAA 
- aromatic diesters
  - opt: zwitterionic dication-anion radicals $\longleftrightarrow$ folded structure (exothermic conformation collapse)
  - Coulomb stablization of zwitterionic structures is analogous to the solvent effects governing DNA ionization ([DNAion1](#ion1) | [DNAion2](#ion2))
- cyclohexane diester: 
  - adenine cation and radical moieties are located on the opposite sides of the cyclohexane ring 
  - attractive ion−dipole and ion-induced dipole interactions

# [Hydrogen-Rich Cation Radicals of DNA Dinucleotides: Generation and Structure Elucidation by UV–Vis Action Spectroscopy](https://pubs.acs.org/doi/abs/10.1021/acs.jpcb.8b07925)

- Why
  - DNA ionization causes chemical changes leading to complex process of DNA damage; intermediates: DNA cation radicals
  - the intrinsic electronic properties of the reactive cation radical intermediates just are elucidated recently
  - without solvent and counterions, gas-phase studies can focus on the intrinsic electronic and chemical properties of the radical species ([ref](#ref))
- Goal
  - purine and pyrimidine nucleobases in dinucleotide cation radicals exhibit different properties: 
    - nucleobase stacking
    - hydrogen bonds
    - propensity for undergoing intramolecular proton transfer
- Intro
  - cation radical
    - $(dGG+2H)^{+\cdot}$: conform collapse, 3'-G C-8-H radical
    - $(dCG+2H)^{+\cdot}$: collapse, a mixture of 5'-C and 3'-G radicals
    - $(dGC+2H)^{+\cdot}$: retain structure, a 3'-C radical
  -  basicity ($pK_a$) in water $\Leftrightarrow$ ability of proton-transfer reactions in solution
     -  $(G+H)^\cdot$: 20.0
     -  $(C+H)^\cdot$: 4.6
  
## 1. Dinucleotide Cation Radical Generation

- larger oligos form stable cation radicals
- smaller one needs DBCE

## 2. Dinucleotide Cation Radical Collision-Induced Dis- sociation and Photodissociation Spectra

- CID of cation radicals
  - $(dGG+2H)^{+\cdot}$: $[M-G]^{+\cdot}$, $[M-G-H]^{+}$, $[d_1/w_1]^+$, $[d_1/w_1+H]^{+\cdot}$
  - $(dGC+2H)^{+\cdot}$: $[M-H_2O]^{+\cdot}$, $[M-C]^{+\cdot}$, $[M-G-H]^{+}$, $d^+$, $[w+2H]^+$, $[z_1+H]^{+\cdot}$
  - $(dCG+2H)^{+\cdot}$: $[M-H_2O]^{+\cdot}$, $[M-C-H]^{+}$, $[M-C]^{+\cdot}$, $w_1^+$
- how nucleobase nature and position affect
  - C at 3'-end $\rightarrow$ elimination of water
  - C at 5'-end $\rightarrow$ lost as $[C+H]^\cdot$
  - loss of C > loss of G
  - 5'-C suppresses 3'-G loss
- UVPD similiar to CID
- close shell systems have similiar absorption $\rightarrow$ not only associated with radical moieties
  
## 3. $[dGG+2H]^{+\cdot}$ Action Spectroscopy and Ion Structures

- action spectra: 450-470nm, 330, 310 and 270nm
- structure:
  - H positon
    - most basic: N-7
    - 2nd basic: 6-OH−N-3−H
  - CE at 5'-terminal stable than that at 3'
  - H transfer
    - $dG^+dG^\cdot$
    - exthothermic 
    - cation and radical at 5'-G most stable
    - cation at 3'-G, radical at 5'-G relatively stable and match spectra
- 450-460nm: SOMO, 156$\alpha (\pi)\rightarrow$ combined $\pi^*$ at 3'-G radical
- $(G+H)^\cdot$ estimates thermal shift and broadening
- 215kJ/mol ($\lambda$<550nm) enough to drive dissociation

## 4. $[dCG+2H]^{+\cdot}$ Action Spectroscopy and Ion Structures

- action spectra: weak 450-480nm, strong 350 and 280nm
- structure:
  - cytosine: O-2 and N-3 basic positions
  - CE at 5'-C ring and 3'-G ring
  - H posiitons: dC3G7
  - H transfer
    - $dC^\cdot G^+ \leftrightarrow dCG^{+\cdot}$
    - transition state high, but exthothermic finally (kinetic hampered)
    - major: radical at C; minor at G
    - RRKM calculation: 310kJ/mol internal energy needed for conversion
    - $E_{int}=E_{thermal}+E_{exc}$, where $E_{exc}$ is part (calculated by heat capacity) of exthothermic reaction energy 
- dissociation of C or (C+H)$^\cdot$ are less endothermic than G or (G+H)$^\cdot$

## 5. $[dGC+2H]^{+\cdot}$ Action Spectroscopy and Ion Structures

- action spectra: extremely weak broad 620nm, 420-500nm and 360nm, strong 285nm
- structure
  - CE at 3'-C ring
  - radical at C: $dG^+C^\cdot$
  - proton transfer exthothermic but not fit spectra 
  
## 6. Discussion

- site of electron attachment to the dications depends on
  - nucleobase nature
     C>G: $RE_{adiab}(C)$=5.17eV; $RE_{adiab}(G)$=4.46eV
  - nucleobase position
    dGG: 5'-G>3'-G
- ring stacking and proton transfer
  - dGG: nucleobase stacking, faciles proton transfer
  - dGC and dCG: nucleobases perpenticular, kinetically hampered
- $(G+H)^{+} (aq,pK_a=3.3)+(G+H)^\cdot (aq) \overset{\Delta G=-95 kJ/mol}{\longrightarrow} G(aq)+(G+2H)^{+\cdot}(aq,pK_a\approx20.0)$
- $(C+H)^{+} (aq,pK_a=4.6)+(C+H)^\cdot(aq) \overset{\Delta G=-0.1 kJ/mol}{\rightleftharpoons} C(aq)+(C+2H)^{+\cdot}(aq,pK_a\approx4.6)$

# [Watson-Crick Base Pair Radical Cation as a Model for Oxidative Damage in DNA](https://pubs.acs.org/doi/10.1021/acs.jpclett.7b01251)

## Background
- mechanisms of DNA damage poorly understood
  - oxidation $\rightarrow$ deprotonation at G $\rightarrow$ H abstraction from sugar $\rightarrow$ DNA strand breaks $\rightarrow$ mutagenesis and cancer
  - probing initially formed radical cation challengeing
- proton-coupled electron and hole transfer is an important
feature in radiation damage process

## Notes
- gas-phase acidity data may be more appropriate to characterize the equilibrium position of the proton in oxidized GC base pairs ([ref](#gasbetter))
- Guanine
  1. the lowest ionization energy among GATC, both in solution and gas $\Rightarrow$
  2. electron loss during ionization of DNA mostly occurs from G $\rightarrow$
  3. G radical cations enhances acidities than G $\Rightarrow$ 
  - dG$^{+\cdot}$-dC pair: H transfer from G to C (G3$\rightarrow$C3) $\Rightarrow$ relocation of radical site to sugar
- homolytic bond dissociation enthaloy of 401kJ/mol for [dG+H(N$_7$)]$^+$ is comparable to that for a typical C-H bond $\Rightarrow$ other radicals via intra- or intermolecular H-abstraction reactions
- CID
  1. $[dGdC]^{+\cdot}-CH_2O$: occurs on the sugar of G
  2. further loss $C_2H_3O_2$
  3. $[dGdC]^{+\cdot}-C_5H_8O_3$ not nucleobase specific

# <jump id="ap1">[The Electronic Spectrum of Protonated Adenine: Theory and Experiment](https://pubs.rsc.org/en/content/articlelanding/2005/cp/b507422c/unauth#!divAbstract)</jump>

## Background

- high photostability of DNA is essential for life on earth
- advantage of gas phase experiment
  - spectra of protonated species in solution is principally complicated, because:
    - solvation shifts and inhomogeneous broadening
    - charged and neutral species coexist $\rightarrow$ superposition of spectra
    - in plolar protic solvents proton exchange fast, causing lifetime broadening
  - mass selection before spectra
- 1951 crystallographic evidence: 9H-A prefers protonated at N-1
- in tA-T Watson-Crick base pair, the N1 atome of A acts as a H-bond acceptor

## Note

- 实验方法： 中性和酸性腺嘌呤的实验谱图与计算的跃迁对比，观察红移或蓝移的情况归属峰的性质,计算激发态构型判断峰的形状
- UV-Vis: 205nm, 260nm both neutral and protonated A
- $S_0-S_1$ photofragment spectrum pf A+H: the lowest $\pi\pi^*$ transtion
  - loss of $NH_3$ ager absorption of one UV photon
- tautomer:
  - 9H-A-N1H most stable > 7H-A-N3H >> 9H-A-N3H
  - neutral ddenine 7H-A large dipole moment than 9H-A
- vertical absorption spectra
  - neutral 9H-A
    - 4.91eV/252nm: 1st $\pi\pi^*$ excitaion, medium $HOMO\rightarrow LUMO+1$ and $HOMO-1\rightarrow LUMO$, not HOMO to LUMO
    - 5.02eV/247nm: weak 1st $n\pi^*$
    - 5.09eV/244nm: 2nd $\pi\pi^*\ (HOMO\rightarrow LUMO)$
    - 5.35eV/232nm: $HOMO\rightarrow Rydberg\ orbital$
  - protonated 1H-9H-A
    - 4.83eV/257nm: 1st $\pi\pi^*\ (HOMO\rightarrow LUMO)$
    - 5.15eV/241nm: 2nd $\pi\pi^*\ (HOMO\rightarrow LUMO+1)$
    - 5.23eV/234nm: weak 1st $n\pi^*$

# <jump id='ap2'>[Gas-phase spectroscopy of protonated adenine, adenosine 5′-monophosphate and monohydrated ions](https://pubs.rsc.org/en/content/articlelanding/2013/cp/c3cp53742k/unauth#!divAbstract)</jump>

- the action spectra of $AMPH^+$, $AH+$, $AH^+(H_2O)$ similiar indicates
  - the same protonation site, mostly N-1
  - the lowest-energy trnsitions are independent of surrondings
- Action Spectra: broad band between 230 and 290nm and 210nm
  - 250,270nm: $\pi\pi^*$
  - 230nm: $n\pi^*$

# <jump id='l1'>[Distonic Isomers and Tautomers of Adenine Cation Radical in the Gas Phase and Aqueous Solution](https://pubs.acs.org/doi/10.1021/jp046575q)</jump>

## Background

- Distonic/ylid ions
  - nonclassical open-shell species in which the charge and radical sites reside on separate atoms
  - often more stable than isomeric canonical cation-radical structures
- DNA damage mechanism: direct ionization produce cation radicals and electron capture leading to anion radicals

  
## Note

- protonation of gas phase under CI depends on PA

![PA_A](https://raw.githubusercontent.com/yueliu96/blog_images/master/Screen%20Shot%202019-01-12%20at%2016.22.32.png)

- $pK_a$ of N-9, N-10, C-2 and C-8: 3.2, 3.3, 6.2 and 11.9
- CAD of $AH^+$: M-H; M-NH3 (H transfer from $N_1,\ N_3\ or\ N_7$ on amino group); ring cleavage M-HCN, consecutive -$CH2N2$
- DFT calcualtion
  - amino group shows less pyramidization
  - removing an electron from orbitals that has nodal surfaces decreases the $\pi$-antibonding interaction resulting in shortening bonds
  - polar solvents are known to affect the realtive stabilites of nucleobase tautomers greatly
- Calcualtion result
  - elimination of $NH_3$ is the lowest-energy channel that requires $\Delta H_{rxn,0}=371kJ\ mole^{-1}$
  - loss of a H is also endothermic
  - a small activation energy for the addition of H to C-2 position
  - H attached to N-10 is exothermic, $\Delta G=383kJ mol^{-1}$, which is sufficient to drive exothermic hydrogen transfer from ... to it
    - methyl group in T
    - SH group in C
    - OH in Tyr
    - $C_{\alpha}$ methines of the peptide backbone

# <jump id='l2'>[Adenine Radicals in the Gas Phase. An Experimental and Computational Study of Hydrogen Atom Adducts to Adenine](https://pubs.acs.org/doi/abs/10.1021/jp0529725)</jump>

![dna damage scheme](https://raw.githubusercontent.com/yueliu96/blog_images/master/Screen%20Shot%202019-01-13%20at%2012.36.45.png)
-  the elusive hydrogen atom adduct to the N-1 position in A, which is thought to be the initial intermediate of chemical damage
   -  N-1 is 48-130 times more basic than N-3
-  C-8 adduct is the most stable tautuomer, which is predicted to be the prdominating product at thermal equilibrium in solution at 298K
-  proton transfer from $H_3O^+ or\ NH_4^+$ to Ade is exthothermic

# [Dependence of Spurious Charge- Transfer Excited States on Orbital Exchange in TDDFT: Large Molecules and Clusters](https://pubs.acs.org/doi/10.1021/ct600282k)

- intensity of CT ransitions is likely to be exaggerated by TDDFT calcualtions
- Density functional theory formally permits the expression of the total ground-state energy and other properties of a quantum many-body systme as functionals of the electron density alone and provides a formally exact scheme for solving the many-body problem
- TDDFT is an extension of DFT in which many-body excitations are associated with the poles of the exact density response
- 6-31G basis sets: an efficient blend of accuracy and manageablw size for large confugated molecules
  - 6-31G*: with polarization functions
  - 6-31+G: with diffuse functions
- Charge transfer states
  - photexcited electron and hole are significant spatial separation
  - usually higher in energy than the relevant Frenkel-exciton band of optical (nonvanishing oscillator-strength) and dark (vanishing oscillater-strength) states
  - however, DFT methods drastically underesetimate their energies $\rightarrow$ all 3 types of states in dimers might be mixed

# [Experimental Evidence for Noncanonical Thymine Cation Radicals in the Gas Phase](https://pubs.acs.org/doi/abs/10.1021/acs.jpcb.7b09872)

# [Cytosine Radical Cations: A Gas-Phase Study Combining IRMPD Spectroscopy, UVPD Spectroscopy, Ion–Molecule Reactions, and Theoretical Calculations](https://onlinelibrary.wiley.com/doi/full/10.1002/cphc.201700281)

# [Radical Cations of the Nucleic Bases and Radiation Damage to DNA: Ab Initio Study](https://www.sciencedirect.com/science/article/pii/S0065327606520064)

# [Hydrogen Bonding and Proton Transfer in Ionized DNA Base Pairs,Amino Acids and Peptides](https://onlinelibrary.wiley.com/doi/abs/10.1002/9783527629213.ch7#)

# <jump id='ion1'>[Electron Detachment Energies and Isomerism in Purinic Deoxyribonucleotides](https://onlinelibrary.wiley.com/doi/abs/10.1002/qua.21330)</jump>

# <jump id='ion2'>[Ab Initio Electron Propagator Methods: Applications to Nucleic Acids Fragments and Metallophthalocyanines.](https://onlinelibrary.wiley.com/doi/abs/10.1002/qua.22836)</jump>

# [Ion/Ion Reactions: New Chemistry for Analytical MS](https://pubs.acs.org/doi/abs/10.1021/ac9014935)

# [One-Electron Oxidation of DNA Oligomers That Lack Guanine:  Reaction and Strand Cleavage at Remote Thymines by Long-Distance Radical Cation Hopping](https://pubs.acs.org/doi/abs/10.1021/ja058758b)

![AT rxn at T](https://raw.githubusercontent.com/yueliu96/blog_images/master/AT%20rxn%20at%20T.jpeg)

A defining characteristic of the one-electron oxidation of duplex DNA is reaction at $G_n$ (n=1-3) sites tat is detected as strand cleavage following chemical or enzymatic treatment. Reaction occurs primarily at guanines because they have low oxidation potentials, which causes the migrating radical cation to pause there briefly. Oxidation of DNA by photoionization with 193 nm light results primarily in reaction at G, but in "guanine-poor regions". reaction at A is alse observed. Pyrimidines T and C are considerably more difficult to oxidize than purines.

Here, one-electron oxidation of DNA oligomers that do not contain guanine: reaction occurs primarily at thymine even though adenine has a significantly lower $E_{ox}$

# <jump id="ref">[Transient Intermediates of Chemical Reactions by Neutralization—Reionization Mass Spectrometry](https://link.springer.com/chapter/10.1007/3-540-36113-8_3)</jump>

# [What Hinders Electron Transfer Dissociation (ETD) of DNA Cations?](https://link.springer.com/article/10.1007%2Fs13361-017-1791-z)

# [Proton and hydrogen atom adducts to cytosine. An experimental and computational study](https://www.sciencedirect.com/science/article/pii/S1387380607000279)

# [Toward True DNA Base-Stacking Energies: MP2, CCSD(T), and Complete Basis Set Calculations](https://pubs.acs.org/doi/10.1021/ja026759n)

# [Purine bases, nucleosides, and nucleotides: aqueous solution redox chemistry and transformation reactions of their radical cations and e- and OH adducts](https://pubs.acs.org/doi/10.1021/cr00093a003)

# [Proton-coupled Electron Transfer in DNA on Formation of Radiation-produced Ion Radicals](http://pubs.acs.org/doi/abs/10.1021/cr100023g)

# [Induction of Strand Breaks in Single-stranded Polyribonucleotides and DNA by Photoionization: One Electron Oxidized Nucleobase Radicals as Precursors](https://pubs.acs.org/doi/abs/10.1021/ja961722m)

# [How Easily Oxidizable is DNA? One-electron Reduction Potentials of Adenosine and Guanosine Radicals in Aqueous Solution](https://pubs.acs.org/doi/10.1021/ja962255b)

# <jump id='gasbetter'>[Structure and Acid-base Properties of One-electron-oxidized Deoxyguanosine, Guanosine, and 1-Methylguanosine](https://pubs.acs.org/doi/10.1021/ja00185a046)</jump>

