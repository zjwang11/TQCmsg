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
Here we take a POSCAR $Al_4Ni_2O_8$ as an example (space group: 227).

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


### 2) add the MAGMOM (Cart. coord.) behind the magnetic atoms in POSCAR

      $  MPOSCAR for Mn2C4
      $  1.0
      $          0.0000000000        2.4600000381         0.0000000000
      $          0.0000000000       -1.2300000191         2.1304225263
      $          10.0000000000       0.0000000000         0.0000000000
      $      C  Mn  
      $      4   2   
      $  Direct
      $       0.333333343         0.666666687         0.300000000
      $       0.666666627         0.333333313         0.300000000
      $       0.333333343         0.666666687        -0.300000000
      $       0.666666627         0.333333313        -0.300000000
      $       0.333333343         0.666666687         0.000000000   0.0 2.5  4.33016
      $       0.666666627         0.333333313         0.000000000   0.0 2.5  4.33016

### 3) src_mom2msg/mom2msg > msgout (get the #MSG and POSCAR_msg if needed)

### 4) pos2msg (obtain this #MSG's all magnetic configurations)




