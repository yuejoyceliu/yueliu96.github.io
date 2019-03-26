---
title: Introduction to Computational Chemistry
date: 2019-03-09 21:24:33
tags:
- ComputChem
categoreis:
- NoteBook
---

**Reference** Jensen, F., 2017. Introduction to computational chemistry. John wiley & sons.

A Z-matrix is a conventient way of specifying a molecular geometry in terms of internal coordinates, and it is used by many electronic structure programs. Futhermore, geometry optimizations are often performed in Z-matirx variables, and since optimizations in a good set of internal coordinates are significantly faster than in Cartesian coordinates.

# 1. Introduction

Given a set of nuclei and electrons, theoretical chemistry can attempt to calculate things such as:

1. The geometrical arrangements of the nuclei that correspond to stable molecules.
2. Their relative energies.
3. Their properties (dipole moment, polarizability, NMR coupling constants etc.).
4. The rate by which one stable molecule can transform into another
5. The time dependence of molecular structures and properties.

One of the main problems in computational chemistry is selecting a suitable level of theory for a given problem, and being able to evaluating the quality of the obtained results.

## 1.1 Background

**Chemistry is knowing the energy as a function of the nuclear coordinates.**

**Properties are knowing how the energy changes upon adding a perturbation.** The link between the properties of a single molecule, or a small collection of molecules, and the macroscopic observable, is statistical mechanics. Macroscopic properties, such as temperature, heat capacities, entropies etc., are the net effect of a very large number of molecules having a certain distribution of energies.

$$
\begin{aligned}
\mathbf H_{tot}\Psi_{tot}(\mathbf R, \mathbf r) &= E_{tot}\Psi_{tot}(\mathbf R, \mathbf r) \\
\mathbf H_{tot} &= \mathbf H_e +\mathbf T_n \\
\mathbf H_{et} &= \mathbf T_e + \mathbf V_{ne} +\mathbf V_{ee} + \mathbf V_{nn} \\
\Psi_{tot}(\mathbf R,\mathbf r) &= \Psi_n(\mathbf R) \Psi_e (\mathbf R, \mathbf r) \\
\mathbf H_e \Psi_e(\mathbf R, \mathbf r) &= E_e(\mathbf R) \Psi_e (\mathbf R, \mathbf r) \\
(\mathbf T_n + E_e(\mathbf R)) \Psi_n(\mathbf R) &= E_{tot}\Psi_n(\mathbf R) \\
\end{aligned}
$$

**Born-Openheimer (BO) approxiamtion**: The Schrodinger equation can be separated into one part which describes the electronic wavefunction for a fixed nuclear geometry, and another part which describes the nuclear wavefunction. where the energy from the electronic wave function plays the role of potential energy. The electronic wave function depends parametrically on the nuclear coordinates. The picture is that the nuclei move on **Potential Energy Surface (PES)**, which are solutions to the electronic Schrodinger equation. (nuclei: R, n; electrons: r, e). The interesting parts of a PES are usually nuclear arrangements which have low energies. For example, nuclear movements near a minimum on the PES, which corresponds to a stable molecule, are molecular vibtrations. Chemical reactions correspond to large movements, and may in the simplest approximation be described by locating the lowest energy path leading from one minimum on the PES to another.

Electrons are very light particles and cannot be described by classical mechanics, while neclei are heavy enough for neglecting quantum effects. If nuclei showed significant quantum aspects, the concept of molecular strucutre would not have any meaning, the nuclei would simply tunnel through barriers and end up in the global minimum. Furthermore, it would not be possible to speak of a molecular geometry, since the Heisenberg uncertainty principle would not permit a measure of nuclear positions to an accuracy much smaller than the molecular dimension.

# 2. Force Field Methods

## 2.1 Introduction

In *Force Field* (FF) or *Molecular Mechanics* (MM) methods, electronic structrue calculations are achieved by writing $E_e$ as a parametric function of nuclear coordinates, and molecules are modelled as atoms held together by bonds. Atoms have different sizes and "softness" and bonds are more or less "stiff". i.e. the molecule is described by a "ball and spring" model. The foundation of FF methods is the observation that molecules tend to be composed of units which are structurally similiar in different molecules. The picture of molecules being composed of structural units, "functional groups", which behave similiarly in different molecules forms the very basis of organic chemistry.

## 2.2 The Force Field Energy

$$E_{FF}=E_{str}+E_{bend}+E_{tors}+E_{vdw}+E_{el}+E_{cross}$$

### 2.2.1 The stretch Energy

$E_{str}$ is the energy function for stretching a bond between two atom types A and B. Its simples form is written as a Taylor expansion around a "natural", or "equilibrium", bond length $R_0$. ($\Delta R = R^{AB}-R_0^{AB}$)

$$E_{str}(\Delta R)=E(0)+k_2(\Delta R)^2 +k_3(\Delta R)^3+k_4(\Delta R)^4+\cdots$$

- E(0)=0: zero point for the energy scale
- terminated at 2nd order: harmonic form
- terminated at 3rd order: $k_3<0, E\rightarrow -\infty$ for long bond lengths
- terminated at 4th order: $k_4>0, E\rightarrow +\infty$ for long bond lengths
- Morse potential satisfies the energy converges towards the dissociation energy for a large bond length, but it converges slowly for lond bond lengths.

$$E_{Morse}(\Delta R)=D[1-e^{\alpha \Delta R}]^2$$

For the large majority of systems, including simulations, the only important chemical region is up to ~10 kcal/mol above the bottom of the PES curve. In this reghion, a 4th order polynomial is essentially indistinguishable form a Morse, and even a simple harminic approximation does a quite good job.

The $R_0$ isn't equilibrium bond lenght for any molecule! The other terms of a polyatomic molecule in FF energy will usually produce a minimum energy structure with bond lengths slightly longer than $R_0$. Essentially all molecules have bond lengths which devieate very little from their "natural" values, typically less than 0.003nm. For this reason, a simple harmonic, or possibly a cubic expansion, is usually sufficient for reproducing experimental geomertries.

### 2.2.2 The Bending Energy

$E_{bend}$ is the energy required for bending an angle formed by three atoms A-B-C. Since chemically important region is below ~10 kcal/mole above the bottom, and the energy coset for bending is so large that most molecules only deviate a few degrees from their natural bond angles, the harmonic term is adequate for most applications. Special atom types are often defined for small rings.

### 2.2.3 The Out-of-plane Bending Energy

The in-plane angle deformations for a planar structure become unrealistically stiff, so a special *out-of-plane energy bend term* ($E_{oop}$ or $E_{inv}$) is usually added to increase in inversion barrier in $sp^3$-hybridized atoms (i.e. an extra energy penalty for being planar). Inversion barriers are in most cases (e,g, $NR_3$) adequately modelled without an explicit $E_{inv}$ term, the barrier arising naturally from the increase in bond angles upon inversion and improper torsinal energy.

### 2.2.4 The Torsional Energy

$E_{tors}$ is the energy change associated with rotation around a B-C bond in a four atom sequency A-B-C-D. Differing from $E_{str}$ and $E_{bend}$, $E_{tors}$ is periodic in angle $\omega$, and the cost in energy for distorting a molecule by rotation around a bond is often low.

$$E_{tors}(\omega)=\sum_{n=1}V_n cos(n\omega)$$

Molecules that are composed of atoms having a maximum valency of 4 are with a few exceptions found to have rotational profiles showing at most three minima. The first three terms are sufficient for qualitatively reproducing such profiles. FF methods which are aimed at large systems often limit the Fourie series to only one term, depending on the bond type (e.g. single bonds only have $cos(3\omega)$ and double bonds only have $cos(2\omega)$). Exceptions from the regular three minima rotational profile around single bonds are caused by repulsive and attractive van der Waals interactions, and can still be modeled by having only terms up to $cos(3\omega)$ in the torsional energy expression. Cases where higher-order terms probably are necessary are those with ratation around bonds to octaheral coordinated metals (Ru(pyridine)$_6$), or a dinuclear complex ($Cl_4Mo-MoCl_4$).

### 2.2.5 The van der Waals Energy

$E_{vdw}$ is the van der Waals energy decribing the repulsion or attraction between atoms that are not directly bonded. $E_vdw$ is very positive at small distances (electron replusion), has a minimum which is slightly negative at a distance corresponding to the two atoms just "touching" each other (electron correlation: dipole-dipole interaction and London force), and goes towards zero as the distance becomes large. Lennard-Jones potential, computationally more efficient, gives results comparable to the more accurate functions, even if its repulsive interaction is bad.
$$E_{LJ}(R)=\varepsilon[(\frac{R_0}{r})^{12}-2(\frac{R_0}{R})^6]$$

Shortcomings:

- $E_{vdw}$ is calculated between pairs of atoms, but it includes many-body contributions in real systems
- atoms are treated as spheres. two exceptions:
  - H-X: electron distirbution around the hydrogen nucleus is not spherical (more spherical for increasing electron numbers), rather the electron distribution is displaced towards the other atom and it affects H's elecgron density a lot (e.g. oxygen or nitrogen leads to a smaller effective van der Waals radius for the hydrogen, than if it is bonded to carbon.)
  - atoms have lone pairs, like O and N: these electrons are more diffuse than the electrons invovled in bonding, and the atoms is ths "larger" in the lond pair direction.
  - H bonds require special attention: such bond strength 2-5 kcal/mol, while normal single bonds are 60-110kcal/mol and van der Waals interaction are 0.1-0.2 kcal/mol.

### 2.2.6 The Electrostatic Energy

The other part of the non-bonded interaction is due to internal distributon of the electrons, creating positive and negative parts of the molecule. This may be modelled by assiging charges to each atom, or the assigning a bond dipole moment to the bond. Two methods give similiar, but not identical results. 

"Many-body" effects, similiar to VDW, can be modelled by including an atom polarization, but often neglect due to computational time. Another question is how far apart should two atoms be before a non-bonded energy term contributes to $E_{FF}$? It is clear that two atoms directly bonded should not have an $E_{vdw}$
or $E_{el}$ term; their interaction is described by $E_{str}$. Most modern force fields calculate $E_{str}$ between all atoms pairs which are 1,2 with respect to each other in terms of bonding, $E_{bend}$ for all pairs which are 1,3, $E_{tors}$ between all pairs which are 1,4, and $E_{vdw}/E_{el}$ between all pairs which are 1,4 or higher.

### 2.2.7 Cross Term

The first five terms are common to all force fields. This term covers coupling between these fundamental, or diagonal terms, (e.g. a term depends on both bond length and angle). It should be noted that some types of cross terms are unstable if the geometry is far from equilibrium.

### 2.2.8 Small Rings and Conjugated Systems

**Small Rings**: If a sufficient number of cross terms is included, however, the necessary number of atom types can be actually reduced, i.e. the cross terms modify the diagonal terms so that a more realistic behaviour is obtained for large deviations from the nature value.

**Conjugated System**: e.g. according to the MM2 type convention, all carbond atoms of 1,3-butadiene are of the same type. But the outer C-C bond is slightly reduced in double bond character while the central bond is roughly halfway between a single and a double bond. Also, the rotational barrier for the central bond is calculated to be ~55kcal/mol, while only ~6kcal/mol in experiment. Two approaches to deal with this case, one is to identify certain bonding combinations and use special parameters for these cases; the other is to perform a simple electronic structure calculation to determine the degree of delocalization within the $\pi$-system. The main problem of the first method is there are so many such special cases, while the other method is compuational expensive and requires additional iteration.

The natural bond length varies between 1.503 $\text{\AA}$ and 1.337 $\text{\AA}$ for bond orders between 0 and 1, these are values for pure single and double bonds between two $sp^2$-carbons. The rotational barrier for an isolated double bond is 60kcal/mol.

### 2.2.9 Comparing Energies of Structurally Different Molecules

The zero point of the energy in each term has so far been choosen for convenience. The force field energy, $E_{FF}$, is often called the *steric energy* as in some sense it is the excess energy relative to a hypothetical molecule with non-interacting fragments. This is inconsequential for comparing energies of different conformations of the same molecule, i.e. where the atom types and bonding are the same.

$$\Delta H_f = E_{FF} + \sum^{bonds} \Delta H_{AB} + \sum^{groups} \Delta H_G$$

To convert the steric energy to heat of formation, terms can be added depending on the number and types of bond present in the molecule. Since correctrions from larger moities are small, it follows that energy differences between systems having the same groups can be calculated directly from differences in steric energy.

## 2.3 Force Field Parameterization