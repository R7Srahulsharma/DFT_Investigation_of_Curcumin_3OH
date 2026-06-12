# DFT and TD-DFT Investigation of Curcumin_3OH Using ORCA

## Project Overview

This repository presents a complete quantum chemical investigation of Curcumin_3OH using Density Functional Theory (DFT) and Time-Dependent Density Functional Theory (TD-DFT) calculations performed with ORCA.

The objective of this study was to evaluate the structural stability, electronic properties, frontier molecular orbitals, and optical absorption characteristics of Curcumin_3OH through a reproducible computational workflow.

---

# Author

**Rahul Sharma**

BS-MS Dual Degree in Chemistry
National Institute of Technology Agartala

---

# Software

* ORCA 6.1.1
* Avogadro
* Chemcraft
* OriginPro
* Windows PowerShell

---

# Computational Workflow

## Step 1: Geometry Optimization

The molecular geometry was optimized using the B3LYP functional with Grimme's D3BJ dispersion correction.

### Input

```text
! B3LYP D3BJ def2-SVP Opt TightSCF RIJCOSX

%maxcore 3000

%pal
 nprocs 8
end

* xyz 0 1
Coordinates
*
```

### Run

```powershell
& "C:\ORCA\orca.exe" opt.inp > opt.out
```

### Output

```text
opt.gbw
opt.xyz
opt.out
```

---

## Step 2: Frequency Analysis

Frequency calculations were performed to verify whether the optimized geometry corresponds to a true minimum on the potential energy surface.

### Input

```text
! B3LYP D3BJ def2-SVP FREQ TightSCF RIJCOSX

%maxcore 3000

%pal
 nprocs 8
end

* xyzfile 0 1 opt.xyz
```

### Run

```powershell
& "C:\ORCA\orca.exe" freq2.inp > freq2.out
```

### Verification

```powershell
Select-String -SimpleMatch "imaginary" freq2.out
```

### Result

```text
Total number of imaginary perturbations ... 0
```

The absence of imaginary frequencies confirms that the optimized structure is a genuine local minimum.

---

## Step 3: Single Point Energy Calculation

A higher-level single-point energy calculation was performed on the optimized geometry.

### Input

```text
! B3LYP D3BJ def2-TZVP TightSCF RIJCOSX

%maxcore 4000

%pal
 nprocs 8
end

* xyzfile 0 1 opt.xyz
```

### Run

```powershell
& "C:\ORCA\orca.exe" sp2.inp > sp2.out
```

### Output

```text
sp2.out
sp2.gbw
```

---

## Step 4: HOMO-LUMO Analysis

Frontier molecular orbitals were generated as cube files for visualization.

### Input

```text
! B3LYP D3BJ def2-TZVP TightSCF RIJCOSX

%plots
 dim1 100
 dim2 100
 dim3 100

 MO("homo.cube",108,0)
 MO("lumo.cube",109,0)
end

* xyz 0 1
Coordinates
*
```

### Run

```powershell
& "C:\ORCA\orca.exe" homo_lumo.inp > homo_lumo.out
```

### Output

```text
homo.cube
lumo.cube
```

### Visualization

* Chemcraft
* Avogadro

---

## Step 5: HOMO-LUMO Gap

Extracted orbital energies:

| Orbital | Energy (eV) |
| ------- | ----------- |
| HOMO    | -2.0792     |
| LUMO    | -1.6592     |

Energy Gap:

Eg = 0.4200 eV

This relatively small HOMO-LUMO gap indicates significant electronic delocalization and favorable charge-transfer characteristics.

---

## Step 6: Global Reactivity Descriptors

Using Koopmans' theorem:

IP = -EHOMO

EA = -ELUMO

### Calculated Values

| Descriptor                 | Value      |
| -------------------------- | ---------- |
| Ionization Potential (IP)  | 2.079 eV   |
| Electron Affinity (EA)     | 1.659 eV   |
| Electronegativity (χ)      | 1.869 eV   |
| Chemical Hardness (η)      | 0.210 eV   |
| Softness (S)               | 2.381 eV⁻¹ |
| Electrophilicity Index (ω) | 8.31 eV    |

---

## Step 7: TD-DFT UV-Visible Spectrum

Excited-state calculations were performed using TD-DFT.

### Input

```text
! CAM-B3LYP def2-SVP TightSCF TDDFT

%tddft
 nroots 10
end

* xyzfile 0 1 opt.xyz
```

### Run

```powershell
& "C:\ORCA\orca.exe" tddft_small.inp > tddft_small.out
```

### Key Electronic Transitions

| State | Wavelength (nm) | Oscillator Strength |
| ----- | --------------- | ------------------- |
| S1    | 304.8           | 0.9359              |
| S2    | 289.6           | 0.1877              |
| S3    | 282.7           | 0.0992              |
| S4    | 275.6           | 0.3790              |

### Major Absorption Peak

304.8 nm

Oscillator Strength = 0.9359

The strongest transition corresponds to a π→π* excitation within the conjugated framework of Curcumin_3OH.

---

# Scientific Findings

✓ Optimized molecular geometry obtained

✓ Zero imaginary frequencies observed

✓ HOMO and LUMO orbitals successfully generated

✓ HOMO-LUMO energy gap determined

✓ Global chemical reactivity descriptors calculated

✓ UV-Visible absorption spectrum predicted using TD-DFT

✓ Strong absorption band observed at 304.8 nm

---

# Repository Structure

```text
Curcumin_3OH_DFT_TDDFT_ORCA
│
├── Input_Files
├── Output_Files
├── Cube_Files
├── Figures
├── Results
└── README.md
```

---

# Future Work

* Molecular Electrostatic Potential (MEP) Analysis
* Natural Bond Orbital (NBO) Analysis
* Solvent Phase Calculations
* Excited-State Geometry Optimization
* Protein-Ligand Molecular Dynamics Simulations
* MM-PBSA Binding Free Energy Analysis

---

# Citation

If this repository is useful, please cite ORCA:

Neese, F. Software update: the ORCA program system, version 6.0. WIREs Computational Molecular Science (2025).
