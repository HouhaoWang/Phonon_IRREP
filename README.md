## Phonon_gkdk_data
- We provide the irreducible representation data for all high-symmetry positions (points/lines/planes) of the 230 space groups, suitable for phonon studies, in the `Phonon_gkdk_data folder`. For each space group, the coordinates of the high-symmetry positions adhere to the primitive and conventional basis sets used by default in Phonopy. Subsequently, for each high-symmetry position, we tabulate the operations of its little group (expressed as 3x3 rotation matrices and translation  column vectors in the primitive lattice basis) alongside the characters of all irreducible representations.


## Phonon_irrep_tool

### phonon_irrep.py
A python tool based on Phonopy to generate irreducible representations of phonon eigenvectors at all high-symmetry positions (points/lines/planes) of the 230 space groups.



- Usage: The Python script `phonon_irrep.py` is a standalone tool and can be run without any installation. The script takes a single input file—the `band.yaml` file produced by Phonopy that stores the phonon eigenvectors. To use it, place `phonon_irrep.py` and `band.yaml` in the same directory and run the following command:
    ```python
    python phonon_irrep.py <space group> <high-symmetry position>
    ```
    where `<space group>` denotes the space group to which the material belongs, and `<high-symmetry position>` denotes the high-symmetry position for which the irreducible representation is to be calculated.

### example
we calculate the irreps of phonon eigenvectors at 100 sampled q-points along HSL DT (0, 0, w) in material BaLiP.

Necessary file for genrating `band.yaml`: 

`POSCAR`: The unit cell structure standardized by Phonopy.

`FORCE_CONSTANTS`: The force constants matrix computed by VASP.

`Band.conf`:
```
  DIM = 4 0 0 0 4 0 0 0 3 #Supercell expansion matrix

  FORCE_CONSTANTS=READ #Read the force constants from the FORCE_CONSTANTS file
  
  BAND=0 0 0 0 0 1 #Define the high-symmetry path for the phonon band [from (0, 0, 0) to (0, 0, 1) in the DT (0, 0, w) direction]

  BAND_POINTS=101 #Number of q-points along the band path

  EIGENVECTORS=.TRUE. # Request the output of eigenvectors
```
Execute the following command to generate the `band.yaml file`, which contains the phonon frequencies and eigenvectors.
```bash
phonopy -c POSCAR band.conf
```

Place `phonon_irrep.py` and `band.yaml` in the same directory and run the following command:
```python
python phonon_irrep.py 187 DT
```
The output of irreducible representation information is stored in `out.txt`.
