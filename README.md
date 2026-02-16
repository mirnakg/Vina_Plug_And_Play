# Vina Plug & Play

An interactive Google Colab notebook for molecular docking using **AutoDock Vina**. This tool walks you through the entire docking workflow — from ligand preparation to receptor cleaning to docking and pose extraction — with guided prompts at every step. No scripting required.

## Overview

This notebook provides a streamlined, step-by-step pipeline for protein–ligand docking:

1. **Ligand Preparation** — Generate a ligand `.pdbqt` file from a SMILES string, or upload your own.
2. **Receptor Preparation** — Fetch a protein structure from the PDB (or upload one), clean it (remove water, ligands, etc.), define the binding pocket, and convert to `.pdbqt`.
3. **Docking** — Run AutoDock Vina and view binding energies for all generated poses.
4. **Pose Extraction** — Convert docked poses from `.pdbqt` back to `.pdb` for visualization in tools like PyMOL or ChimeraX.

## Requirements

All dependencies are installed automatically within the notebook:

- [AutoDock Vina](https://github.com/ccsb-scripps/AutoDock-Vina) (`vina`)
- [RDKit](https://www.rdkit.org/) (`rdkit`)
- [Meeko](https://github.com/forlilab/Meeko) (`meeko`)
- [Open Babel](https://openbabel.org/) (`openbabel-wheel`)
- [Gemmi](https://gemmi.readthedocs.io/) (`gemmi`)
- [BioPandas](https://biopandas.github.io/biopandas/) (`biopandas`)

## Usage

1. Open the notebook in **Google Colab**.
2. Run cells sequentially — each step will prompt you for input.
3. Optionally mount Google Drive to read/save files directly.

### Step 1: Ligand Preparation

You have two options:

- **Provide a `.pdbqt` file** — enter a file path or upload directly.
- **Enter a SMILES string** — the notebook generates a 3D conformer with RDKit, optimizes it with MMFF, and converts it to `.pdbqt` via Meeko.

### Step 2: Receptor Preparation

- **Upload a `.pdb` file** or **enter a PDB ID** to download from RCSB.
- The notebook auto-detects hetero residues/ligands and lets you choose which to remove.
- Optionally retain metal ions (Zn, Mg, Fe, Ca, Mn, Cu, Co, Ni).
- Define the binding pocket by:
  - **Ligand-based center** — automatically computed from a co-crystallized ligand's coordinates.
  - **Manual coordinates** — enter `[X, Y, Z]` directly.
- Choose **full receptor** or **pocket-only** mode (keeps residues within a specified radius).
- Convert the cleaned `.pdb` to `.pdbqt` using Open Babel.

### Step 3: Docking

- Runs AutoDock Vina with `exhaustiveness=32` and generates up to 10 poses.
- Outputs a table of binding energies (total, intermolecular, intramolecular) for each pose.

### Step 4: Pose Extraction

- Converts docked `.pdbqt` poses back to `.pdb` using Meeko and RDKit.
- Option to export the best pose only or all poses.

## Example Output

```
Pose   Total    Inter    Intra
------------------------------
1       -7.42    -8.10     0.68
2       -7.15    -7.89     0.74
3       -6.98    -7.55     0.57
...
```

## Notes

- Designed for **Google Colab** (uses `google.colab` for file uploads and Drive mounting).
- For more control over receptor preparation, use **PyMOL** as an alternative.
- Re-run Steps 1–4 to dock additional protein–ligand pairs in the same session.
