---
title: Out of Field Proposal
date: 2019-01-16 15:47:38
tags:
categories:
- NoteBook
---

how concentration, temperature, bilayer, time and pH affects gp41

# [Oligomeric Structure and Three-Dimensional Fold of the HIV gp41 Membrane-Proximal External Region and Transmembrane Domain in Phospholipid Bilayers](https://pubs.acs.org/doi/10.1021/jacs.8b04010)

## HIV-1 glycoprotein, gp41

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

## MPER-TMD Structure

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

## Notes

- $\beta$-strand conformation is correlated with membrane dehydration
- a monomeric membrane-spanning $\alpha$-helix is expected to undergo rapid uniaxial diffusion in the membrane, while a highly oligomerized peptide or a peptide that contains an extended segment on the membrane surface is expected to be immobilized
- MPER-TMD trimer is insensitive to the peptide concentration

## Question
- inconsistent and contradictory structural information abounds in the literature about the C-terminal membrane-interaction region of gp41
- difficulty of crystallizing and solubilizaing the MPER-TMD, most structural studies of this functionally important domain were carried out using either only MPER or only TMD
- FP and TMD disorder the cell and virus membranes by mechanisms that still poorly understood

# [Misfolding of Human Islet Amyloid Polypeptide at Lipid Membrane Populates through β-Sheet Conformers without Involving α-Helical Intermediates](https://pubs.acs.org/doi/10.1021/jacs.8b08537)

## advantage of this article

- quickly capture the transient intermediates in situ and in real time
- identify the formation of $\beta$-hairpin-like monomers, $\beta$-sheet oligomers and fibrils
- reveal the mechanism of amyloid aggregation at the lipid membrane
- method
  - X-ray crystallography: high-rsolution, but not enough time resolution to probe the real-time aggregation

## method

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
    - 1625
    - 1680
  - achiral amide II at 1540: $\beta$-sheet oligomers and fibrils
- loop: achiral: 1660, 1230
- coil: achiral: 1660
- turn: achiral: 1660
  
# [Biological Macromolecules at Interfaces Probed by Chiral Vibrational Sum Frequency Generation Spectroscopy](https://pubs.acs.org/doi/10.1021/cr4006044)

## SFG

Second-order nonlinear optical technique, which uses two pulsed lase sources, one at infrared (IR) frequency ($\omega_{IR}$) and the other ar visible frequency ($\omega_{VIS}$). When this two beams are made to spqtially and temporally overlap at surfaces, a second order nonlinear optical process producing polarization at the sum frequency ($\omega_{IR}+\omega_{VIS}$) can be induced to generate SFG signal.

The electric field of SFG signals $E_{SFG}^I \propto \sum_{JK}\chi_{IJK}^{(2)} E_{VIS}^J E_{IR}^K$. $\chi_{IJK}^{(2)}$ is an element of the second-order susceptibility tensor, which contains structural and chemical information about the target medium. It is nonzero only when the medium lacks centrosymmetry and the second-order susceptibility of an interface consists of a nonresonant term, $\chi_{NR}^{(2)}$, and a sum of vibrationally resonant terms, $\chi_q^{(2)}$
$$\chi^{(2)}=\chi_{NR}^{(2)}+\sum_q \chi_q^{(2)}=\chi_{NR}^{(2)}+\sum_q \frac{A_q}{\omega_{IR}-\omega_q+i\Gamma_q}$$
where $A_q$ is the amplitude, $\Gamma_q$ is the damping coefficient, $\omega_q$ is the resonat frequency of the qth vibrational mode, and $w_{IR}$ is the frequency of the incident IR beam. The SFG signal is enhanced when $\omega_{IR}$ is in resonance with $\omega_q$. Thus, SFG is a surface-specific vibrational spectroscopy