# TQC and TopMat in 1651 MSGs
The complete theory of topological quantum chemistry (TQC) in all 1651 magnetic space groups (MSGs).</br>
The series of codes for searching for topological materials (TopMat) in 1651 MSGs.

* Ref: J. Gao, et al. "Magnetic band representations, Fu-Kane-like symmetry indicators, and magnetic topological materials", Phys. Rev. B 106, 035150 (2022). https://doi.org/10.1103/PhysRevB.106.035150  <br>

## A generate workflow for topologicl materials in 1651 magnetic space groups (MSGs) online http://tm.iphy.ac.cn/TopMat_1651msg.html
### 1) prepare the original POSCAR file (without magnetism).

### 2) phonopy --symmetry --tolerance 0.01 -c POSCAR

### 3) pos2msg (converting PPOSCAR to POSCAR_msg and initializing MAGMOM on magnetic atoms)
 
### 4) cp POSCAR_msg POSCAR; do spin-polarized VASP calculations with the given "MAGMOM" setting.

### 5) irvsp -sg sg#B [ -nb $m $n ] > outir (generating tqc.txt/tqc.data when using only maximal HSKPs)

### 6) solve compatibility relations (CR) and calculate symmetry indicators (SI) in 1651 magnetic space groups (using tqc.data).


# mom2msg (The additional tool to generate POSCAR_msg)
To find the #MSG (in OG setting) according to the magnetic configuration.</br>
If you find problems, please contact us. Email: rhzhang@iphy.ac.cn</br>


* how to make:

      $  tar -zxvf src_mom2msg.tar.gz
      $  cd src_mom2msg
      $  make

### 1) prepare the original POSCAR file (without magnetism).
Here we take a POSCAR $Al_4Ni_2O_8$ as an example (space group: 227):

    $       SG 227 -0.125 -0.125 -0.125 :Generated by spacegroup for irvsp!
    $           1.0      
    $            0.0000000000000000     4.0229999999999997     4.0229999999999997
    $            4.0229999999999997     0.0000000000000000     4.0229999999999997
    $            4.0229999999999997     4.0229999999999997     0.0000000000000000
    $        Al  Ni  O    
    $          4   2   8
    $       Direct   
    $         0.4999999499999994  0.4999999499999994  0.4999999499999994
    $        -0.0000000500000006  0.4999999499999994  0.4999999499999994
    $         0.4999999499999994  0.4999999499999994 -0.0000000500000006
    $         0.4999999499999994 -0.0000000500000006  0.4999999499999994
    $        -0.1250000500000006 -0.1250000500000006 -0.1250000500000006 
    $         0.1249999499999994  0.1249999499999994  0.1249999499999994 
    $         0.2549999499999993  0.2549999499999993  0.2549999499999993
    $         0.7349999499999997  0.2549999499999993  0.2549999499999993
    $         0.2549999499999993  0.2549999499999993  0.7349999499999997
    $         0.2549999499999993  0.7349999499999997  0.2549999499999993
    $         0.7449999499999995  0.7449999499999995  0.7449999499999995
    $         0.2649999499999991  0.7449999499999995  0.7449999499999995
    $         0.7449999499999995  0.7449999499999995  0.2649999499999991
    $         0.7449999499999995  0.2649999499999991  0.7449999499999995



### 2) add the MAGMOM (Cart. coord.) behind the magnetic atoms in POSCAR
There is no need to write 0 0 0 after a non-magnetic atoms.

    $       SG 227 -0.125 -0.125 -0.125 :Generated by spacegroup for irvsp!
    $           1.0      
    $            0.0000000000000000     4.0229999999999997     4.0229999999999997
    $            4.0229999999999997     0.0000000000000000     4.0229999999999997
    $            4.0229999999999997     4.0229999999999997     0.0000000000000000
    $        Al  Ni  O    
    $          4   2   8
    $       Direct   
    $         0.4999999499999994  0.4999999499999994  0.4999999499999994
    $        -0.0000000500000006  0.4999999499999994  0.4999999499999994
    $         0.4999999499999994  0.4999999499999994 -0.0000000500000006
    $         0.4999999499999994 -0.0000000500000006  0.4999999499999994
    $        -0.1250000500000006 -0.1250000500000006 -0.1250000500000006 0 0 1
    $         0.1249999499999994  0.1249999499999994  0.1249999499999994 0 0 1
    $         0.2549999499999993  0.2549999499999993  0.2549999499999993
    $         0.7349999499999997  0.2549999499999993  0.2549999499999993
    $         0.2549999499999993  0.2549999499999993  0.7349999499999997
    $         0.2549999499999993  0.7349999499999997  0.2549999499999993
    $         0.7449999499999995  0.7449999499999995  0.7449999499999995
    $         0.2649999499999991  0.7449999499999995  0.7449999499999995
    $         0.7449999499999995  0.7449999499999995  0.2649999499999991
    $         0.7449999499999995  0.2649999499999991  0.7449999499999995


### 3) src_mom2msg/mom2msg > msgout (get the #MSG and POSCAR_msg if needed)
msgout:
    $      pos. mom. (frac):
    $       0.500000  0.500000  0.500000  0.000000  0.000000  0.000000
    $      -0.000000  0.500000  0.500000  0.000000  0.000000  0.000000
    $       0.500000  0.500000 -0.000000  0.000000  0.000000  0.000000
    $       0.500000 -0.000000  0.500000  0.000000  0.000000  0.000000
    $      -0.125000 -0.125000 -0.125000  0.124285  0.124285 -0.124285
    $       0.125000  0.125000  0.125000  0.124285  0.124285 -0.124285
    $       0.255000  0.255000  0.255000  0.000000  0.000000  0.000000
    $       0.735000  0.255000  0.255000  0.000000  0.000000  0.000000
    $       0.255000  0.255000  0.735000  0.000000  0.000000  0.000000
    $       0.255000  0.735000  0.255000  0.000000  0.000000  0.000000
    $       0.745000  0.745000  0.745000  0.000000  0.000000  0.000000
    $       0.265000  0.745000  0.745000  0.000000  0.000000  0.000000
    $       0.745000  0.745000  0.265000  0.000000  0.000000  0.000000
    $       0.745000  0.265000  0.745000  0.000000  0.000000  0.000000
    $
    $     #symm 48
    $     #  1   0
    $       1  0  0    0.000000
    $       0  1  0    0.000000
    $       0  0  1    0.000000
    $     #  2   0
    $       1  1  1    0.500000
    $       0  0 -1    0.000000
    $      -1  0  0    0.000000
    $     #  3   0
    $       0  1  0    0.000000
    $       1  0  0    0.000000
    $      -1 -1 -1    0.500000
    $     #  4   0
    $       0  0 -1    0.000000
    $       1  1  1    0.500000
    $       0 -1  0    0.000000
    $     #  5   1
    $      -1 -1 -1    0.500000
    $       0  0  1    0.000000
    $       0  1  0    0.000000
    $     #  6   1
    $       0 -1  0    0.000000
    $      -1  0  0    0.000000
    $       0  0 -1    0.000000
    $     #  7   1
    $       0  0  1    0.000000
    $      -1 -1 -1    0.500000
    $       1  0  0    0.000000
    $     #  8   1
    $      -1  0  0    0.000000
    $       0 -1  0    0.000000
    $       1  1  1    0.500000
    $     # 25   0
    $      -1  0  0    0.000000
    $       0 -1  0    0.000000
    $       0  0 -1    0.000000
    $     # 26   0
    $      -1 -1 -1    0.500000
    $       0  0  1    0.000000
    $       1  0  0    0.000000
    $     # 27   0
    $       0 -1  0    0.000000
    $      -1  0  0    0.000000
    $       1  1  1    0.500000
    $     # 28   0
    $       0  0  1    0.000000
    $      -1 -1 -1    0.500000
    $       0  1  0    0.000000
    $     # 29   1
    $       1  1  1    0.500000
    $       0  0 -1    0.000000
    $       0 -1  0    0.000000
    $     # 30   1
    $       0  1  0    0.000000
    $       1  0  0    0.000000
    $       0  0  1    0.000000
    $     # 31   1
    $       0  0 -1    0.000000
    $       1  1  1    0.500000
    $      -1  0  0    0.000000
    $     # 32   1
    $       1  0  0    0.000000
    $       0  1  0    0.000000
    $      -1 -1 -1    0.500000
    $     #symm_mag,  #symm: 16 48
    $     Magnetic SG type : Type III (translationgleiche)
    $
    $                                 Int.   Sch.    #SG   #symm
    $     Crystalline SG(org.):     Fd-3m      Oh^7  227   48
    $     unitary  part (only):    I4_1/a     C4h^6   88    8
    $     unitary +antiunitary:  I4_1/amd    D4h^19  141   16
    $
    $     Magnetic SG number (OG) :  1219
    $      SG#B 88   OG(141. 7.1219)
    $      !!! POSCAR_msg is created successfully !!!



### 4) pos2msg (obtain this #MSG's all magnetic configurations)




