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
Here we take a POSCAR $NiF_2$ as an example (space group: 136):

   $     Ni F2
   $     1.0
   $             4.7100000381         0.0000000000         0.0000000000
   $             0.0000000000         4.7100000381         0.0000000000
   $             0.0000000000         0.0000000000         3.1180000305
   $        Ni    F
   $         2    4
   $     Direct
   $          0.000000000         0.000000000         0.000000000  
   $          0.500000000         0.500000000         0.500000000  
   $          0.303299993         0.303299993         0.000000000
   $          0.196700007         0.803300023         0.500000000
   $          0.803300023         0.196700007         0.500000000
   $          0.696699977         0.696699977         0.000000000



### 2) add the MAGMOM (Cart. coord.) behind the magnetic atoms in POSCAR
There is no need to write 0 0 0 after a non-magnetic atoms.

   $     Ni F2
   $     1.0
   $             4.7100000381         0.0000000000         0.0000000000
   $             0.0000000000         4.7100000381         0.0000000000
   $             0.0000000000         0.0000000000         3.1180000305
   $        Ni    F
   $         2    4
   $     Direct
   $          0.000000000         0.000000000         0.000000000  -1 0 0
   $          0.500000000         0.500000000         0.500000000   1 0 0
   $          0.303299993         0.303299993         0.000000000
   $          0.196700007         0.803300023         0.500000000
   $          0.803300023         0.196700007         0.500000000
   $          0.696699977         0.696699977         0.000000000



### 3) src_mom2msg/mom2msg > msgout (get the #MSG and POSCAR_msg if needed)
POSCAR_msg: Additional $He$ atoms are generated by unitary(#1) and anti-unitary(#0) operations

   $     SG#B 14   OG( 58. 6. 476)
   $          1.0
   $          4.710000038     0.000000000     0.000000000
   $          0.000000000     4.710000038     0.000000000
   $          0.000000000     0.000000000     3.118000031
   $      Ni  F    He
   $        2   4   8
   $     Direct
   $       0.00000000  0.00000000  0.00000000  # cart -1.00000  0.00000  0.00000
   $       0.50000000  0.50000000  0.50000000  # cart  1.00000  0.00000  0.00000
   $       0.30329999  0.30329999  0.00000000
   $       0.19670001  0.80330002  0.50000000
   $       0.80330002  0.19670001  0.50000000
   $       0.69669998  0.69669998  0.00000000
   $       0.18289798  0.32203075  0.24659575  # 1
   $      -0.18289798 -0.32203075 -0.24659575  # 1
   $       0.31710202  0.82203075  0.25340425  # 1
   $       0.68289798  0.17796925  0.74659575  # 1
   $      -0.18289798 -0.32203075  0.24659575  # 0
   $       0.18289798  0.32203075 -0.24659575  # 0
   $       0.68289798  0.17796925  0.25340425  # 0
   $       0.31710202  0.82203075  0.74659575  # 0



msgout:

   $      pos. mom. (frac):
   $       0.000000  0.000000  0.000000 -0.212314  0.000000  0.000000
   $       0.500000  0.500000  0.500000  0.212314  0.000000  0.000000
   $       0.303300  0.303300  0.000000  0.000000  0.000000  0.000000
   $       0.196700  0.803300  0.500000  0.000000  0.000000  0.000000
   $       0.803300  0.196700  0.500000  0.000000  0.000000  0.000000
   $       0.696700  0.696700  0.000000  0.000000  0.000000  0.000000
   $
   $     #symm 16
   $     #  1   0
   $       1  0  0    0.000000
   $       0  1  0    0.000000
   $       0  0  1    0.000000
   $     #  2   0
   $      -1  0  0    0.000000
   $       0 -1  0    0.000000
   $       0  0 -1    0.000000
   $     #  5   1
   $      -1  0  0    0.000000
   $       0 -1  0    0.000000
   $       0  0  1    0.000000
   $     #  6   1
   $       1  0  0    0.000000
   $       0  1  0    0.000000
   $       0  0 -1    0.000000
   $     #  9   1
   $       1  0  0    0.500000
   $       0 -1  0    0.500000
   $       0  0 -1    0.500000
   $     # 10   1
   $      -1  0  0    0.500000
   $       0  1  0    0.500000
   $       0  0  1    0.500000
   $     # 13   0
   $      -1  0  0    0.500000
   $       0  1  0    0.500000
   $       0  0 -1    0.500000
   $     # 14   0
   $       1  0  0    0.500000
   $       0 -1  0    0.500000
   $       0  0  1    0.500000
   $     #symm_mag,  #symm:  8 16
   $     Magnetic SG type : Type III (translationgleiche)
   $
   $                                 Int.   Sch.    #SG   #symm
   $     Crystalline SG(org.):  P4_2/mnm    D4h^14  136   16
   $     unitary  part (only):    P2_1/c     C2h^5   14    4
   $     unitary +antiunitary:      Pnnm    D2h^12   58    8
   $
   $     Magnetic SG number (OG) :   476
   $      SG#B 14   OG( 58. 6. 476)
   $      !!! POSCAR_msg is created successfully !!!


### 4) pos2msg (obtain this #MSG's all magnetic configurations)
   $     phonopy --symmetry --tolerance 0.01 -c POSCAR_msg
PPOSCAR:
   $     generated by phonopy
   $        1.0 
   $          4.7100000380000004    0.0000000000000000    0.0000000000000000
   $          0.0000000000000000    4.7100000380000004    0.0000000000000000
   $          0.0000000000000000    0.0000000000000000    3.1180000309999998
   $     Ni F He
   $        2    4    8   
   $     Direct
   $       0.0000000000000000  0.0000000000000000  0.0000000000000000
   $       0.5000000000000000  0.5000000000000000  0.5000000000000000
   $       0.3032999900000000  0.3032999900000000  0.0000000000000000
   $       0.1967000100000000  0.8032999900000000  0.5000000000000000
   $       0.8032999900000000  0.1967000100000000  0.5000000000000000
   $       0.6967000100000000  0.6967000100000000  0.0000000000000000
   $       0.1828979800000000  0.3220307500000000  0.2465957500000000
   $       0.8171020200000000  0.6779692500000001  0.7534042500000000
   $       0.3171020200000000  0.8220307499999999  0.2534042500000000
   $       0.6828979800000000  0.1779692500000000  0.7465957500000000
   $       0.8171020200000000  0.6779692500000001  0.2465957500000000
   $       0.1828979800000000  0.3220307500000000  0.7534042500000000
   $       0.6828979800000000  0.1779692500000000  0.2534042500000000
   $       0.3171020200000000  0.8220307499999999  0.7465957500000000

Paste PPOSCAR into the website http://tm.iphy.ac.cn/TopMat_1651msg.html with #SG 58 and #MSG 476.
OUTPUT:

   $     SG#B  14   OG (    58.6.476)   BNS (      58.398)
   $       1.0
   $         0.00000000000000   -4.71000003800000    0.00000000000000
   $         4.71000003800000    0.00000000000000    0.00000000000000
   $         0.00000000000000    4.71000003800000    3.11800003100000
   $        Ni    F   He
   $         2    4    8
   $     Direct
   $         0.00000000000000    0.00000000000000    0.00000000000000
   $         0.00000000000000    0.50000000000000    0.50000000000000
   $         0.69670001000000    0.30329999000000    0.00000000000000
   $         0.69670001000000    0.19670001000000    0.50000000000000
   $         0.30329999000000    0.80329999000000    0.50000000000000
   $         0.30329999000000    0.69670001000000    0.00000000000000
   $         0.90694883000000    0.29892981000000    0.26203882000000
   $         0.09305117000000    0.70107019000000    0.73796118000000
   $         0.38287119000000    0.20107019000000    0.23796118000000
   $         0.61712881000000    0.79892981000000    0.76203882000000
   $         0.61712881000000    0.70107019000000    0.26203882000000
   $         0.38287119000000    0.29892981000000    0.73796118000000
   $         0.09305117000000    0.79892981000000    0.23796118000000
   $         0.90694883000000    0.20107019000000    0.76203882000000
   $
   $     INCAR:
   $     LSORBIT = T
   $     LNONCOLLINEAR = T
   $     SAXIS = 0 0 1
   $     MAGMOM= 3  3  0  3 -3  0 300*0.0
   $
   $     KPOINTS:
   $     MKPOINTS used for magnetic space group
   $       8
   $     rec
   $         0.50000000    0.00000000    0.50000000    1.0    ! A
   $         0.00000000    0.00000000    0.50000000    1.0    ! B
   $         0.50000000    0.50000000    0.00000000    1.0    ! C
   $         0.00000000    0.50000000    0.50000000    1.0    ! D
   $         0.50000000    0.50000000    0.50000000    1.0    ! E
   $         0.00000000    0.00000000    0.00000000    1.0    ! GM
   $         0.50000000    0.00000000    0.00000000    1.0    ! Y
   $         0.00000000    0.50000000    0.00000000    1.0    ! Z

cp OUTPUT POSCAR; do spin-polarized VASP calculations with the given "MAGMOM" setting.
