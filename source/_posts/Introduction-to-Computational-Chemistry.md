---
title: Introduction to Computational Chemistry
date: 2019-03-09 21:24:33
tags:
- ComputChem
categories:
- NoteBook
---

**Reference** Jensen, F., 2017. Introduction to computational chemistry. John wiley & sons.

A Z-matrix is a convenient way of specifying a molecular geometry in terms of internal coordinates, and it is used by many electronic structure programs. Furthermore, geometry optimizations are often performed in Z-matrix variables, and since optimizations in a good set of internal coordinates are significantly faster than in Cartesian coordinates.

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

**Born-Openheimer (BO) approximation**: The Schrodinger equation can be separated into one part which describes the electronic wave function for a fixed nuclear geometry, and another part which describes the nuclear wave function. where the energy from the electronic wave function plays the role of potential energy. The electronic wave function depends parametrically on the nuclear coordinates. The picture is that the nuclei move on **Potential Energy Surface (PES)**, which are solutions to the electronic Schrodinger equation. (nuclei: R, n; electrons: r, e). The interesting parts of a PES are usually nuclear arrangements which have low energies. For example, nuclear movements near a minimum on the PES, which corresponds to a stable molecule, are molecular vibrations. Chemical reactions correspond to large movements, and may in the simplest approximation be described by locating the lowest energy path leading from one minimum on the PES to another.

Electrons are very light particles and cannot be described by classical mechanics, while nuclei are heavy enough for neglecting quantum effects. If nuclei showed significant quantum aspects, the concept of molecular structure would not have any meaning, the nuclei would simply tunnel through barriers and end up in the global minimum. Furthermore, it would not be possible to speak of a molecular geometry, since the Heisenberg uncertainty principle would not permit a measure of nuclear positions to an accuracy much smaller than the molecular dimension.

# 2. Force Field Methods

## 2.1 Introduction

In *Force Field* (FF) or *Molecular Mechanics* (MM) methods, electronic structure calculations are achieved by writing $E_e$ as a parametric function of nuclear coordinates, and molecules are modeled as atoms held together by bonds. Atoms have different sizes and "softness" and bonds are more or less "stiff". i.e. the molecule is described by a "ball and spring" model. The foundation of FF methods is the observation that molecules tend to be composed of units which are structurally similar in different molecules. The picture of molecules being composed of structural units, "functional groups", which behave similarly in different molecules forms the very basis of organic chemistry.

## 2.2 The Force Field Energy

$$E_{FF}=E_{str}+E_{bend}+E_{tors}+E_{vdw}+E_{el}+E_{cross}$$

### 2.2.1 The stretch Energy

$E_{str}$ is the energy function for stretching a bond between two atom types A and B. Its simples form is written as a Taylor expansion around a "natural", or "equilibrium", bond length $R_0$. ($\Delta R = R^{AB}-R_0^{AB}$)

$$E_{str}(\Delta R)=E(0)+k_2(\Delta R)^2 +k_3(\Delta R)^3+k_4(\Delta R)^4+\cdots$$

- E(0)=0: zero point for the energy scale
- terminated at 2nd order: harmonic form
- terminated at 3rd order: $k_3<0, E\rightarrow -\infty$ for long bond lengths
- terminated at 4th order: $k_4>0, E\rightarrow +\infty$ for long bond lengths
- Morse potential satisfies the energy converges towards the dissociation energy for a large bond length, but it converges slowly for lone bond lengths.

$$E_{Morse}(\Delta R)=D[1-e^{\alpha \Delta R}]^2$$

For the large majority of systems, including simulations, the only important chemical region is up to ~10 kcal/mol above the bottom of the PES curve. In this region, a 4th order polynomial is essentially indistinguishable form a Morse, and even a simple harmonic approximation does a quite good job.

The $R_0$ isn't equilibrium bond length for any molecule! The other terms of a polyatomic molecule in FF energy will usually produce a minimum energy structure with bond lengths slightly longer than $R_0$. Essentially all molecules have bond lengths which deviate very little from their "natural" values, typically less than 0.003nm. For this reason, a simple harmonic, or possibly a cubic expansion, is usually sufficient for reproducing experimental geometries.

### 2.2.2 The Bending Energy

$E_{bend}$ is the energy required for bending an angle formed by three atoms A-B-C. Since chemically important region is below ~10 kcal/mole above the bottom, and the energy cost for bending is so large that most molecules only deviate a few degrees from their natural bond angles, the harmonic term is adequate for most applications. Special atom types are often defined for small rings.

### 2.2.3 The Out-of-plane Bending Energy

The in-plane angle deformations for a planar structure become unrealistically stiff, so a special *out-of-plane energy bend term* ($E_{oop}$ or $E_{inv}$) is usually added to increase in inversion barrier in $sp^3$-hybridized atoms (i.e. an extra energy penalty for being planar). Inversion barriers are in most cases (e,g, $NR_3$) adequately modeled without an explicit $E_{inv}$ term, the barrier arising naturally from the increase in bond angles upon inversion and improper torsinal energy.

### 2.2.4 The Torsional Energy

$E_{tors}$ is the energy change associated with rotation around a B-C bond in a four atom sequence A-B-C-D. Differing from $E_{str}$ and $E_{bend}$, $E_{tors}$ is periodic in angle $\omega$, and the cost in energy for distorting a molecule by rotation around a bond is often low.

$$E_{tors}(\omega)=\sum_{n=1}V_n cos(n\omega)$$

Molecules that are composed of atoms having a maximum valency of 4 are with a few exceptions found to have rotational profiles showing at most three minima. The first three terms are sufficient for qualitatively reproducing such profiles. FF methods which are aimed at large systems often limit the Fourier series to only one term, depending on the bond type (e.g. single bonds only have $cos(3\omega)$ and double bonds only have $cos(2\omega)$). Exceptions from the regular three minima rotational profile around single bonds are caused by repulsive and attractive van der Waals interactions, and can still be modeled by having only terms up to $cos(3\omega)$ in the torsional energy expression. Cases where higher-order terms probably are necessary are those with rotation around bonds to octahedral coordinated metals (Ru(pyridine)$_6$), or a dinuclear complex ($Cl_4Mo-MoCl_4$).

### 2.2.5 The van der Waals Energy

$E_{vdw}$ is the van der Waals energy describing the repulsion or attraction between atoms that are not directly bonded. $E_vdw$ is very positive at small distances (electron repulsion), has a minimum which is slightly negative at a distance corresponding to the two atoms just "touching" each other (electron correlation: dipole-dipole interaction and London force), and goes towards zero as the distance becomes large. Lennard-Jones potential, computationally more efficient, gives results comparable to the more accurate functions, even if its repulsive interaction is bad.

$$E_{LJ} (R)=\varepsilon [(\frac{R_0}{r})^{12}-2(\frac{R_0}{R})^6]$$

Shortcomings:

- $E_{vdw}$ is calculated between pairs of atoms, but it includes many-body contributions in real systems
- atoms are treated as spheres. two exceptions:
  - H-X: electron distribution around the hydrogen nucleus is not spherical (more spherical for increasing electron numbers), rather the electron distribution is displaced towards the other atom and it affects H's electron density a lot (e.g. oxygen or nitrogen leads to a smaller effective van der Waals radius for the hydrogen, than if it is bonded to carbon.)
  - atoms have lone pairs, like O and N: these electrons are more diffuse than the electrons involved in bonding, and the atoms is "larger" in the lone pair direction.
  - H bonds require special attention: such bond strength 2-5 kcal/mol, while normal single bonds are 60-110kcal/mol and van der Waals interaction are 0.1-0.2 kcal/mol.

### 2.2.6 The Electrostatic Energy

The other part of the non-bonded interaction is due to internal distribution of the electrons, creating positive and negative parts of the molecule. This may be modeled by assigning charges to each atom, or the assigning a bond dipole moment to the bond. Two methods give similar, but not identical results. 

"Many-body" effects, similar to VDW, can be modeled by including an atom polarization, but often neglect due to computational time. Another question is how far apart should two atoms be before a non-bonded energy term contributes to $E_{FF}$? It is clear that two atoms directly bonded should not have an $E_{vdw}$
or $E_{el}$ term; their interaction is described by $E_{str}$. Most modern force fields calculate $E_{str}$ between all atoms pairs which are 1,2 with respect to each other in terms of bonding, $E_{bend}$ for all pairs which are 1,3, $E_{tors}$ between all pairs which are 1,4, and $E_{vdw}/E_{el}$ between all pairs which are 1,4 or higher.

### 2.2.7 Cross Term

The first five terms are common to all force fields. This term covers coupling between these fundamental, or diagonal terms, (e.g. a term depends on both bond length and angle). It should be noted that some types of cross terms are unstable if the geometry is far from equilibrium.

### 2.2.8 Small Rings and Conjugated Systems

**Small Rings**: If a sufficient number of cross terms is included, however, the necessary number of atom types can be actually reduced, i.e. the cross terms modify the diagonal terms so that a more realistic behavior is obtained for large deviations from the nature value.

**Conjugated System**: e.g. according to the MM2 type convention, all carbon atoms of 1,3-butadiene are of the same type. But the outer C-C bond is slightly reduced in double bond character while the central bond is roughly halfway between a single and a double bond. Also, the rotational barrier for the central bond is calculated to be ~55kcal/mol, while only ~6kcal/mol in experiment. Two approaches to deal with this case, one is to identify certain bonding combinations and use special parameters for these cases; the other is to perform a simple electronic structure calculation to determine the degree of de-localization within the $\pi$-system. The main problem of the first method is there are so many such special cases, while the other method is computational expensive and requires additional iteration.

The natural bond length varies between 1.503 $\text{\AA}$ and 1.337 $\text{\AA}$ for bond orders between 0 and 1, these are values for pure single and double bonds between two $sp^2$-carbons. The rotational barrier for an isolated double bond is 60kcal/mol.

### 2.2.9 Comparing Energies of Structurally Different Molecules

The zero point of the energy in each term has so far been chosen for convenience. The force field energy, $E_{FF}$, is often called the *steric energy* as in some sense it is the excess energy relative to a hypothetical molecule with non-interacting fragments. This is inconsequential for comparing energies of different conformations of the same molecule, i.e. where the atom types and bonding are the same.

$$\Delta H_f = E_{FF} + \sum^{bonds} \Delta H_{AB} + \sum^{groups} \Delta H_G$$

To convert the steric energy to heat of formation, terms can be added depending on the number and types of bond present in the molecule. Since corrections from larger moieties are small, it follows that energy differences between systems having the same groups can be calculated directly from differences in steric energy.

## 2.3 Force Field Parameterization

Inherent contradiction in designing highly accurate force fields:

- problem 1: need numerous experimental data
- solution 1: rely on data from electronic structure calculations to derive force field parameters $\rightarrow$ the electrostatic interaction may be assigned on the basis of fitting parameters to the electrostatic potential derived from an electronic wave function
- problem 2: van der Waals interactions are difficult to calculate reliably by electronic structure methods, requiring a combination of electron correlation and very large basis sets
- solution 2: VDW parameters $\leftarrow$ experimental data for either the solid or liquid state
- problem 3: since the parameterization implicitly takes many-body effects into account, the parameters are not unique

1. functional form of FF

    In MM2(91), fewer parameters are used than estimated ones: two routes for insufficient parameters:
    1. estimate the missing parameters by comparison to force field parameters for similar systems
    2. use external information, experimental or electronic structure calculations

2. how to assign weights for reference data?
3. error function $\rightarrow$ find the global minimum?

$$ErrF(parameter)=\sum_{data}weight \cdot (reference\ value-calculated\ value)^2$$

### 2.3.1 Parameter Reduction in Force Fields

achieve by reducing the dependence on atom types. The quality of force field parameters is essential for judging how much faith can be put in the results.

### 2.3.2 Force Fields for Metal Coordination Compounds

The increased number of ligands combined with the multitude of possible geometries significantly increases the problems of assigning suitable functional forms for each of the energy term.

1. the energy cost for a geometrical distortion (bond stretching and bending) is usually much smaller around a metal atom than for a carbon atom: coordination compounds are much more dynamics and the distance of a given metal-ligand bond is often sensitive to the nature of the other ligand.
2. lack of well-defined bonds.

### 2.3.3 Universal Force Fields

a method with reduced parameters sets: can calculate geometries correctly, but conformational energies are quite poor.

## 2.4 Differences in Force Fields

There are many different force fields in use. They differ in three main aspects:

1. The functional form of each energy term
2. The number of cross terms included
3. The type of information used for fitting the parameters

- large system
    - simple functional forms: only $E_{str}$ and $E_{bend}$ harmonic forms, no cross terms, Lennard-Jones potential for $E_{vdw}$
    - further simplification: united atom approach (i.e. not consider hydrogens explicitly). e.g. a single "$CH_2$ atom" assigned instead of a carbon and two hydrogens for modeling a $CH_2$ group
- small or medium size molecules
    - several cross terms, at least cubic or quartic expansions of $E_{str}$ and $E_{bend}$, and possibly an exponential type potential for $E_{vdw}$

## 2.5 Computational Consideration

Evaluation of the non-bonded energy is by far the most time-consuming. $E_{str}$, $E_{bend}$ and $E_{tors}$, grows linearly with the system size. The non-bonded contributions, $E_{vdw}$(and $E_{el}$), grows as the square of the system size. In the limit of large molecules, the computational time for calculating the force field energy grows approximately as the square of the number of atoms. The majority of these non-bonded energy contributions are numerically very small, as the distance between the atom  pairs is large.

The first solution is to use a cutoff distance, e.g. $10 \text{\AA}$. Besides that, prepare a non-bonded or neighbor list over atom pairs, only calculate their contributions, and update the list at  suitable intervals to avoid calculation of distances between all pairs of atoms.

$E_{vdw}$ becomes small (less than ~0.001kcal/mol) beyond a distance of ~$10\text{\AA}$. But the electrostatic interaction reaches the same level of importance at a distance of ~$30\text{\AA}$. The interaction between net charges is very long range (~$3000\text{\AA}$).

The simplest way of implementing the cut-off approximation is to neglect all contributions if the distance is larger than the cut-off. This is in general not a very good method as the energy function becomes discontinuous. A better method is to use two cut-off distances between which a switch function connects the correct $E_{vdw}$ or $E_{el}$ smoothly with zero. But the chemical significance of the cut-off of course still remains. It is especially troublesome in simulation studies where the distribution of solvent molecules can be very dependent on the use of cut-off.

Obtaining a good description of the electrostatic interaction between molecules (or between different parts of the same molecule) is one of the big problems in force field work. For polar molecules, such as  for example amino acids, the electrostatic interactions are very important. Unfortunately, atom centered point charge models, or bond dipoles, are fairly crude approximations of the real interaction. See more in [section 9.2](#9.2)

## 2.6 Validation of Force Fields

The quality of a force field calculation depends on two things: how appropriate is the mathematical form of the energy expression, and how accurate are the parameters. Reproducibility is another concern.

Force field methods are primarily geared to predict two properties: geometries and relative energies. Structural features are in general much easier to predict than relative energies, which are a consequence of many small contributions, i.e. the exact shape of the individual energy terms and the balance between them. The largest contributions to conformational energy differences are the non-bonded and torsional terms. For large system it is inevitable that small inaccuracies in the functional forms for the energy terms and parameters will influence the shape of the whole energy surface to the point where minima may disappear or become saddle points.

## 2.7 Practical Considerations

Force field methods are models of the real quantum mechanical systems. The total neglect of electrons as individual particles forces the user to define explicitly the bonding present in the molecule prior to any calculations. Input:

1.  The types of atom present
2.  How they are connected
3. A start guess of the geometry

## 2.8 Advantages and Limitations of Force Field Methods

- advantages:
    - speed (allows large systems)
- limitations:
    - unusual molecules (little info);
    - "zero-dimensional" (no error assessment within this method)

## 2.9 Transition Structure Modeling

Structural changes can be divided into two general types: those of a conformational nature and those involving bond breaking/forming. The bottleneck for structural changes is the highest energy point along the reaction path, called the Transition State or Transition Structure ([TS](#ts))
1. Conformational TSs:
    - have the same atom types and bonding for both the reactant and product
    - can be located on the force field energy surface by standard optimization algorithms
    - often localized to rotation around a single bond
2. TSs for reaction:
    - reactant and product are not described by the same set of atom types and/or bonding
    - two different force field energy functions for reactant and product, i.e. the energy as a function of the reactant coordinate is not continuous

methods for modeling differences in activation energies between similar reactions by means of force field techniques

### 2.9.1 Modeling the TS as a Minimum Energy Structure

1. locate the TS for a typical example of the reaction with electronic structure methods, often at ab initio HF level
2. modify FF function to create a TS geometry with minimum energy
3. minimize the structure until the ab initio TS geometry is reproducible
4. relative energy differences between the reactant and the TS model correlates with relative activation energies.

Purely electronic effects, like Hammett type effects due to para-substitution in aromatic systems

- Problem
  - TS is a first-order saddle point, not a minimum
  - invite new parameters

### 2.9.2 Modeling the TS as a Minimum Energy Structure on the Reactant/Product Energy Seam

Energy minimization is subject to the constraint that the reactant and product energies are identical. Only parameters for describing the reactant and product are matter, but require to be more accurate. 

Disadvantages: exothermic reaction produces a lower activation energy, so the FF need to calculate relative energies of the reactant and product, i.e. the ability to convert steric energies to heat of formation. If the result doesn't accurately repeat the real TS, it's hard to modify parameters. The TS is given in terms of the diabatic energy surfaces for the reactant and product, activation energies will be too high, which can be improved by adding a "resonance" term to produce a smooth surface connecting the reactant and product.

## 2.10 Hybrid Force Field-Electronic Structure Methods

FF methods are inherently unable to describe the details of bond breaking/forming reactions, since there is an extensive rearrangement of the electrons, which is neglected in the classical method.

For studying enzymes: assume the whole system is important for holding the active size in the proper arrangement, and the "backbone" conformation may change during the reaction. Hybrid methods have been designed for modeling such cases, where the active size is calculated by electronic structure methods (usually semi-empirical, low-lavel ab initio or DFT methods), while the backbone is calculated by a force field method.

# 3. Electronic Structure Methods

If solutions are generated without reference to experimental data, the methods are usually called *ab initio*, in contrast to [semi-empirical models](#3.9)

## 3.1 The Adiabatic and Born-Oppenheimer Approximations

$$\begin{aligned}
H_{tot} &= T_n+T_e+V_{ne}+V_{ee}+V_{nn}\\
&= T_n+H_e+H_{mp} \text{ (center of mass system)}\\
H_e &= T_e+V_{ne}+V_{ee}+V_{nn}\\
H_{mp} &= -\frac{1}{2M_{tot}}(\sum_{i=1}^N \nabla_i)^2\\
\Psi_{tot}(R,r)&=\sum_i^\infty \Psi_{ni}(R)\Psi_i(R,r), \;\;i=1,2...\infty
\end{aligned}\\
\sum_{i=1}^\infty (T_n+H_e+H_{mp})\Psi_{ni}(R)\Psi_i(r,r) = E_{tot}\sum_{i=1}^\infty \Psi_{ni}(R)\Psi_i(R,r)\\
\nabla^2_n\Psi_{ni}+E_j\Psi_{ni}+\sum_{i=1}^\infty \lbrace 2\langle \Psi_j |\nabla_n|\Psi_i \rangle(\nabla_n\Psi_{ni})+\langle\Psi_j|\nabla_n^2|\Psi_i\rangle\Psi_{ni} +\langle\Psi_j|H_{mp}|\Psi_i\rangle\Psi_{ni}\rbrace = E_{tot}\Psi_{nj} $$

The electronic wave function $\Psi_i$ has been removed from the first two terms while the curly bracket contains terms coupling different electronic states. The first two terms in the curly bracket are the first- and second order non-adiabatic coupling elements, which are important for systems involving more than one electronic surface, such as photochemical reaction. The last element si the mass polarization.

In the **adiabatic approximation** the form of the total wave function is restricted to one electronic surface
$$(\nabla_n^2+E_j+\langle\Psi_j|\nabla_n^2|\Psi_j\rangle+\langle\Psi_j|H_{mp}|\Psi_j\rangle)\Psi_{nj}=E_{tot}\Psi_{nj}$$
neglecting the mass polarization and reintroducing hte kinetic energy operator gives
$$(T_n+E_j(R)+U(R))\Psi_{nj}(R)=E_{tot}\Psi_{nj}(R)$$
U(R) term is known as the *diagonal correction*, and is smaller than $E_j(R)$ by a factor roughly equal to the ratio of the electronic and nuclear masses.It is usually a slowly varying function of R, and the shape of the energy surface is therefore determined almost exclusively by $E_j(R)$. In **Born-Oppenheimer (BO) approximation** the diagonal correction is neglected , and the resulting equation takes on the usual Schrodinger form, where the electronic energy plays the role of a potential energy.
$$(T_n+E_j(R))\Psi_{nj}(R)=E_{tot}\Psi_{nj}(R)\\
(T_n+V_j(R))\Psi_{nj}(R)=E_{tot}\Psi_{nj}(R)$$
In the BO picture the nuclei move on a **potential energy surface** (PES) which is a solution to the electronic Schrodinger equation. Solution of above equation leads to energy levels for molecular vibrations and rotations, which in turn are fundamentals for may forms of spectroscopy, such as IR, Raman, microwave etc.

When two or more solutions to the electronic Schrodinger equation (S.E.) come close together energetically, adiabatic and therefore BO approximation breaks down.

We implicitly neglected relativistic effect (important for the 4th and 5th rows an d transition metals, see [Chapter 8](#chp8)), so need to introduce an ad hoc quantum effect for spin-dependent terms, which are calculated as corrections (e.g. by perturbation theory) after electronic Schrodinger equation ahs been solved..

## 3.2 Self-consistent Field Theory

Electronic S.E. can only be solved exactly for the $H_2^+$ molecule, and similar one-electron system. In the general case we have to rely on approximate (numerical) methods.

Spin: each electron has a spin quantum number of 1/2. In the presence of external magnetic field there are two possible states, corresponding to alignment along ($\alpha$) or opposite ($\beta$) to the field: $\langle\alpha|\alpha\rangle=\langle\beta|\beta\rangle=1;\langle\alpha|\beta\rangle\langle\beta|\alpha\rangle=0$

Variational principle: $E_e=\frac{\langle\Psi|H_e|\Psi\rangle}{\langle\Psi|\Psi\rangle}\geq E_{real}$

Pauli principle: two electrons cannot have all quantum numbers equal $\rightarrow$ antisymmetric wave function

single Slater determinant: neglect electron correlation, or equivalently, the electron-electron repulsion is only included as an average effect.

Hartree-Fock equations: derived from a single determinant trial wave function and variational principle. It is a kind of branching point, either additional approximations for semi-empirical methods, or improved by additional determinants to converge solutions towards exact solutions.

## 3.3 The Energy of a Slater Determinant



## 3.4 Koopmans' Theorem
## 3.5 The Basis Set Approximation
## 3.6 Alternative Formulation of the Variational Problem
## 3.7 Restricted and Unrestricted Hartree-Fock
## 3.8 SCF Techniques
### 3.8.1 SCF Convergence
### 3.8.2 Use of Symmetry
### 3.8.3 Ensuring that the HF Energy is a Minimum
### 3.8.4 Initial Guess Orbitals
### 3.8.5 Direct SCF
### 3.8.6 Linear Scaling Techniques
## <jump id='3.9'>3.9 Semi-Empirical Methods</jump>
### 3.9.1 Neglect of Diatomic Differential Overlap Approximation (NDDO)
### 3.9.2 Intermediate NEglect of Differential Overlap Approximation (INDO)
### 3.9.3 Complete Neglect of Differential Overlap Approximation (CNDO)
## 3.10 Parameterization
### 3.10.1 Modified Intermediate NEglect of Differential Overlap (MINDO)
### 3.10.2 Modified NDDO Models
### 3.10.3 Modified Neglect of Diatomic Overlap (MNDO)
### 3.10.4 Austin Model 1 (AM1)
### 3.10.5 Modified NEglect of Diatomic Overlap Parametric Method Number 3 (MNDO-PM3)
### 3.10.6 The MNDO/d Method 
### 3.10.7 Semi-Ab Initio Method 1
## 3.11 Performance of Semi-empirical Methods
## 3.12 Extend Huckel Theory
### 3.12.1 Sample Huckel Theory
## 3.13 Limitations and Advantages of Semi-empirical Methods References

## <jump id='chp8'>8</jump>

## <jump id='9.2'>9.2</jump>

# <jump id='ts'>12</jump>