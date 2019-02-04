---
title: Out of Field Proposal
date: 2019-01-16 15:47:38
tags:
categories:
- NoteBook
---

# Goal

- how concentration, temperature, bilayer, time and pH affects gp41
  - secondary structures ($\alpha$-helix, $\beta$-strand and turn/loop?)
  - tilt angles (if all $\alpha$-helix, or one is $3_{10}$ helix)

## [Oligomeric Structure and Three-Dimensional Fold of the HIV gp41 Membrane-Proximal External Region and Transmembrane Domain in Phospholipid Bilayers](https://pubs.acs.org/doi/10.1021/jacs.8b04010)

### HIV-1 glycoprotein, gp41

- mediate fusion of the virus lipid envelope with the target cell membrane during virus entry into cells
- MPER and TMD
  - membrane-proximal external region (MPER)
    - harbors the epitopes for four broadly neutralizing antibodies
    - binds to the membrane surface
  - transmembrane domain (TMD)
    - anchors the protein to the virus lipid envelope
    - spans the bilayer
  - both are important for HIV entry into cells
    - Trp-to-Ala mutations in MPER and deletion of the MPER $\rightarrow$ abrogate virus entry and membrane fusion
    - replace gp41 TMD with other TMD $\rightarrow$ impact fusion activity
    - truncate C-terminus of TMD in simian HIV $\rightarrow$ reduce fusogenicity

  structure unchanged within 235K to 303K

### MPER-TMD Structure

- Turn Structure
  - helix-turn-helix
  - MPER as bound to the membrane surface while TMD spans the bilayer
  - monomeric
- Continuous Helix
  - continuous helix, perpendicular to the membrane plane
  - tilted orientation for long helix to reduce the hydrophobic mismatch between the peptide adn the bilayer portion of the bicelle
- trimeric-MPER + monomeric-TMD
- Helix-turn-helix trimer
  - most $\alpha$-helix: membrane-independent
  - TMD 50% $\beta$-strand: a combination of the amino acid sequence and the spontaneous negative curvature of PE membranes
  - but not uniquely constrian the turn structure bewteen W678 and K683 at the atomic level

These divergent structural conclusions may arise from the truncated nature of th epeptide sequences in most studies, but could also reflect an inherent conformational plasticity of this region of gp41, which may be importanct for the protein to fold into different structures at different stages of virus-cell fusion

heterogeneity in the protein oligomeric states, differenced in th ebicelle stability and size and the differenct P/L ratios used

### Notes

- $\beta$-strand conformation is correlated with membrane dehydration
- a monomeric membrane-spanning $\alpha$-helix is expected to undergo rapid uniaxial diffusion in the membrane, while a highly oligomerized peptide or a peptide that contains an extended segment on the membrane surface is expected to be immobilized
- MPER-TMD trimer is insensitive to the peptide concentration

### Question
- inconsistent and contradictory structural information abounds in the literature about the C-terminal membrane-interaction region of gp41
- difficulty of crystallizing and solubilizaing the MPER-TMD, most structural studies of this functionally important domain were carried out using either only MPER or only TMD
- FP and TMD disorder the cell and virus membranes by mechanisms that still poorly understood

# SFG Theory

## [Biological Macromolecules at Interfaces Probed by Chiral Vibrational Sum Frequency Generation Spectroscopy](https://pubs.acs.org/doi/10.1021/cr4006044)

Second-order nonlinear optical technique, which uses two pulsed lase sources, one at infrared (IR) frequency ($\omega_{IR}$) and the other at visible frequency ($\omega_{VIS}$). When this two beams are made to spatially and temporally overlap at surfaces, a second order nonlinear optical process producing polarization at the sum frequency ($\omega_{IR}+\omega_{VIS}$) can be induced to generate SFG signal.

The electric field of SFG signals $E_{SFG}^I \propto \sum_{JK}\chi_{IJK}^{(2)} E_{VIS}^J E_{IR}^K$. $\chi_{IJK}^{(2)}$ is an element of the second-order susceptibility tensor, which contains structural and chemical information about the target medium. It is nonzero only when the medium lacks centrosymmetry and the second-order susceptibility of an interface consists of a nonresonant term, $\chi_{NR}^{(2)}$, and a sum of vibrationally resonant terms, $\chi_q^{(2)}$
$$\chi^{(2)}=\chi_{NR}^{(2)}+\sum_q \chi_q^{(2)}=\chi_{NR}^{(2)}+\sum_q \frac{A_q}{\omega_{IR}-\omega_q+i\Gamma_q}$$
where $A_q$ is the amplitude, $\Gamma_q$ is the damping coefficient, $\omega_q$ is the resonat frequency of the qth vibrational mode, and $w_{IR}$ is the frequency of the incident IR beam. The SFG signal is enhanced when $\omega_{IR}$ is in resonance with $\omega_q$. Thus, SFG is a surface-specific vibrational spectroscopy

## [Molecular Chemical Structure on Poly(methyl methacrylate) (PMMA) Surface Studied by Sum Frequency Generation (SFG) Vibrational Spectroscopy](https://pubs.acs.org/doi/full/10.1021/jp013161d) 

In an SFG setup, a pulsed visible laser beam (532nm) and a tunable pulsed IR beam are overlapped spatially and temporally on a surface. The light emitted by the nonlinear process at the sum frequency, $\omega=\omega_1+\omega_2$, is detected by a photodector. The intensity of output is proportional to the square of the samples's second-order nonlinear susceptibility, which vanishes when a material has inversion symmetry under the electric-dipole approximation. Bothe theoretical calculations and experimental results show that SFG is submonolayer sensitive. Aplot of SFG intensities vs the frequency of the IR laser produces the vibrational spectrum of the surface species. As SFG is a polarized light experiment, the orientation of surface molecules can also be deduced by using different polarization combinations of input and output beams.

![sfg setup](https://raw.githubusercontent.com/yueliu96/blog_images/master/sfg_setup.jpg)
$$I(\omega)=\frac{8\pi^3\omega^2sec^2\beta}{c^3n_1(\omega)n_1(\omega_1)n_1(\omega_2)}|\chi_{eff}^{(2)}|^2I_1(\omega_1)I_2(\omega_2)$$
where $n_i(\omega)$ is the refractive index of medium i at frequency $\omega$, $\beta$ is thereflection angle of the sum frequency field, $I_1(\omega_1)$ and $I_2(\omega_2)$ are the intensities of the two input files. $\chi_{eff}^{(2)}$ is the effective second-order nonlinear susceptibility tensor of the surface, which is related to the second-order nonlinear susceptibility $\chi^{(2)}$ in the lab coordinate system.

Different component of $\chi^{(2)}$ are related to the respective componets of the molecular hyperpolarizability (in the molecular coordinated system, which is a product of IR and Raman transition moments) by the average orientational angle of the functional group. Therefore, we can deduce the orientation information of each functional group after determining the corresponding components of $\chi^{(2)}$ by fitting SFG spectra and knowing the molecular hyperpolarizability.

$$\chi_{eff,ssp}^{(2)}=L_{yy}(\omega_{SFG})L_{yy}(\omega_{Vis})L_{zz}(\omega_{IR})sin\beta_{IR} \chi_{yyz}^{(2)}$$

$$\chi_{eff,ppp}^{(2)} = - L_{xx} (\omega_{SFG}) L_{xx} (\omega_{Vis}) L_{zz} (\omega_{IR}) cos\beta_{SFG} cos\beta_{Vis} sin\beta_{IR}\chi^{(2)}_{xxz}\\
-L_{xx}(\omega_{SFG}) L_{zz}(\omega_{Vis}) L_{xx} (\omega_{IR})cos\beta_{SFG} sin\beta_{Vis} cos\beta_{IR} \chi^{(2)}_{xzx}\\
+L_{zz}(\omega_{SFG}) L_{xx}(\omega_{Vis}) L_{xx}(\omega_{IR})sin\beta_{SFG}cos\beta_{Vis} cos\beta_{IR} \chi^{(2)}_{zxx}\\
+L_{zz} (\omega_{SFG}) L_{zz} (\omega_{Vis}) L_{zz} (\omega_{IR}) sin\beta_{SFG} sin\beta_{Vis} sin\beta_{IR} \chi^{(2)}_{zzz}$$

Here $\chi_{xyz}$ is one componaent of $\chi^{(2)}$ with the lab coordinates chosedn such that z is along the interface normal and x is in the incident plane. $\chi_{eff,ssp}^{(2)}$ is a component of the effective second-order nonlinear susceptibility measured in the experiment, means the element obtained by s-polarized SF beam, s-polarized visible beam and p-polarized IR beam. $\beta_{x}$ is the angle between the surface normal and the x beam. $L_{ii} (i=x,y\ or\ z)$ are the Fresnel coefficients. Using the near total reflection geometry, the first three items in the equation of $\chi_{eff,ppp}^{(2)}$ are approxiamated to be 0. 

With IR-visible SFG, if the IR frequency is near vibrational resonance, $\chi_{eff}^{(2)}$ can be written as 

$$\chi_{eff}^{(2)}=\chi_{nr}+\sum_q \frac{A_q}{\omega_{IR}-\omega_q+i\Gamma_q}$$

$\chi_{nr}$ arises from the nonresonant background contribution

$$
I_{SFG}=|A_0+\sum_j^\text{num of peaks}\frac{A_j}{\omega-\omega_j+i\Gamma_j}|^2\\
\chi^{(2)}_{eff}(j)=\frac{A_j}{\Gamma_j}$$
where $A_j$, $\omega_j$ and $\Gamma_j$ are the strength, resonant frequency and damping coefficient of the vibrational mode j, respectively. And they can be obtained by fitting the spectrum

## [In Situ Molecular Level Studies on Membrane Related Peptides and Proteins in Real Time Using Sum Frequency Generation Vibrational Spectroscopy](https://www.sciencedirect.com/science/article/pii/S1047847709000744?via%3Dihub)

### name of lipid

| Abbr. | Full Name |
| ------ | ------| 
| POPC | 1-Palmitoyl-2-Oleoyl-sn-Glycero-3-Phosphocholine |
| POPG | 1-Palmitoyl-2-Oleoyl-sn-Glycero-3-[Phospho-rac-(1-glycerol)] (Sodium Salt) |
| DMPC | 1,2-Dimyristoyl-sn-Glycero-3-Phosphocholine |
| d-DMPC | 1,2-Dimyristoyl-D54-sn-Glycero-3-Phosphocholine-1,1,2,2-D4-N,N,N-trimethyl-D9 |
| DMPC-d54 | 1,2-Dimyristoyl-D54-sn-Glycero-3-Phosphocholine |
| DPPC | 1,2-Dipalmitoyl-sn-Glycero-3-Phosphocholine |
| d-DPPC | 1,2-Dipalmitoyl-D62-sn-Glycero-3-Phosphocholine-1,1,2,2-D4-N,N,N-trimethyl-D9 |
| DPPG | 1,2-Dipalmitoyl-sn-Glycero-3-[Phospho-rac-(1-glycerol)] (Sodium Salt) |
| d-DPPG | 1,2-Dipalmitoyl-D62-sn-Glycero-3-[Phospho-rac-(1-glycerol)] (Sodium Salt) |
| DSPC | 1,2-Distearoyl-sn-Glycero-3-Phosphocholine |
|d-DSPC or DSPC-d83 |	1,2-Distearoyl-D70-sn-Glycero-3-Phosphocholine-1,1,2,2-D4-N,N,N-trimethyl-D9 |
| DSPC-d70 |	1,2-Distearoyl-D70-sn-Glycero-3-Phosphocholine |
| DSPG | 1,2-Distearoyl-sn-Glycero-3-[Phospho-rac-(1-glycerol)] (Sodium Salt) |

### SFG setup

a near total reflection experimental geometry that enables us to obtain very strong SFG amide I signals of interfacial proteins, which makes the data analysis eaiser and more accurate. A tunable IR laser beam and a green laser beam of fixed wavelength 532nm are overlapped at the surface of a $CaF_2$ prism onto which a bilayer is deposited. The generated SFG signal is collected by monochromator and aphotomeltilpier tube. By scanning the IR over a certain frequency range, the allowed vibrational modes at the interface can be obtained.

![sfg set](https://raw.githubusercontent.com/yueliu96/blog_images/master/sfg_setup_ye.jpg)

### detection of SFG amide I signal

#### advantage

- the water bending mode does not contribute noticeable SFG signals
  - detected directly without a background substraction
- proteins in the bulk solution do not generate SFG signals
  - selectively probe interfacial proteins/peptides
- probe more measurements than ATR-FRIR in studying the orientation of interfacial proteins/peptides

#### how

SFG amide I signals of proteins can be affected by the surface coverage, orientation and secondary structures of the adsorbed proteins. The amide I mode contains predominately the peptide C=O stretching bands. These C=O groups are held together by hydrogen bonds within the secondary structures and the frequency of the C=O stretch depens heavily on its hydrogen-bonded environment.

- secondary structure
  - $\alpha$-helix: 1650
  - $\beta$-sheet: B1/B3 antiparallel 1685; B2 mode antiparallel : 1635
  - $3_{10}$ helix: 1635 and 1670
- tilt angle of $\alpha$-helix
  - assume all have the same orientation ($\delta$ distribution): easy
  - [two distributions](#2tilt), also introduced the maximum entropy function to deduce the orientation distribution of melittin in a single lipid bilayer based on the ATR-FTIR and SFG measurements
     ![tilt22](https://raw.githubusercontent.com/yueliu96/blog_images/master/2tilt_w.jpg)
  - [membrane proteins the transduce extracellular signals](#tiltout)
     ![tilt out](https://raw.githubusercontent.com/yueliu96/blog_images/master/tilt%20out%20membrane.jpg)

# SFG Method

## Tell $\beta$-strand and $\beta$-sheet

### [Misfolding of Human Islet Amyloid Polypeptide at Lipid Membrane Populates through β-Sheet Conformers without Involving α-Helical Intermediates](https://pubs.acs.org/doi/10.1021/jacs.8b08537)

![beta oligomer](https://raw.githubusercontent.com/yueliu96/blog_images/master/betaoligomers.jpeg)

1. advantage of this article
- quickly capture the transient intermediates in situ and in real time
- identify the formation of $\beta$-hairpin-like monomers, $\beta$-sheet oligomers and fibrils
- reveal the mechanism of amyloid aggregation at the lipid membrane
- method
  - X-ray crystallography: high-rsolution, but not enough time resolution to probe the real-time aggregation

2. method

   the combination of interface-sensitive chiral amide I, achiral amide II and amide III spectral signals of the protein backbone generated in sum frequency generation vibrational spectroscopy (SFG-VS) can provide a unique and powerful tool to capture the hIAPP intermediates at the interface d uring the agggregation process with sufficient structural temporal resolutions

   develop a highly-sensitive femtosecond SFG-VS system, can acquire the ssp and psp sepctra simultaneously with a recording time of < 5 seconds

   Amide II vibrations arise from the out-of-phase combination of the C-N stretch and the N-H in-plane deformation

- $\alpha$-helix: achiral: 1660, 1280
- $\beta$-sheet:
  - chiral amide I mode:
    - $\beta$-hairpin-like monomer (2 antiparallel hydrogen bonded $\beta$-strands connected by a $beta$-turn or short loop): 1630-1643
    - B mode parallel $\beta$-sheet oligomers and fibruls: 1624 (<1630)
    - A mode parrallel $\beta$-sheet: 1670
  - chiral N-H stretch mode: 3285 $cm^{-1}$
  - achiral amide I
    - 1625: B2 mode of antiparallel
    - 1680: (B1/B3 mode of antiparallel $\beta$-sheet) 
  - achiral amide II at 1540: $\beta$-sheet oligomers and fibrils
- loop: achiral: 1660, 1230
- coil: achiral: 1660
- turn: achiral: 1660
  
## Orientation angles

### [Observing a Model Ion Channel Gating Action in Model Cell Membranes in Real Time in Situ: Membrane Potential Change Induced Alamethicin Orientation Change](https://pubs.acs.org/doi/10.1021/ja2110784)

![sfg](https://pubs.acs.org/appl/literatum/publisher/achs/journals/content/jacsat/2012/jacsat.2012.134.issue-14/ja2110784/production/images/large/ja-2011-110784_0004.jpeg)

#### $3_{10}$-helix

A $3_{10}$ helix is a type of secondary structure found in proteins and polypeptides. Of the numerous protein secondary structures present, it is the 4th most common type observed; following $\alpha$-helices, $\beta$-sheets and reverse turns. $3_{10}$ helices constitute nearly 10%-15% of all helices in protein secondary structures, and are typically observed as extensions of $\alpha$-helices fond at either their N- or C- termini.


#### alamethicin

Predominantly helical with an N-terminal $\alpha$-helix and a C-terminal domain containing a $3_{10}$-helical element. The Pro14 residue separating the two domains induces a $20^\circ-35^\circ$ bend in alamethicin

#### SFG result

- 1670$cm^{-1}$: a helical structure dominated by $\alpha$-helix with minor contribution from a $3_{10}$-helix
- 1635: $3_{10}$-helical structure
- 1720: carbonyl groups of lipid bilayer
- the relationship between the measured ppp and ssp intensity ratios of the peaks at 1670 and 1635 $cm^{-1}$, it is possible to determine the orientation angles $\theta_1$ and $\theta_2$
- SFG signal intensity is related to the number of molecules detected and their orientations

[Surpport Information](https://pubs.acs.org/doi/suppl/10.1021/ja2110784/suppl_file/ja2110784_si_001.pdf)

### [Orientation Determination of Protein Helical Secondary Structures Using Linear and Nonlinear Vibrational Spectroscopy](https://pubs.acs.org/doi/abs/10.1021/jp904153z)

SFG amide I signals can be collected using different polarization combinations of the input laser beams and output signal beam to measure the second-order nonlinear hyperpolarizability elements through the orientation distribution of these helices. Although such orientation information can also be measured using polarized infrared or polarized Raman amide I signals, SFG has a much lower detection limit, which can be used to study the orientation of a helix when its surface coverage is much lower than a monolayer.
$$I_{ssp}\propto (-L_{yy}(\omega)L_{zz}(\omega_1)L_{yy}(\omega_2)sin\beta_2 \chi_{yyz})^2$$
where $L_{ii}(\omega)$ is a Fresnel coefficient and local field correction factor and $\beta,\ \beta_1\ and\ \beta_2$ are angles of the signal, visible and IR beams with respect to the surface normal, respectively.

when input or output beam angle is close to the critical angle of the total internal reflection:
$$I_{ppp}\propto |L_{zz}(\omega)L_{zz}(\omega_1)L_{zz}(\omega_2)sin\beta sin\beta_1sin\beta_2 \chi_{zzz}|^2 $$
![SFG tilt](https://raw.githubusercontent.com/yueliu96/blog_images/master/SFGorien.jpeg)

**Pauling's $\alpha$-Helix**

Pauling's assumption: each peptide bond is planar due to the resonace structure between teh carbonyl C=O bond and teh amide C-N bond. On the basis of this assumption, two helical models were constructed and proposed, a $\gamma$-helix (not discovered in any protein structures) and an $\alpha$-helix, with 5.1 residues per turn and 3.6 residues per turn, respectively.

$\alpha$-helix: it repeats itselt every 5.4 $\overset{\circ}{A}$ along the helical axis. Every backbone carbonyl C=O and N-H group on a peptide unit is hydrogen bonded to another N-H and C=O, respectively. Additionally, the backbone C=O groups point in the same direction, while the N-H groups point in the opposite direction.

Three amide I vibrational modes of $\alpha$-helices, A, $E_1$ and $E_2$. A and $E_1$ are IR-active, while the all three modes are Raman-active. Because a SFG-active mode needs to be both IR- and Raman-active, only the A and $E_1$ modes are SFG-active.

**theory**

For short $\alpha$-helices, whose number of peptide units not close to 3.6 or 7.2 may be influenced by a breaking of the symmetry, it is important to calculate the molecular hyperpolarizability ratios $\beta_{aac}/\beta_{ccc}$ and $\beta_{aca}/\beta_{ccc}$ For idal $\alpha$-helical structures, either a unit cell with 18 peptide units (for 5 turns) or an infinitely long $\alpha$-helix:

$$
\chi_{A,xxz}=\chi_{A,yyz}=\frac{1}{2}N_S[(1+r)<cos\theta>-(1-r)<cos^3\theta>]\beta_{ccc}\\\\
\chi_{A,zzz}=N_S[r<cos\theta>+(1-r)<cos^3\theta>]\beta_{ccc}\\\\
\chi_{E_1,xxz}=\chi_{E_1,yyz}=-N_S(<cos\theta>-<cos^3\theta>)\beta_{aca}\\\\
\chi_{E_1,zzz}=2N_S(<cos\theta>-<cos^3\theta>)\beta_{aca}\\\\
\beta_{aca}\approx0.32\beta_{ccc} \text{, depolarization ratio }r=\beta_{aac}/\beta_{ccc}\approx 0.54$$

For any $\alpha$-helix longer than 18 peptide units, the extra units (any peptide units beyond a multiple number of repeated helical units) are much less than the normal units. In this case, the deviation fron the $\alpha$-helical symmetry should be minimal, and the SFG data analysis for a perfec $\alpha$-helix can be approximately applied.

For short $\alpha$-helices, whose number of peptide units not close to 3.6 or 7.2 may be influenced by a breaking of the symmetry, it is important to calculate the molecular hyperpolarizability ratios $\beta_{aac}/\beta_{ccc}$ and $\beta_{aca}/\beta_{ccc}$ 

All $\alpha$-helices in a sample may not adopt the exact same orientation. Use a gaussian distrubution to describe the orientation distribution: the average orientation and orientation distribution width need to be simultaneously deduced. SFG can measure two orientation parameters, $<cos\theta>$ and $<cos^3\theta>$. To deduce Gaussian distribution, these two parameters need to be measured independently, so the absolute intensity of the SFG signal needs to be obtained.

However, the orientation distribution may sometimes ne more complicated than a Gaussian distribution. If the same helix adopt two different orientations with separate orientation angles $\theta_1$ and $\theta_2$, ATR-FTIR is needed. In ATR-FTIR studies, the tilt angle of an $\alpha$-helix can be calculated from the order parameter $(S_\theta)$, which is defined as $S_\theta=\frac{3<cos^2\theta>-1}{2}$. $<cos^2\theta>$ can be determined from the measured intensity ratio in ATR-FTIR using p- and s-polarized IR light.

Also, a maximum entropy distribution function can be used as a trial function for determining the orientation distribution. Mathematically, this function can have the minimum amount of bias depending on the number of available measured parameters. If the orientation distribution is still difficult to deduce after using combined vibrational spectroscopic studies, isotope-labled proteins can be used, similiar to those in NMR studies.

### [Interactions of Alamethicin with Model Cell Membranes Investigated Using Sum Frequency Generation Vibrational Spectroscopy in Real Time in Situ](https://pubs.acs.org/doi/10.1021/jp911174d)
![alam tilt](https://raw.githubusercontent.com/yueliu96/blog_images/master/alam%20helix%20angle.jpeg)

#### SFG advantage

- intrinsically surface-sensitive
- require small amount of samples
- probe surfaces and interfaces in situ in real-time
- polarized vibrational spectroscopy
  - idenfication of interfacial molecular species
  - orientation and its distribution of functional groups on a surface or at an interface

#### Note

- two peaks: 1635 & 1670:
  - 1670 higher than normal (1660) is dominatedly contributed by $\alpha$-helix (1-13 residues) but with a $3_{10}$-heix part (14-20 residues)
  - 1635: $3_{10}$-helix 
  - two helcial segments because of the presence of the helix-breaking Pro14 residue
- 1685: antiparallel $\beta$-sheet or aggregated strand of peptides
- lipid chain length is one of the factors that determine the phase of the lipid bilayer at room temperature
  - similiar lipids with londer chains tend to exist in the gel phase, wheras shorter chains are likely in the fluid phase

### <jump id='2tilt'>[Multiple Orientation of Melittin inside a Single Lipid Bilayer Determined by Combined Vibrational Spectroscopic Studies](https://pubs.acs.org/doi/abs/10.1021/ja067446l)</jump>
![2tilt](https://raw.githubusercontent.com/yueliu96/blog_images/master/2helixtilt.jpeg)

combine SFG with attenuated total refkection-Fourier transform infrared spectroscopy (ATR-FTIR) to investigate the orientation of $\alpha$-helical peptides reconstituted in substrate supported lipid bilayers.

**theoretical background**

ATR-FTIR: $S_\theta=(3<cos^2\theta>-1)/2$, with $S_\theta=1$ representing helices orientated perpendicularly to the surface and $S_\theta=-0.5$ representing helices lying down parallel to the surface. For most biological samples, however, $S_\theta$ is between -0.5 and 1, and there can be ambiguity as to exact orientation of helices. SFG can be used to measure two additional independent parameters, $<cos\theta>$ and $<cos^3\theta>$ and thus greatly reduce teh ambiguity involved.

In order to deduce the orientation of $\alpha$-helices from SFG signals obtained using various polarization combinations, we need to know how $\chi^{(2)}$, the second-order surface susceptibility of interfacial peptides in the lab coordinate system, is related to $\beta^{(2)}$, the hyperpolarizability of an $\alpha$-helix in the molecular coordinate system.

**SFG Hyperpolarizability of a Bent Helix**

represent the peptide as being composed of two $\alpha$-helices, with an interhelical angle $\theta_h$ between N-terminal helix segment and the C-terminal helix segment. The final form of $\chi$ is thus a function of both $\psi$ and $\theta$.

![bent tilt](https://raw.githubusercontent.com/yueliu96/blog_images/master/bent2tilt.jpeg)

Figure a and b show how $|\chi_{zzz}/\chi_{yyz}|$ changes as a function of $\theta$ and $\psi$ in a 3-D plot and a contour plot, assuming a 135$^\circ$ interhelical angle $\theta_h$.

![more bent tilt figure](https://raw.githubusercontent.com/yueliu96/blog_images/master/Screen%20Shot%202019-02-03%20at%2016.09.43.png)

**Orientation Distribution Function**

one way to determine protein orientation distribution functions is to study how proteins interact with polarized light. The Gaussian function $(1/\sigma 2\pi)exp((-\theta-\theta_0)^2/(2\sigma^2))$, which requires the determination of two parameters: both the mean tilt angle $\theta_0$ and the distribution width $\sigma$.

![tilt&ditribution](https://raw.githubusercontent.com/yueliu96/blog_images/master/tilt2distri.jpeg)

**Maximum entropy theory**

the least biased approach in deducing orientation distribution based on limited measurables. [reference](https://pubs.acs.org/doi/abs/10.1021/jp077556u)

$$
\begin{aligned}
G(\theta)=&e^{-\sum_i \lambda_i cos^i\theta}\\
1=&\int_{-1}^1 G(\theta)\sqrt{1-cos^2\theta}\mathrm{d}cos\theta\\
<cos\theta>=&\int_{-1}^1 cos\theta G(\theta)\sqrt{1-cos^2\theta} \mathrm{d}cos\theta\\
<cos^2\theta>=&\int_{-1}^1 cos^2\theta G(\theta)\sqrt{1-cos^2\theta}\mathrm{d}cos\theta\\
<cos^3\theta>=&\int_{-1}^1 cos^3\theta G(\theta)\sqrt{1-cos^2\theta}\mathrm{d}cos\theta\\
\end{aligned}
$$

We can also calculate the population of each orientation by integration since the orientation distribution function is normalized.

### <jump id='tiltout'>[In Situ Investigation of Heterotrimeric G Protein βγ Subunit Binding and Orientation on Membrane Bilayers](https://pubs.acs.org/doi/abs/10.1021/ja075542w)</jump>

This is the first time that SFG has been used to deduce the orientation of a peripheral membrane protein.

Soluble $G\beta_1\gamma_2$ generated weaker signals, with peak centered at 1630 $cm^{-1}$. This means it associates at best weakly with the surface, and when it does the $\beta$-propeller faces the membrane surface. At this orientaiton the helical domains orient more or less parallel to the surface. Therefore, the$\beta$-propeller of $G\beta_1$ should be able to generate some SFG amide signals due to its interaction with the surface despite its native semi-centrosymmetry, but $\alpha$-helices lying down generate no or extremely weak ssp and ppp SFG signals.

The injection of geranylgeranylated $G\beta_1\gamma_2$ resulted in significantly stronger SFG signals at 1650. It is anchored to the membrane via the geranylgeranyl group with the $\beta$-propeller more or less oeroendicular to the surface. Under this circumstance, the helical domains are no longer parallel to the surface and hence contribute the dominant spectral features. Furthermore, the $\beta$-propeller does not substantially interact with the membrane and its signal is minimal.

# To Be Read 

[Structure and Orientation of Interfacial Proteins Determined by Sum Frequency Generation Vibrational Spectroscopy: Method and Application](https://www.sciencedirect.com/science/article/pii/B9780124165960000075?via%3Dihub)

[Molecular Interactions between Magainin 2 and Model Membranes in Situ](https://pubs.acs.org/doi/abs/10.1021/jp904154w)


# Useful Link

1. [Protein Secondary Structure](http://www.cryst.bbk.ac.uk/PPS2/course/section8/ss-960531_1.html)