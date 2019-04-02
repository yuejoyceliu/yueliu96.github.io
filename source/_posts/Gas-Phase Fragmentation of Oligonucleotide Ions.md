---
title: Gas-Phase Framentation of Oligo Ions
date: 2019-01-09 12:00:27
tags:
- DNA
- MS
categories:
- MSReading
---
 [Gas-Phase Fragmentation of Oligonucleotide Ions](https://www.sciencedirect.com/science/article/pii/S1387380604003264?via%3Dihub)

- The preferred dissociation channels for a given ion are a function of the ion type, the structure of the molecule, the internal energy distribution of the ion and the time-frame over which the fragmentation reactions can evolve
- McLuckey's nomenclature for backbone cleavages (a/w,b/x,c/y,d/z, 5'-frag:a,b,c,d; 3'-frag: w,x,y,z)

*MALDI and mechanism not included.*

## 1 hetero-dinucleotide FAB CID

### 1.1 $(M+H)^+$

- protonated 3'-(B$_2$+2H)$^+$ > 5'-(B$_1$+2H)$^+$
  - except 3'-T; T: low proton affinity
  - interaction between P and the 3'-B, including a partial positive charge on 3'-B $\rightarrow$ enhance glycosidic bond cleavage
- neutral 5'-(B$_1$+H) > neutral 3'-(B$_2$+H)
  - loss of 3'-base only in dAG and dAC
  - 4 bases similar preference
- $w_1>d_1$
  - $(w_1+H_2)^+$ only not seen in dTG and dTC, where $(d_1+H_2)^+$ is not produced

### 1.2 $(M-H)^-$

- 5'-B$_1^-$>3'-B$_2^-$
- 5'-(B$_1$+H) > 3'-(B$_2$+H) except dGA and dGT
- $w_1^->d_1^-$

### trend
- basicity: $C^->T^-$, $A^->G^-$
- 3'-terminus base is stabilized through H-bond interaction with the P: 
  - strength: G>T>C>A
- acidities: A>T>G>C
- proton affinity: cytidine(C+S), G+S, A+S > C > G > A > T+S > T

## 2 ESI mass spectrometry

### 2.1 Negative mass spec

#### 2.1.1 mononucleotide

- loss of B is facilitated by the presence of 3'-P rather than 5'-P
- 3'-P: lower excitation threshold and greater fragmentation efficiency
- 2-B-5'-P
  - water loss following loss of B
  - neutral base loss dAp, dTp > dCp > dGp, and pdA, pdT >pdC >>pdG
  - H-bond stablize G

#### 2.1.2 deoxyribodinucleotide

- Conplementary ions

$$M^{n-} \rightarrow m_a^{x-} + m_b^{y-}\\
\frac {|(M/n)-(m_a/x)|}{|(M/n)-(m_b/y)|}=\frac {y}{x}$$

- 5'-B > 3'-B
- 5' loss for a given 3'-B: 
  - low charge parent ion: no obvious preference
  - high charge parent ion : A$^-$>G$^-$>T$^-$>C$^-$ or A$^-$>T$^-$>G$^-$,C$^-$
- 3'-B affects 5'-B loss: 3'-B=A>C>T>G
- subsequent decomposition: w and (a-B)
- loss of PO$_3^-$ from 5'-P ions (ex: w ions $\rightarrow$ y) can compete effectively with loss of a base. Lower charge generally favors more greatly the loss of PO$_3^-$ group
- Multiple base loss increases with increasing activation and increasing charge state

#### 2.1.3 trinucleotide

- 5'-B$_1$> B$_2$, B$_3$: A>T>G>C
- loss of 5'-B depends on 3'-B=A>T>G>C
- subsequent: w and (a-B)
- c, x, y, z types also observed

#### 2.1.4 tetranucleotide

- (M-H)$^-$: 3'-B more readily than 5'-B loss
- (M-2H)$^{2-}$
  - same general trend as trinucleotide 
  - y more abundant

#### 2.1.5 single-base nucleotide (3- to 8-mers)

- nucleobase identity
  - poly-T: loss of 5'-T
  - poly-G: loss of 5'-G inhibited
  - the ease of fragmentation: poly-A>>T$\approx$C>G
    - weak N-glycosidic bond strong associated with A
    - stable G due to H-bonding
- odd- and even-electron parent anions:
  - odd: w no M-B $\rightarrow$ backbone cleavage without loss of B
  - even: first loss a base, followed by backbone cleavage

#### 2.1.6 other mass analyzers

- triple quadrupoles (TQIT):
  - low energy process $\rightarrow$ sensitive
  - more extensive structural info
- quadrupole ion traps (QIT):
  - beam-type collisional activation experiment
  - multiple competitive dissociation reactions can happen
- base loss on CID in triple quadrupoles is much less dependent on the identity of the base than in quadrupole ion traps
- base loss not necessary for backbone cleavages for a modified tetraribonucleotide

#### 2.1.7 oligonucleotides with a modified nuclebase: CACGXG

- loss of all non-terminal bases in conjunction with cleavage of their respective 3' C-O bonds
- more electron withdrawing of X, more facile of the loss of B$^-$
- more electron withdrawing of product ions, more likely to further fragmentation

#### 2.1.8 large DNA anions: 50- to 108mers

- predominant dissociation channels depend on DNA molecule itself
- base loss: AH>GH, CH>>TH

#### 2.1.9 BIRD-FT-MS pm 7-mers

- all backbone cleavages are preceded by base loss
- preferred cleavage sites depends on the internal energy of the precursor ions
  - effective T>540K: cleavage at C and G residues
  - effective T<475K: dissociation at A residues dominates

#### 2.1.10 DNA duplex ions

- noncovalent dissociation of the complex into single strands
- covalent fragmentation
  - predominant channel: neutral base loss
  - base loss initiated backbone fragmentation

#### 2.1.11 RNA

- base loss less important
- loss pf a neutral or negatively charged B is the low-energy dissociation process
- 5'-B prefer: C>>T>U
- backbone fragmentation of RNA is decoupled from base loss
- c/y ions in major

### 2.2 Positive ESI

#### 2.2.1 dinucleotide $(M+H)^+$

- 3'-$BH_2^+$ loss > 5', except 3'-T

#### 2.2.2 all trimers and 16 mixed-base tetramers $(M+H)^+$ in QIT

- initial step:  neutral base loss
  - loss depends on PA: C $\approx$ G>A>>T
  - position: 5'>3'>internal
- cleavage of 3'C-O phosphodiester bond $\rightarrow$ w and (a-B)
- dTTT
  - protonaed at phosphate oxygen
  - $z_2^+$ ion (also occur as a 2nd process in a few cases when 5'-B=C/G/A)

#### 2.2.3 up to 10-mer in TQIT

- charged B loss followed by w/(a-B)
  - C>G>A>>T
  - 3'>5'>internal
  - agree with dimers, but trimers
- poly-T: x-2H and z-2H

#### 2.2.4 EBE-TOF MS

- $BH_2^+$ loss agree with PA
- charge of the precursor affects the abundance of ions from the bases more than position of the base
- loss of T as an anion possible for $(M-2H)^{2-}$

#### 2.2.5 ECD and IRMPD of doubly protonated

- ECD
  - polydG: radical w/d "sequence". no even-e a/z ions
  - polydC: even-e w/d ions, a/z ions in most
  - polydA: even-e w/d ions, little fragmentation than C/G
  - polydT: poor ionization, low PA
  - dGCATGC: even-e d-ion and a $z^\cdot$-type
- IRMPD
  - similar to CID: B, w/(a-B)
  - more sequence info than ECD

