# clone repo
```
git clone --depth=1 --single-branch https://gitlab.com/QEF/q-e
cd q-e
git checkout 98901cc0d67dfed37319187ab6ed10387c1b8f43
cd ..
```

# build pw.x and run tests.
```
mkdir build_gnu_mpi
cd build_gnu_mpi
cmake -DCMAKE_C_COMPILER=mpicc -DCMAKE_Fortran_COMPILER=mpif90 -DQE_ENABLE_SCALAPACK=ON ../q-e
make -j32 qe_pw_exe
ctest -j32 -L "system--pw"
ls bin
cd ..
```

# download and run a benchmark case.
```
git clone https://github.com/QEF/benchmarks
cd benchmarks/AUSURF112
OMP_NUM_THREADS=1 mpirun -np 16 ../../build_gnu_mpi/bin/pw.x -inp ausurf.in | tee ausurf.out
```
