# please enter latest results at the TOP of this file.

# [r267](https://code.google.com/p/cudpp/source/detail?r=267) -all -iterations=1 #
cudpp\_testrig and cudpp\_hash\_testrig pass on Windows 7 / CUDA 4.0 / GTX 480 and Quadro FX 4800

cudpp\_testrig and cudpp\_hash\_testrig pass on CentOS Linux x64 / CUDA 4.0 / Tesla C2050

cudpp\_testrig passes all except cudppRand on Mac OS 10.6.8 / CUDA 4.0 / Quadro FX 4800

cudpp\_testrig passes on Dirac/Fermi (Linux x64, C2050) (JDO)

cudpp\_hash\_testrig passes on Dirac/Fermi (Linux x64, C2050) (JDO)

# [r265](https://code.google.com/p/cudpp/source/detail?r=265), -all -iterations=1 #
cudpp\_testrig passes on OS X Lion / CUDA 4.0 / GT330M (JDO)

# [r257](https://code.google.com/p/cudpp/source/detail?r=257), -all -iterations=1 #
cudpp\_testrig passes on Dirac/Fermi (Linux x64, C2050) (JDO)

cudpp\_hash\_testrig passes on Dirac/Fermi (Linux x64, C2050) (JDO)

cudpp\_testrig fails on the last two tridiag tests (but passes everything else) on Dirac/Tesla (Linux x64, C1060) (JDO)

# [r256](https://code.google.com/p/cudpp/source/detail?r=256), -all -iterations=1 #
cudpp\_testrig passes on Win7 x64, GeForce GTX 480.

# [r243](https://code.google.com/p/cudpp/source/detail?r=243), -all -iterations=1 #
cudpp\_testrig passes on CentOS Linux x64, M2070, but cudpp\_hash\_testrig doesn't run.

[mharris@compute-0-4 bin]$ uname -a
Linux compute-0-4.local 2.6.18-128.1.14.el5 #1 SMP Wed Jun 17 06:38:05 EDT 2009 x86\_64 x86\_64 x86\_64 GNU/Linux

[mharris@compute-0-4 bin]$ nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2011 NVIDIA Corporation
Built on Thu\_May\_12\_11:09:45\_PDT\_2011
Cuda compilation tools, release 4.0, V0.2.1221

[mharris@compute-0-4 bin]$ gcc --version
gcc (GCC) 4.1.2 20080704 (Red Hat 4.1.2-44)

# [r235](https://code.google.com/p/cudpp/source/detail?r=235), -all -iterations=1 #
Passes on Dirac/Fermi and Dirac/Tesla (JDO, Mon Jul 25)

Passes on MacBook Pro "nanaimo-bar" / OS X Lion / GF220 (JDO, Mon Jul 25)
```
Darwin nanaimo-bar.local 11.0.0 Darwin Kernel Version 11.0.0: Sat Jun 18 12:56:35 PDT 2011; root:xnu-1699.22.73~1/RELEASE_X86_64 x86_64
i686-apple-darwin11-llvm-gcc-4.2 (GCC) 4.2.1 (Based on Apple Inc. build 5658) (LLVM build 2335.15.00)
Cuda compilation tools, release 4.0, V0.2.1221
```

# [r230](https://code.google.com/p/cudpp/source/detail?r=230), -all -iterations=1 #
Passes on Win7 x64 4GB, GTX 480, CUDA 4.0, 275.33 display driver (MJH, Mon Jul 25)

# [r188](https://code.google.com/p/cudpp/source/detail?r=188), -all -iterations=1 #
Passes on Dirac/Tesla (C1060 4 GB) and Dirac/Fermi (C2050 3 GB) (JDO, Thu Jul 14)

# [r181](https://code.google.com/p/cudpp/source/detail?r=181), -all -iterations=1 #
Passes on Dirac/Tesla (C1060 4 GB) and Dirac/Fermi (C2050 3 GB) (JDO, Fri Jul 8)
```
Linux dirac46 2.6.18-194.11.3.el5n-perf #1 SMP Thu Sep 16 15:26:59 PDT 2010 x86_64 x86_64 x86_64 GNU/Linux
gcc (GCC) 4.4.2
Cuda compilation tools, release 4.0, V0.2.1221
Built on Sun_Mar_20_16:45:27_PDT_2011
```