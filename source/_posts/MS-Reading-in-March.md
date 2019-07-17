---
title: MS Reading in March
date: 2019-03-04 09:45:29
tags:
- MS
- DNA
categories:
- MSReading
---

[ETD & internal energy](#ETDE) | [UVPD](#uvpd) | [IRMPD & DFT](#irdft) | [RE & T noncanonical isomer](#Tisomer) | [Rxn & C isomers](#Ciso) | ...

# <jump id='ETDE'>[Kinetic Ion Thermometers for Electron Transfer Dissociation](https://pubs.acs.org/doi/abs/10.1021/jp510244d)</jump>

Peptide fragment ions of the z-type were used as kinetic ion thermometers to gauge the internal energy of peptide cation-radicals produced by electron transfer in the gas-phase. Backbone fragments of the c and z type are engaged in relatively long-lived ion−molecule complexes that allow the **vibrational energy to be redistributed** between the fragments, which presumably occurs **proportionally to their heat capacities**.

**Electron transfer** in a gas-phase cation−anion reaction is a highly **exothermic** process that results in **excitation of the products and often induces their dissociation**. This energy is available to be deposited in the products in the form of **electronic or vibrational excitation**

The fluoranthene molecule requires at least $E_{exc,f}=333kJ/mol (3.45eV)$ of the available energy to form in an excited electronic state. EA(fluoranthene)=58kJ/mol(0.6 eV).

Competing with dissociation, ions A undergo **cooling collisions** with the He gas in the ion trap, forming a fraction of nonreactive ions A'. Furthermore, the average energy transferred per collision with He, estimated at 0.44 kJ/mol, is expected to be highest at high ion internal energies, which may account for the loss of 150−200 kJ/mol in 340−450 collisions.


# <jump id='uvpd'>UVPD in Ion Trap</jump>

The one on  the left is for dissociative single-photon excitation where the excited state is unbound. The one on the right is for excitation followed by internal conversion to a vibrationally highly excited ground electronic state that dissociates.  The conditions for single photon action are as follows:
- The photon energy must be greater than the ion dissociation energy (Edis)
- The dissociation must occur on the time scale of the experiment.  In our case of ions in a ion traps, the dissociation must be faster than collisional cooling that proceeds on the 20-50 ms time scale according to [Rob Pepin's kinetic measurements](#ETDE).  So, both the photon energy, and the dissociation kinetics are important for observing an action band.

# <jump id='irdft'>[Assigning Structures to Gas-Phase Peptide Cations and Cation-Radicals. An Infrared Multiphoton Dissociation, Ion Mobility, Electron Transfer, and Computational Study of a Histidine Peptide Ion](https://pubs.acs.org/doi/abs/10.1021/jp3000784)</jump>

Gas-phase peptide ions can exist as multiple tautomers differing in the protonation sites, and each tautomer can have multiple conformers that are not a priori known or predictable based on the peptide sequence.

Infrared Multiphoton dissociation (IRMPD)
- Limitations: peak intensities sometimes do not correlate with the dipole strength of the corresponding vibrational excitations and difficulties have been noticed with scaling the calculated vibrational frequencies. Strong hydrogen bonding leads to IRMPD bands that are difficult to assign to stretching vibrational modes. 
- The charge-reduced cation-radicals have quite distinct IR spectra that should allow them to be distinguished by ETD-IRMPD when instruments for this technique become available.

Electron structure computations that can handle medium-size (>50 atoms) peptide ions are limited to gradient optimizations using density functional theory (DFT) methods. The most popular DFT hybrid functional (**B3LYP**), in the form that implements the local exchange and correlation functional of Vosko et al. and a nonlocal Lee−Yang−Parr functional with a gradient correction, has a well-recognized deficiency in that it does not fully eliminate two-electron, fourcenter integrals involving the same electron in the exchange part of the functional, leading to what is known as the **electron self-interaction error**. While this error is not critical in small molecular systems, it has been found to be quite **serious for peptide ions of >150 atoms where B3LYP calculations showed convergence collapses**. These problems can possibly be overcome by compensating the energy errors inherent to **B3LYP by perturbational (MP2) energy calculations**. MP2 calculations have been used to assign structures of small peptide ions. However, MP2 scales with the fifth power of the number of electrons/atomic orbitals and becomes prohibitively expensive when the molecular size exceeds about 100 atoms, corresponding to a peptide ion of 6−7 amino acid residues. In this paper, both the **wB97X and M06-2X relative energies are very close to those from averaged B3LYP and MP2 calcualtions**.

The charge-reduced peptide cation-radicals had collisional cross sections that were nearly identical to those of the precursor dications. This indicated that **the peptide cation-radicals retained specific hydrogen bonding motifs from the precursor ion**.

# <jump id='Tisomer'>[Experimental Evidence for Noncanonical Thymine Cation Radicals in the Gas Phase](https://pubs.acs.org/doi/abs/10.1021/acs.jpcb.7b09872)</jump>

- Among the DNA nucleobases, thymine has the **highest ionization energy** (8.8-9.4 eV) and **highest electrochemical oxidation potential** -- T: nonreactive spacer; T cation radical: electron acceptor.

- But A-T-rich DNA models demonstrated the high reactivity of the ionized T nucleobase. Another reaction indicates deprotonation followed by oxygen addition to the C-7-H$_2$ radical. An important finding in these studies was the theoretical existence of a low-energy tautomer of $T^{+\bullet}$

- Exotermic charge-transfer ion-molecule reactions typically proceed at the collision rate and provide a sensitive probe of ion structure in situations where isomeric ions differ in their adiabatic recombination enerigies (REs). 
$$A^+ + B \rightarrow A + B^+ \text{ when RE(A)>RE(B)} $$

- 50 ms is a benchmark ion residence time in the ion trap

- T: loss of HNCO (m/z 83) and loss of (HNCO+CO) (m/z 55)

**Summary**: The reaction of T+gaseous anisole (IE=8.42eV) cation occurs on a rate of 20% indicataes major T: RE<8.42eV. Demonstarted by the calculation of the existence of noncononical $T^{+\bullet}$ (RE<5.9eV). Isomerization occurs probably during the process of collision


# <jump id='Ciso'>[Cytosine Radical Cations: A Gas-Phase Study Combining IRMPD Spectroscopy, UVPD Spectroscopy, Ion–Molecule Reactions, and Theoretical Calculations](https://onlinelibrary.wiley.com/doi/full/10.1002/cphc.201700281)</jump>

- Such solvent-free analysis is unencumbered by multi-conformational averagin g and counterion efffects, allowing for direct experimental observation of the specific radical species
- isomerization between the low-energy isomers of the cytosine radical cation would require less energy than their fragmentation.
- C: loss of CO (m/z 83) amd loss of (NCO) (m/z 69)
- if an electron is stripped from the Cyt site, resulting in a transient radical cation species, a facile hydrogen-atom or electron-transfer reaction may follow. This will lead to propagation of the radical site either intramolecularly within the DNA strand or intermolecularly through reactions with neighboring species
- highly delocalized phenoxy radicals display reactivity towards nitric oxide even if the spin density at the oxygen atom is as low as 0.17
- $A^{\bullet +}+B\rightarrow A + B^{\bullet +}$ when B has a lower ionization potential (IP). IP(Cyt) = 8.695 - 8.738eV
- $M^{\bullet +}+RSH\rightarrow MH^+ +RS^\bullet$: hydrogen abstraction of $Cyt^{\bullet +}$: exothermic (~75kJ/mol) and a small activation barrier

**Summary**: IRMPD, UVPD and calculation favors a mixture of protonated cytosine cation radicals (C-H2 or C-H3) from CID oxidation of $[Cu^{II}(terpy)(M)]^{\bullet 2+}$. The $Cyt^{\bullet +}$ isomeric mixture might originate from different $[Cu^{II}(terpy)(M)]^{\bullet 2+}$ isomers present in solution, or from the gas-phase rearrangement of $Cyt^{\bullet +}$ upon CID of the Cu complex. A high-energy disonic isomer, a reasonalbe match with UVPD spectra, is unlikely formed.
