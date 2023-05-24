---
search:
  boost: 0.5
---

# EasyBuild release notes {: #release_notes }

The latest version of EasyBuild provides support for building and
installing [**2,995** different software packages](../version-specific/supported-software),
including 39 different (compiler) toolchains.
It contains 248 software-specific easyblocks and 39 generic easyblocks,
alongside 16,628 easyconfig files.

!!! note
    See also the [concise overview of major changes in EasyBuild v4.0][eb4_changes_overview].


## EasyBuild v4.7.1 (20 March 2023) {: #release_notes_eb471 }

bugfix/update release

**framework**

- various enhancements, including:

    - add option to make `sanity_check_paths` arch dependent ([#3845](https://github.com/easybuilders/easybuild-framework/pull/3845))
    - add support for `%(start_dir)s` easyconfig template ([#4073](https://github.com/easybuilders/easybuild-framework/pull/4073))
    - add Ubuntu friendly package naming scheme `EasyBuildDebFriendlyPNS` ([#4115](https://github.com/easybuilders/easybuild-framework/pull/4115))
    - allow to directly import constants from `easybuild.framework.easyconfig.constants` ([#4144](https://github.com/easybuilders/easybuild-framework/pull/4144))
    - accept single source as dict and single checksum in `check_checksums_for` ([#4180](https://github.com/easybuilders/easybuild-framework/pull/4180))
    - add pre/post extension hook that is triggered before/after individual extension installations ([#4193](https://github.com/easybuilders/easybuild-framework/pull/4193))
    - enforce absolute paths as start dir of extensions ([#4196](https://github.com/easybuilders/easybuild-framework/pull/4196))
    - print warning when non-existing `start_dir` is specified for extension ([#4201](https://github.com/easybuilders/easybuild-framework/pull/4201))
    - add support to silence deprecation warning for easyconfigs and toolchains ([#4207](https://github.com/easybuilders/easybuild-framework/pull/4207))
    - skip directories when fixing shebangs ([#4209](https://github.com/easybuilders/easybuild-framework/pull/4209))
    - add support for `modunloadmsg` easyconfig parameter ([#4223](https://github.com/easybuilders/easybuild-framework/pull/4223))

- various bug fixes, including:

    - fix use of `locate` in `check_os_dependency` ([#4166](https://github.com/easybuilders/easybuild-framework/pull/4166))
    - add `VERSION` to `easybuild.easyblocks` namespace in test sandbox ([#4171](https://github.com/easybuilders/easybuild-framework/pull/4171))
    - also apply filter to asyncprocess test subsuite ([#4172](https://github.com/easybuilders/easybuild-framework/pull/4172))
    - don't use deprecated `SafeConfigParser` when running with Python 3.x ([#4173](https://github.com/easybuilders/easybuild-framework/pull/4173))
    - update CI workflows to run `apt-get update` if installation of packages via `apt-get install` failed, likely due to stale apt cache ([#4176](https://github.com/easybuilders/easybuild-framework/pull/4176))
    - fixes for `findPythonDeps` script ([#4179](https://github.com/easybuilders/easybuild-framework/pull/4179))
    - check type of `versionsuffix` value in `det_full_ec_version`, and raise useful error message if it's not a string ([#4184](https://github.com/easybuilders/easybuild-framework/pull/4184))
    - avoid GC3Pie deprecation warning ([#4185](https://github.com/easybuilders/easybuild-framework/pull/4185))
    - correctly restore `sys.path` in tests ([#4186](https://github.com/easybuilders/easybuild-framework/pull/4186))
    - suppress output of `--skip-test-step` test ([#4187](https://github.com/easybuilders/easybuild-framework/pull/4187))
    - fix flaky `test_search_file` due to accidental matches for `.*C++` search pattern ([#4190](https://github.com/easybuilders/easybuild-framework/pull/4190))
    - silence `distutils` deprecation warnings ([#4204](https://github.com/easybuilders/easybuild-framework/pull/4204))
    - improve handling of `start_dir` and add tests for cases where either `ext_dir` or initial `start_dir` or both are unset or `None` ([#4206](https://github.com/easybuilders/easybuild-framework/pull/4206))
    - restore initial environment before processing each easystack item ([#4213](https://github.com/easybuilders/easybuild-framework/pull/4213))
    - make `test_help_long` work on small terminals ([#4218](https://github.com/easybuilders/easybuild-framework/pull/4218))

- other changes:

    - use better test assertions by replacing use of `assertFalse`/`assertTrue` ([#4170](https://github.com/easybuilders/easybuild-framework/pull/4170), [#4205](https://github.com/easybuilders/easybuild-framework/pull/4205))
    - remove Travis CI configuration file ([#4174](https://github.com/easybuilders/easybuild-framework/pull/4174))
    - filter out deprecation warnings for platform.dist in `get_os_version` and `platform.linux_distribution` in `get_os_name` ([#4175](https://github.com/easybuilders/easybuild-framework/pull/4175))
    - only give read permissions in GitHub Actions workflows ([#4182](https://github.com/easybuilders/easybuild-framework/pull/4182))
    - fix website/docs links in `README` ([#4199](https://github.com/easybuilders/easybuild-framework/pull/4199))
    - only print "`default:`" for configuration option of `strlist` type if default is not empty ([#4220](https://github.com/easybuilders/easybuild-framework/pull/4220))

**easyblocks**

- minor enhancements and updates, including:

    - fix TensorFlow easyblock for new versions of Bazel & TensorFlow ([#2854](https://github.com/easybuilders/easybuild-easyblocks/pull/2854))
    - make NAMD easyblock aware of `(pre)testopts` ([#2856](https://github.com/easybuilders/easybuild-easyblocks/pull/2856))
    - update `MesonNinja` easyblock for Meson >=0.64.0 ([#2861](https://github.com/easybuilders/easybuild-easyblocks/pull/2861))
    - update scipy easyblock for scipy >= 1.9.0 to use `meson`/`ninja`  ([#2862](https://github.com/easybuilders/easybuild-easyblocks/pull/2862), [#2903](https://github.com/easybuilders/easybuild-easyblocks/pull/2903))
    - modify logic in QScintilla easyblock to find the PyQt5 `sipdir` in more places ([#2868](https://github.com/easybuilders/easybuild-easyblocks/pull/2868))
    - add `testinstall` custom easyconfig parameter to `PythonPackage` easyblock ([#2872](https://github.com/easybuilders/easybuild-easyblocks/pull/2872))
    - use `-x` option for "`go install`" in `GoPackage` generic easyblock, to print commands as they are executed ([#2878](https://github.com/easybuilders/easybuild-easyblocks/pull/2878))
    - allow disabling pybind11 tests with `runtest = False` ([#2892](https://github.com/easybuilders/easybuild-easyblocks/pull/2892))
    - call parent `post_install_step` in `EasyBuildMeta` easyblock (so `postinstallcmds` are taken into account) ([#2893](https://github.com/easybuilders/easybuild-easyblocks/pull/2893))
    - update and enhance Maple easyblock for recent versions ([#2895](https://github.com/easybuilders/easybuild-easyblocks/pull/2895))
    - relax glob pattern to find Mathematica install script ([#2896](https://github.com/easybuilders/easybuild-easyblocks/pull/2896))
    - implement CUDA support in the ELPA EasyBlock & fix `$CPP` configure issue on newer ELPA versions ([#2898](https://github.com/easybuilders/easybuild-easyblocks/pull/2898))
    - update Trilinos easyblock to allow disabling of building tests and forward deps + support Trilinos v13.x ([#2900](https://github.com/easybuilders/easybuild-easyblocks/pull/2900))
    - enhance Python easyblock to create non-versioned symlink for `python-config` + check for `bin/python` and `bin/python-config` in sanity check ([#2904](https://github.com/easybuilders/easybuild-easyblocks/pull/2904))

- various bug fixes, including:

    - do not use `-g77` option when installing NVHPC 22.9+ ([#2819](https://github.com/easybuilders/easybuild-easyblocks/pull/2819))
    - check that `sanity_check_module_loaded` attribute exists before querying it in `PythonPackage` easyblock ([#2865](https://github.com/easybuilders/easybuild-easyblocks/pull/2865))
    - fix `$JULIA_DEPOT_PATH` in installation of multiple `JuliaPackage` extensions ([#2869](https://github.com/easybuilders/easybuild-easyblocks/pull/2869))
    - fix checking of CUDA/ROCR-Runtime dependencies for Clang to determine default build targets ([#2873](https://github.com/easybuilders/easybuild-easyblocks/pull/2873))
    - show template values of `exts_default_options` in `PythonBundle` ([#2874](https://github.com/easybuilders/easybuild-easyblocks/pull/2874))
    - fix missing initialization of `CMakeMake` in `CMakePythonPackage` ([#2876](https://github.com/easybuilders/easybuild-easyblocks/pull/2876))
    - fix error when failing `pip` version check during `PythonPackage` sanity check ([#2877](https://github.com/easybuilders/easybuild-easyblocks/pull/2877))
    - handle templating correctly in `CMakeMake` when playing with `configopts` ([#2882](https://github.com/easybuilders/easybuild-easyblocks/pull/2882))
    - avoid crash in test step of PyTorch easyblock if `runtest` is not a command ([#2883](https://github.com/easybuilders/easybuild-easyblocks/pull/2883))
    - fix check configure option in FlexiBLAS easyblock ([#2886](https://github.com/easybuilders/easybuild-easyblocks/pull/2886))
    - use older `ncgen -H` for older netCDF ([#2889](https://github.com/easybuilders/easybuild-easyblocks/pull/2889))
    - fix linking numexpr with Intel MKL's VML library for imkl >= 2021.x ([#2897](https://github.com/easybuilders/easybuild-easyblocks/pull/2897))

- other changes:

    - only give read permissions in GitHub Actions workflows ([#2863](https://github.com/easybuilders/easybuild-easyblocks/pull/2863))
    - use start dir of extension to install R packages ([#2867](https://github.com/easybuilders/easybuild-easyblocks/pull/2867))
    - fix website/docs links in `README` ([#2870](https://github.com/easybuilders/easybuild-easyblocks/pull/2870))
    - add deprecation notice to `RPackage` extensions with relative paths in `start_dir` ([#2879](https://github.com/easybuilders/easybuild-easyblocks/pull/2879))

**easyconfigs**

- added example easyconfig files for 99 new software packages:

    - astro-tulips ([#17263](https://github.com/easybuilders/easybuild-easyconfigs/pull/17263)), BA3-SNPS-autotune ([#17248](https://github.com/easybuilders/easybuild-easyconfigs/pull/17248)), BayesAss3-SNPs ([#17247](https://github.com/easybuilders/easybuild-easyconfigs/pull/17247)), Block (#27), CatLearn ([#14940](https://github.com/easybuilders/easybuild-easyconfigs/pull/14940)),
    CDFlib ([#17133](https://github.com/easybuilders/easybuild-easyconfigs/pull/17133)), Cellpose ([#13703](https://github.com/easybuilders/easybuild-easyconfigs/pull/13703)), CheckM-Database ([#17462](https://github.com/easybuilders/easybuild-easyconfigs/pull/17462)), chemprop ([#17261](https://github.com/easybuilders/easybuild-easyconfigs/pull/17261)), cimfomfa ([#17268](https://github.com/easybuilders/easybuild-easyconfigs/pull/17268)), conan ([#17326](https://github.com/easybuilders/easybuild-easyconfigs/pull/17326)),
    cooler ([#17328](https://github.com/easybuilders/easybuild-easyconfigs/pull/17328)), crossguid ([#16207](https://github.com/easybuilders/easybuild-easyconfigs/pull/16207)), cuSPARSELt ([#17141](https://github.com/easybuilders/easybuild-easyconfigs/pull/17141)), cython-blis ([#17544](https://github.com/easybuilders/easybuild-easyconfigs/pull/17544)), DBCSR ([#17170](https://github.com/easybuilders/easybuild-easyconfigs/pull/17170)), dclone ([#17225](https://github.com/easybuilders/easybuild-easyconfigs/pull/17225)),
    DensPart ([#17473](https://github.com/easybuilders/easybuild-easyconfigs/pull/17473)), Deprecated (#1248), DLPack ([#17311](https://github.com/easybuilders/easybuild-easyconfigs/pull/17311)), DMLC-Core ([#17311](https://github.com/easybuilders/easybuild-easyconfigs/pull/17311)), dorado ([#17195](https://github.com/easybuilders/easybuild-easyconfigs/pull/17195)), duplex-tools ([#17497](https://github.com/easybuilders/easybuild-easyconfigs/pull/17497)),
    eQuilibrator ([#16812](https://github.com/easybuilders/easybuild-easyconfigs/pull/16812)), fastai ([#16985](https://github.com/easybuilders/easybuild-easyconfigs/pull/16985)), fastjet ([#17367](https://github.com/easybuilders/easybuild-easyconfigs/pull/17367)), fastjet-contrib ([#17377](https://github.com/easybuilders/easybuild-easyconfigs/pull/17377)), ffnvcodec ([#17271](https://github.com/easybuilders/easybuild-easyconfigs/pull/17271)),
    finder (#1917), flowFDA ([#17495](https://github.com/easybuilders/easybuild-easyconfigs/pull/17495)), gbasis ([#17473](https://github.com/easybuilders/easybuild-easyconfigs/pull/17473)), genomepy ([#17506](https://github.com/easybuilders/easybuild-easyconfigs/pull/17506)), Giotto-Suite ([#17207](https://github.com/easybuilders/easybuild-easyconfigs/pull/17207)), GKeyll ([#16044](https://github.com/easybuilders/easybuild-easyconfigs/pull/16044)),
    GraphDB ([#17280](https://github.com/easybuilders/easybuild-easyconfigs/pull/17280)), graphviz-python ([#17352](https://github.com/easybuilders/easybuild-easyconfigs/pull/17352)), grid ([#17473](https://github.com/easybuilders/easybuild-easyconfigs/pull/17473)), GUSHR ([#16905](https://github.com/easybuilders/easybuild-easyconfigs/pull/16905)), Health-GPS ([#17434](https://github.com/easybuilders/easybuild-easyconfigs/pull/17434)), HepMC3 ([#17341](https://github.com/easybuilders/easybuild-easyconfigs/pull/17341)),
    HiCMatrix ([#17330](https://github.com/easybuilders/easybuild-easyconfigs/pull/17330)), Inferelator ([#17223](https://github.com/easybuilders/easybuild-easyconfigs/pull/17223)), iodata ([#17473](https://github.com/easybuilders/easybuild-easyconfigs/pull/17473)), irodsfs ([#17486](https://github.com/easybuilders/easybuild-easyconfigs/pull/17486)), jupyter-contrib-nbextensions ([#17270](https://github.com/easybuilders/easybuild-easyconfigs/pull/17270)),
    jupyterlab-lmod ([#16563](https://github.com/easybuilders/easybuild-easyconfigs/pull/16563)), jupyterlmod ([#16563](https://github.com/easybuilders/easybuild-easyconfigs/pull/16563)), kb-python ([#17260](https://github.com/easybuilders/easybuild-easyconfigs/pull/17260)), kineto ([#17194](https://github.com/easybuilders/easybuild-easyconfigs/pull/17194)), KMCP ([#17267](https://github.com/easybuilders/easybuild-easyconfigs/pull/17267)),
    krbalancing ([#17325](https://github.com/easybuilders/easybuild-easyconfigs/pull/17325)), Lace (#954), LASSO-Python ([#17510](https://github.com/easybuilders/easybuild-easyconfigs/pull/17510)), libemf ([#16188](https://github.com/easybuilders/easybuild-easyconfigs/pull/16188)), loomR ([#14518](https://github.com/easybuilders/easybuild-easyconfigs/pull/14518)), MAKER ([#17345](https://github.com/easybuilders/easybuild-easyconfigs/pull/17345)),
    methylartist ([#17264](https://github.com/easybuilders/easybuild-easyconfigs/pull/17264)), nanoflann ([#17311](https://github.com/easybuilders/easybuild-easyconfigs/pull/17311)), netMHCII (#9741), NEXUS-CL ([#17350](https://github.com/easybuilders/easybuild-easyconfigs/pull/17350)), nichenetr ([#17524](https://github.com/easybuilders/easybuild-easyconfigs/pull/17524)),
    Parallel-Hashmap ([#17311](https://github.com/easybuilders/easybuild-easyconfigs/pull/17311)), pdsh ([#17139](https://github.com/easybuilders/easybuild-easyconfigs/pull/17139)), Perseus ([#17210](https://github.com/easybuilders/easybuild-easyconfigs/pull/17210)), PfamScan ([#17530](https://github.com/easybuilders/easybuild-easyconfigs/pull/17530)), Phenoflow ([#17495](https://github.com/easybuilders/easybuild-easyconfigs/pull/17495)), PIRATE ([#17275](https://github.com/easybuilders/easybuild-easyconfigs/pull/17275)),
    PLAMS ([#17473](https://github.com/easybuilders/easybuild-easyconfigs/pull/17473)), plot1cell ([#17498](https://github.com/easybuilders/easybuild-easyconfigs/pull/17498)), pybinding ([#17137](https://github.com/easybuilders/easybuild-easyconfigs/pull/17137)), pyperf ([#17063](https://github.com/easybuilders/easybuild-easyconfigs/pull/17063)), pyslim ([#17150](https://github.com/easybuilders/easybuild-easyconfigs/pull/17150)),
    pytest-rerunfailures ([#17295](https://github.com/easybuilders/easybuild-easyconfigs/pull/17295)), pytest-shard ([#17295](https://github.com/easybuilders/easybuild-easyconfigs/pull/17295)), python-louvain ([#17207](https://github.com/easybuilders/easybuild-easyconfigs/pull/17207)), PyTorch-Ignite ([#15491](https://github.com/easybuilders/easybuild-easyconfigs/pull/15491)),
    PyVCF3 ([#17519](https://github.com/easybuilders/easybuild-easyconfigs/pull/17519)), R2jags ([#17226](https://github.com/easybuilders/easybuild-easyconfigs/pull/17226)), rapidcsv ([#16211](https://github.com/easybuilders/easybuild-easyconfigs/pull/16211)), rapidNJ ([#17399](https://github.com/easybuilders/easybuild-easyconfigs/pull/17399)), Rivet ([#17380](https://github.com/easybuilders/easybuild-easyconfigs/pull/17380)), rmarkdown ([#17189](https://github.com/easybuilders/easybuild-easyconfigs/pull/17189)),
    scArches ([#17069](https://github.com/easybuilders/easybuild-easyconfigs/pull/17069)), scHiCExplorer ([#17334](https://github.com/easybuilders/easybuild-easyconfigs/pull/17334)), scib ([#17142](https://github.com/easybuilders/easybuild-easyconfigs/pull/17142)), SeaView ([#17385](https://github.com/easybuilders/easybuild-easyconfigs/pull/17385)), silhouetteRank ([#17207](https://github.com/easybuilders/easybuild-easyconfigs/pull/17207)),
    siscone ([#17342](https://github.com/easybuilders/easybuild-easyconfigs/pull/17342)), smfishHmrf ([#17207](https://github.com/easybuilders/easybuild-easyconfigs/pull/17207)), sparse-neighbors-search ([#17329](https://github.com/easybuilders/easybuild-easyconfigs/pull/17329)), SpatialDE ([#17207](https://github.com/easybuilders/easybuild-easyconfigs/pull/17207)), sradownloader ([#17188](https://github.com/easybuilders/easybuild-easyconfigs/pull/17188)),
    stardist ([#17215](https://github.com/easybuilders/easybuild-easyconfigs/pull/17215)), Strainberry ([#17522](https://github.com/easybuilders/easybuild-easyconfigs/pull/17522)), toil ([#17098](https://github.com/easybuilders/easybuild-easyconfigs/pull/17098)), vConTACT2 ([#17372](https://github.com/easybuilders/easybuild-easyconfigs/pull/17372)), VirSorter2 ([#17371](https://github.com/easybuilders/easybuild-easyconfigs/pull/17371)),
    vitessce-python ([#17472](https://github.com/easybuilders/easybuild-easyconfigs/pull/17472)), vitessceR ([#17525](https://github.com/easybuilders/easybuild-easyconfigs/pull/17525)), YODA ([#17343](https://github.com/easybuilders/easybuild-easyconfigs/pull/17343))

- added additional easyconfigs for various supported software packages, including:

    - AlphaFold 2.3.0, Anaconda3 2022.10, angsd 0.940, archspec 0.2.0, Armadillo 11.4.3, AUGUSTUS 3.5.0, bcbio-gff 0.7.0,
    BCFtools 1.17, beagle-lib 4.0.0, Beast 2.7.3, BeautifulSoup 4.11.1, Biopython 1.81, BLAT 3.7, Blender 3.4.1,
    Blosc2 2.6.1, Boost 1.81.0, Bottleneck 1.3.6, BUSCO 5.4.5, bx-python 0.9.0, CatMAP 20220519, CellRanger 7.1.0,
    Cereal 1.3.2, CFITSIO 4.2.0, CheckM 1.2.2, code-server 4.9.1, configurable-http-proxy 4.5.3, csvkit 1.1.0, 4.8,
    CUDA 12.1.0, cuDNN 8.8.0.121, cwltool 3.1.20221008225030, Cython 0.29.33, DGL 0.9.1, DIAMOND 2.1.0, dill 0.3.6,
    DIRAC 23.0, dm-tree 0.1.8, dRep 3.4.2, eggnog-mapper 2.1.10, elfutils 0.189, ELPA 2022.05.001, epiScanpy 0.4.0,
    FabIO 0.14.0, FastQ_Screen 0.14.0, FFmpeg 5.1.2, FLAC 1.4.2, flatbuffers 23.1.4, FLINT 2.9.0, GDAL 2.4.4,
    GDAL 3.6.2, GDGraph 1.56, GEOS 3.11.1, GMAP-GSNAP 2023-02-17, gmsh 4.11.1, gnuplot 5.4.6, GOATOOLS 1.3.1,
    googletest 1.12.1, GPyTorch 1.9.1, Greenlet 2.0.2, GST-plugins-base 1.22.1, GStreamer 1.22.1, GTDB-Tk 2.1.1,
    h5py 3.8.0, HDBSCAN 0.8.29, HDF5 1.14.0, HiCExplorer 3.7.2, Highway 1.0.3, HTSlib 1.17, hypothesis 6.68.2,
    Hypre 2.27.0, igraph 0.10.3, IGV 2.16.0, IJulia 1.24.0, Imath 3.1.6, imbalanced-learn 0.10.1, imkl 2023.0.0,
    imkl-FFTW 2023.0.0, impi 2021.8.0, intel-compilers 2023.0.0, IRkernel 1.3.2, JAGS 4.3.1, jax 0.4.4, Julia 1.8.5,
    JupyterHub 3.0.0, jupyter-matlab-proxy 0.5.0, jupyter-resource-usage 0.6.3, jupyter-server-proxy 3.2.2,
    Kent_tools 442, leidenalg 0.9.1, LERC 4.0.0, libcerf 2.3, libgit2 1.5.0, libnsl 2.0.0, libsndfile 1.2.0,
    libtirpc 1.3.3, libxslt 1.1.37, Longshot 0.4.5, MAFFT 7.505, Maple 2022.1, MaSuRCA 4.1.0, Mathematica 13.1.0,
    MATIO 1.5.23, MATLAB 2022a + 2022a-r3 + 2022b, matplotlib 3.7.0, MaxQuant 2.2.0.0, MCL 22.282, MDAnalysis 2.4.2,
    Miniconda3 22.11.1, mm-common 1.0.5, MPFR 4.2.0, mpi4py 3.1.4, mpmath 1.2.1, msprime 1.2.0, MultiQC 1.14,
    mygene 3.2.2, nano 7.1, nanomax-analysis-utils 0.4.4, ncbi-vdb 3.0.2, NetLogo 6.2.2 + 6.3.0, nettle 3.8.1,
    networkx 3.0, Nextflow 22.10.6, nlohmann_json 3.11.2, numba 0.56.4, NVHPC 22.9 + 22.11 + 23.1, NVSHMEM 2.8.0,
    OpenMPI 4.1.5, Optuna 3.1.0, ORCA 5.0.4, PAML 4.10.5, panaroo 1.3.2, ParallelIO 2.5.10, parasail 2.6, Pillow 9.4.0,
    PIPITS 3.0, PLINK 2.00a3.7, plotly.py 5.12.0 + 5.13.1, PLUMED 2.8.1, poetry 1.2.2, polymake 4.8, preseq 3.2.0,
    presto 1.0.0-20230113, PROJ 9.1.1, protobuf 3.21.9, psycopg2 2.9.5, pybind11 2.10.3, PyCharm 2022.3.2,
    py-cpuinfo 9.0.0, pyFAI 0.21.3, pyfaidx 0.7.1, pyGenomeTracks 3.8, pygraphviz 1.10, pymca 5.7.6, Pysam 0.20.0,
    PySCF 2.1.1, PyTables 3.8.0, Python 3.11.2, python-parasail 1.3.3, PyZMQ 24.0.1, QCG-PilotJob 0.13.1,
    QIIME2 2022.11, QtPy 2.3.0, QUAST 5.2.0, R 4.2.2, Ray-project 2.2.0, RDKit 2022.09.4, Redis 7.0.8, redis-py 4.5.1,
    ReFrame 4.0.5, RepeatMasker 4.1.4, RepeatModeler 2.0.4, rjags 4-13, RMBlast 2.13.0, ROOT 6.22.08, Salmon 1.9.0,
    SAMtools 1.17, Scalasca 2.6.1, scikit-learn 1.2.1, SciPy-bundle 2023.02, SDL2 2.26.3, SeqKit 2.3.1, silx 1.0.0,
    snakemake 7.22.0, SNAP-HMM 20221022, SpaceRanger 2.0.1, SPAdes 3.15.5, spaln 2.4.13f, Spark 3.3.1,
    SRA-Toolkit 3.0.3, SSW 1.2.4, STAR 2.7.10b, STAR-CCM+ 18.02.008, SVG 2.87, TensorFlow-Datasets 4.8.3,
    Tkinter 3.10.8, tqdm 4.64.1, Trilinos 13.4.1, Trim_Galore 0.6.10, Trinity 2.15.1, TWL-NINJA 0.98-cluster_only,
    Unidecode 1.3.6, vsc-mympirun 5.3.0, VSEARCH 2.22.1, wget 1.21.3, wxWidgets 3.2.2.1, x264 20230226,
    Xerces-C++ 3.2.4, XlsxWriter 3.0.8, xtb 6.5.1, Xvfb 21.1.6

- minor enhancements, including:

    - add additional extensions to R 4.2.1 ([#17043](https://github.com/easybuilders/easybuild-easyconfigs/pull/17043), [#17125](https://github.com/easybuilders/easybuild-easyconfigs/pull/17125), [#17224](https://github.com/easybuilders/easybuild-easyconfigs/pull/17224), [#17493](https://github.com/easybuilders/easybuild-easyconfigs/pull/17493), [#17523](https://github.com/easybuilders/easybuild-easyconfigs/pull/17523))
    - add additional extensions to Bioconductor 3.15 ([#17126](https://github.com/easybuilders/easybuild-easyconfigs/pull/17126), [#17315](https://github.com/easybuilders/easybuild-easyconfigs/pull/17315), [#17494](https://github.com/easybuilders/easybuild-easyconfigs/pull/17494))
    - add sanity check command to OpenMolcas v22.10 ([#17128](https://github.com/easybuilders/easybuild-easyconfigs/pull/17128))
    - add `Set::Object` and `Heap::Fibonacci` extensions to Perl 5.32.1 ([#17151](https://github.com/easybuilders/easybuild-easyconfigs/pull/17151))
    - add additional extensions to Python 3.10.8 (required for scipy test suite) ([#17159](https://github.com/easybuilders/easybuild-easyconfigs/pull/17159))
    - enhance OpenFold 1.0.1 for standalone usage ([#17206](https://github.com/easybuilders/easybuild-easyconfigs/pull/17206))
    - add SDL2 dependency for FFmpeg 5.0.1 to build `ffplay` ([#17213](https://github.com/easybuilders/easybuild-easyconfigs/pull/17213))
    - set `$JULIA_DEPOT_PATH` and `$JULIA_HISTORY` in Julia easyconfigs ([#17216](https://github.com/easybuilders/easybuild-easyconfigs/pull/17216))
    - add `Devel::Size` + `Math::Utils` extension to recent Perl easyconfigs ([#17246](https://github.com/easybuilders/easybuild-easyconfigs/pull/17246), [#17466](https://github.com/easybuilders/easybuild-easyconfigs/pull/17466))
    - combine errors of extension patch check into a single failure ([#17286](https://github.com/easybuilders/easybuild-easyconfigs/pull/17286))
    - add case-insensitive name clash test ([#17303](https://github.com/easybuilders/easybuild-easyconfigs/pull/17303))
    - add ffnvcodec build dependency to all recent FFmpeg easyconfigs ([#17316](https://github.com/easybuilders/easybuild-easyconfigs/pull/17316))
    - use '`import deap.base`' in sanity check for deap extension in `SciPy-bundle` 2022.05 ([#17429](https://github.com/easybuilders/easybuild-easyconfigs/pull/17429))
    - add source URL to cuDNN 8.8 easyconfig ([#17439](https://github.com/easybuilders/easybuild-easyconfigs/pull/17439))
    - add missing zstd dep to Boost ([#17482](https://github.com/easybuilders/easybuild-easyconfigs/pull/17482))

- various bug fixes, including:

    - fix `postinstallcmds` and clarify download instructions for netMHC + netMHCpan 4.0a (#9739, #9740)
    - fix OpenBLAS 0.3.15 patch to correctly set the CPU core type for Tiger Lake ([#15845](https://github.com/easybuilders/easybuild-easyconfigs/pull/15845))
    - add alternative checksum for UCX 1.13.1 after source tarball was changed in-place (without actual code changes) ([#17077](https://github.com/easybuilders/easybuild-easyconfigs/pull/17077))
    - fix build of TensorFlow 2.5+ on `aarch64` ([#17101](https://github.com/easybuilders/easybuild-easyconfigs/pull/17101))
    - explictely download `qe-gipaw` source tarball from `qe-gipaw` GitHub repository in QuantumESPRESSO 7.1 easyconfigs ([#17129](https://github.com/easybuilders/easybuild-easyconfigs/pull/17129))
    - add patch for `GCCcore` 11.1.0 + 11.2.0 to fix AVX2 bug ([#17135](https://github.com/easybuilders/easybuild-easyconfigs/pull/17135))
    - add patch to make ncbi-vdb 3.0.0 compatible with HDF5 1.12.2 ([#17140](https://github.com/easybuilders/easybuild-easyconfigs/pull/17140))
    - fix source URL for p7zip v17.x ([#17144](https://github.com/easybuilders/easybuild-easyconfigs/pull/17144))
    - add patches for Qt5 5.15.5 to fix compilation failures in abseil and breakpad with glibc 2.34 ([#17165](https://github.com/easybuilders/easybuild-easyconfigs/pull/17165))
    - remove dependency on Pillow from scikit-bio v0.5.7 ([#17178](https://github.com/easybuilders/easybuild-easyconfigs/pull/17178))
    - correctly specify path to libfabric installation prefix in PMIx 4.1.0 easyconfig ([#17204](https://github.com/easybuilders/easybuild-easyconfigs/pull/17204))
    - use GCC as toolchain for serial variants of HDF5, since it has a FORTRAN API ([#17221](https://github.com/easybuilders/easybuild-easyconfigs/pull/17221))
    - fix CMake print summary for long hostnames for NECI ([#17230](https://github.com/easybuilders/easybuild-easyconfigs/pull/17230))
    - add missing pmix patch to OpenMPI 4.1.1 easyconfig used in `iomkl/2021a` and `iomkl/2021b` ([#17240](https://github.com/easybuilders/easybuild-easyconfigs/pull/17240))
    - include required `stereo_chemical_props.txt` for OpenFold 1.0.1 ([#17242](https://github.com/easybuilders/easybuild-easyconfigs/pull/17242))
    - add patch for PAPI 7.0.0 to fix compilation error ([#17244](https://github.com/easybuilders/easybuild-easyconfigs/pull/17244))
    - also update `$PERL5LIB` for RepeatMasker v4.1.4 ([#17245](https://github.com/easybuilders/easybuild-easyconfigs/pull/17245))
    - add alternative `source_url` for MariaDB > 10.4 ([#17250](https://github.com/easybuilders/easybuild-easyconfigs/pull/17250))
    - remove use of rysnc in building `Kent_tools` ([#17252](https://github.com/easybuilders/easybuild-easyconfigs/pull/17252))
    - add missing pkgconf build dependency in recent libxslt easyconfigs ([#17254](https://github.com/easybuilders/easybuild-easyconfigs/pull/17254))
    - add psycopg2, PyYAML, and Cartopy dependencies to QGIS 3.28.1 ([#17257](https://github.com/easybuilders/easybuild-easyconfigs/pull/17257))
    - fix `postinstallcmds` in shovill easyconfigs ([#17279](https://github.com/easybuilders/easybuild-easyconfigs/pull/17279))
    - allow multiple easyconfigs with same name if they differ by CUDA version included in `versionsuffix` ([#17289](https://github.com/easybuilders/easybuild-easyconfigs/pull/17289))
    - remove duplicate SlamDunk easyconfig using lowercase name ([#17301](https://github.com/easybuilders/easybuild-easyconfigs/pull/17301))
    - use `https` in homepage + source URL for GenomeThreader 1.7.3 ([#17338](https://github.com/easybuilders/easybuild-easyconfigs/pull/17338))
    - consistently use Check capitailisation ([#17351](https://github.com/easybuilders/easybuild-easyconfigs/pull/17351))
    - add alternative checksum for spatial 7.3-14 extension in R 4.1.x easyconfigs ([#17356](https://github.com/easybuilders/easybuild-easyconfigs/pull/17356))
    - fix homepage + source URL for ELPA (due to switch to new domain) ([#17357](https://github.com/easybuilders/easybuild-easyconfigs/pull/17357))
    - fix homepage in ELPA easyconfigs (due to switch to new domain) ([#17358](https://github.com/easybuilders/easybuild-easyconfigs/pull/17358))
    - rename libpsml for consistency with libPSML ([#17359](https://github.com/easybuilders/easybuild-easyconfigs/pull/17359))
    - replace obsolete `pycrypto` with `pycryptodome` in Python 3.10.x easyconfigs ([#17412](https://github.com/easybuilders/easybuild-easyconfigs/pull/17412))
    - update deap to version 1.3.3 in SciPy-bundle 2022.05 easyconfigs (since deap 1.3.1 is broken) ([#17413](https://github.com/easybuilders/easybuild-easyconfigs/pull/17413))
    - add patch for Qt5 5.12.2 with `GCCcore/11.2.0` to fix template bug ([#17464](https://github.com/easybuilders/easybuild-easyconfigs/pull/17464))
    - replace src include path with installation dir for HDF5 ([#17469](https://github.com/easybuilders/easybuild-easyconfigs/pull/17469), [#17488](https://github.com/easybuilders/easybuild-easyconfigs/pull/17488))
    - disable Python support for OTF2 v2.2, since we're not including Python 2.x as dependency ([#17499](https://github.com/easybuilders/easybuild-easyconfigs/pull/17499))
    - update homepage and source urls of DFT-D3 ([#17528](https://github.com/easybuilders/easybuild-easyconfigs/pull/17528))
    - use `Binary` easyblock for ANIcalculator to prevent RPATH sanity check failures ([#17536](https://github.com/easybuilders/easybuild-easyconfigs/pull/17536))

- other changes:

    - fix invalid escape sequences in easyconfigs by using raw strings (`r"..."`) ([#11149](https://github.com/easybuilders/easybuild-easyconfigs/pull/11149))
    - add exception for ncbi-vdb 3.0.0 dependency variant ([#17131](https://github.com/easybuilders/easybuild-easyconfigs/pull/17131))
    - use proper source tarball instead of cloning GitHub repository for wxWidgets v3.2.1 ([#17167](https://github.com/easybuilders/easybuild-easyconfigs/pull/17167))
    - enable `-fPIC` in GEOS 3.11.1 (required by GDAL) ([#17196](https://github.com/easybuilders/easybuild-easyconfigs/pull/17196))
    - fix website/docs links in `README` ([#17232](https://github.com/easybuilders/easybuild-easyconfigs/pull/17232))
    - remove commented out line and delete unused patch for TALON ([#17298](https://github.com/easybuilders/easybuild-easyconfigs/pull/17298))
    - re-enable disabled tests ([#17304](https://github.com/easybuilders/easybuild-easyconfigs/pull/17304))
    - rename MAGMA to MAGMA-gene-analysis to avoid name collision ([#17345](https://github.com/easybuilders/easybuild-easyconfigs/pull/17345))
    - Archive ARB and blasr patch files ([#17346](https://github.com/easybuilders/easybuild-easyconfigs/pull/17346))
    - Archive BAMM, BamM, and GroopM to avoid BAMM/BamM name collision ([#17348](https://github.com/easybuilders/easybuild-easyconfigs/pull/17348))
    - consistently use NanoFilt capitalisation ([#17349](https://github.com/easybuilders/easybuild-easyconfigs/pull/17349))
    - rename ncl to NEXUS-CL to avoid case-insensitive name clash ([#17350](https://github.com/easybuilders/easybuild-easyconfigs/pull/17350))
    - rename python graphviz to graphviz-python to avoid case-insensitive name clash ([#17352](https://github.com/easybuilders/easybuild-easyconfigs/pull/17352))
    - archive charmm and CHARMM easyconfigs to avoid case-insensitive name clash ([#17364](https://github.com/easybuilders/easybuild-easyconfigs/pull/17364))



## EasyBuild v4.7.0 (January 9th 2023) {: #release_notes_eb470 }

feature release

**framework**

- print deprecation warning with running EasyBuild with Python 2 ([#4136](https://github.com/easybuilders/easybuild-framework/pull/4136))

- various enhancements, including:

    - add support for checksums specified in external `checksums.json` file ([#3749](https://github.com/easybuilders/easybuild-framework/pull/3749))
    - vendor `distutils.version.LooseVersion` as `easybuild.tools.LooseVersion` (since distutils is deprecated in Python 3.10) ([#3794](https://github.com/easybuilders/easybuild-framework/pull/3794), [#4156](https://github.com/easybuilders/easybuild-framework/pull/4156))
    - take into account custom configuration options specified in easystack file ([#4057](https://github.com/easybuilders/easybuild-framework/pull/4057))
    - add support for using `--output-format=md` (MarkDown) ([#4117](https://github.com/easybuilders/easybuild-framework/pull/4117), [#4155](https://github.com/easybuilders/easybuild-framework/pull/4155))
    - add support for `--filter-rpath-sanity-libs` to skip RPATH sanity check for designated libraries ([#4119](https://github.com/easybuilders/easybuild-framework/pull/4119))
    - add sanity_check_load_module method to EasyBlock to provide control over when module is loaded during sanity check step ([#4125](https://github.com/easybuilders/easybuild-framework/pull/4125))
    - add `eb_bash_completion_local.bash` script to `setup.py` ([#4127](https://github.com/easybuilders/easybuild-framework/pull/4127))
    - check whether `nvidia-smi/rocm-smi` command is available before trying to run it in `get_gpu_info` ([#4131](https://github.com/easybuilders/easybuild-framework/pull/4131))
    - add `gfbf` as subtoolchain of foss ([#4143](https://github.com/easybuilders/easybuild-framework/pull/4143))
    - add support for `postinstallmsgs` ([#4145](https://github.com/easybuilders/easybuild-framework/pull/4145))
    - make `iimkl` toolchain aware of `intel-compilers` ([#4146](https://github.com/easybuilders/easybuild-framework/pull/4146))
    - add definition for `nvofbf` toolchain ([#4157](https://github.com/easybuilders/easybuild-framework/pull/4157), [#4163](https://github.com/easybuilders/easybuild-framework/pull/4163))

- various bug fixes, including:

    - also use EasyConfig instances cache in process_easyconfig when `build_specs` is empty dict ([#4107](https://github.com/easybuilders/easybuild-framework/pull/4107))
    - fix build options that should have empty list as default value ([#4108](https://github.com/easybuilders/easybuild-framework/pull/4108))
    - catch easyconfig parsing failure so we can generate and post a test report ([#4109](https://github.com/easybuilders/easybuild-framework/pull/4109))
    - add explicit return when no checksums match those specified in a tuple ([#4112](https://github.com/easybuilders/easybuild-framework/pull/4112))
    - tweak `findPythonDeps.py` script to use canonical package names ([#4118](https://github.com/easybuilders/easybuild-framework/pull/4118))
    - add `-fdefault-double-8` to `r8` toolchain compiler option for GCC (to be consistent with Intel) ([#4121](https://github.com/easybuilders/easybuild-framework/pull/4121))
    - always start with empty list for banned/requires libraries to avoid that corresponding build option is updated in-place ([#4137](https://github.com/easybuilders/easybuild-framework/pull/4137))
    - fix container tests by using EPEL archive URL for downloading Singularity RPM ([#4138](https://github.com/easybuilders/easybuild-framework/pull/4138))
    - use `-march=x86-64 -mtune=generic` instead of `-xSSE2` when using Intel oneAPI compilers ([#4147](https://github.com/easybuilders/easybuild-framework/pull/4147))
    - partially `skip test_det_copy_ec_specs` if no GitHub token is available ([#4149](https://github.com/easybuilders/easybuild-framework/pull/4149))

- other changes:

    - drop support for easystack files using `'software'` top-level key ([#4057](https://github.com/easybuilders/easybuild-framework/pull/4057))
    - also run unit tests with Python 3.11 + add Python 3.11 to classifiers in `setup.py` ([#4092](https://github.com/easybuilders/easybuild-framework/pull/4092), [#4141](https://github.com/easybuilders/easybuild-framework/pull/4141))
    - use new EasyBuild logo in README ([#4123](https://github.com/easybuilders/easybuild-framework/pull/4123))
    - automatically cancel Github Action workflow runs for outdated commits ([#4132](https://github.com/easybuilders/easybuild-framework/pull/4132))
    - auto-enable use of oneAPI C/C++ compilers for intel-compilers >= 2022.2.0 ([#4135](https://github.com/easybuilders/easybuild-framework/pull/4135))
    - trim CI test configurations to avoid hitting GitHub rate limits ([#4148](https://github.com/easybuilders/easybuild-framework/pull/4148))
    - various tweaks to docstrings and help messages to fix problems with auto-generated documentation in MarkDown format ([#4129](https://github.com/easybuilders/easybuild-framework/pull/4129), [#4130](https://github.com/easybuilders/easybuild-framework/pull/4130), [#4154](https://github.com/easybuilders/easybuild-framework/pull/4154), [#4160](https://github.com/easybuilders/easybuild-framework/pull/4160), [#4162](https://github.com/easybuilders/easybuild-framework/pull/4162), [#4168](https://github.com/easybuilders/easybuild-framework/pull/4168))
    - update copyright lines for 2023 ([#4161](https://github.com/easybuilders/easybuild-framework/pull/4161))

**easyblocks**

- add generic easyblocks for installing (bundle of) Julia packages: JuliaPackage ([#2816](https://github.com/easybuilders/easybuild-easyblocks/pull/2816)) and JuliaBundle ([#2830](https://github.com/easybuilders/easybuild-easyblocks/pull/2830))

- minor enhancements and updates, including:

    - enhance TensorFlow easyblock to take into account provided OpenSSL dependency ([#2575](https://github.com/easybuilders/easybuild-easyblocks/pull/2575))
    - add fix_shebang to `install_step` of PythonPackage easyblock so that we can fix shebangs when installing extensions ([#2680](https://github.com/easybuilders/easybuild-easyblocks/pull/2680))
    - update PETSc easyblock for newer versions (>= 3.17) ([#2796](https://github.com/easybuilders/easybuild-easyblocks/pull/2796))
    - update Clang easyblock to add support for new directory structure in Clang versions >= 14 + support Flang ([#2800](https://github.com/easybuilders/easybuild-easyblocks/pull/2800))
    - update Xmipp easyblock since versions >= 3.20.07 use `noAsk` option to configure ([#2809](https://github.com/easybuilders/easybuild-easyblocks/pull/2809))
    - add `include/opencv4` to `$CPATH` for OpenCV versions >= 4.0 ([#2818](https://github.com/easybuilders/easybuild-easyblocks/pull/2818))
    - add extra option for disabling LAPACK in ESMF ([#2821](https://github.com/easybuilders/easybuild-easyblocks/pull/2821))
    - enable building of static libraries for libxml2 >= 2.10 ([#2825](https://github.com/easybuilders/easybuild-easyblocks/pull/2825))
    - update Xmipp easyblock to handle effects of CUDA at SYSTEM level and newer CUDA version requirements for stdc++ ([#2831](https://github.com/easybuilders/easybuild-easyblocks/pull/2831))
    - update LLVM easyblock to put `'cmake'` symlink in place so separate CMake modules required for LLVM 15+ can be found ([#2832](https://github.com/easybuilders/easybuild-easyblocks/pull/2832))
    - set `$TEMPDIRPATH` for testsuite in the BerkeleyGW easyblock, to avoid polluting `/tmp` ([#2836](https://github.com/easybuilders/easybuild-easyblocks/pull/2836))
    - add `configure_no_prefix` option to skip addition of prefix to configure command in ConfigureMake easyblock ([#2842](https://github.com/easybuilders/easybuild-easyblocks/pull/2842))
    - update `qscintilla.py` to be compatible with EB install of PyQt5 >= 5.15 ([#2845](https://github.com/easybuilders/easybuild-easyblocks/pull/2845))
    - add UCC to known_dependencies in OpenMPI EasyBlock ([#2847](https://github.com/easybuilders/easybuild-easyblocks/pull/2847))
    - update Clang-AOMP easyblock to handle version 5.2 and newer ([#2851](https://github.com/easybuilders/easybuild-easyblocks/pull/2851))

- various bug fixes, including:

    - fix installing of Clang with RPATH linking ([#2799](https://github.com/easybuilders/easybuild-easyblocks/pull/2799))
    - fix `--module-only` for Clang + fix sanity check for Clang 11.x ([#2800](https://github.com/easybuilders/easybuild-easyblocks/pull/2800))
    - create `$XDG_CACHE_HOME` for PyTorch tests ([#2806](https://github.com/easybuilders/easybuild-easyblocks/pull/2806))
    - make PythonPackage easyblock compatible with `--sanity-check-only` by loading module early during sanity check step ([#2828](https://github.com/easybuilders/easybuild-easyblocks/pull/2828))
    - fix docstring of PythonBundle generic easyblock ([#2833](https://github.com/easybuilders/easybuild-easyblocks/pull/2833))
    - fix counting of failures in PyTorch tests ([#2834](https://github.com/easybuilders/easybuild-easyblocks/pull/2834), [#2840](https://github.com/easybuilders/easybuild-easyblocks/pull/2840))
    - make sure that ANSYS INSTALL script has execute permissions ([#2852](https://github.com/easybuilders/easybuild-easyblocks/pull/2852), [#2853](https://github.com/easybuilders/easybuild-easyblocks/pull/2853))

- other changes:

    - remove useless `-openmp` build option for MRtrix v3.x ([#2822](https://github.com/easybuilders/easybuild-easyblocks/pull/2822))
    - update HDF5 easyblock to use `--enable-threadsafe` configure option to make C API thread safe ([#2824](https://github.com/easybuilders/easybuild-easyblocks/pull/2824))
    - use new EasyBuild logo in README ([#2827](https://github.com/easybuilders/easybuild-easyblocks/pull/2827))
    - automatically cancel Github Action workflow runs for outdated commits ([#2835](https://github.com/easybuilders/easybuild-easyblocks/pull/2835))
    - use fixed names for `bazel/wrapper` subdirectories used when building TensorFlow, to make debugging easier ([#2841](https://github.com/easybuilders/easybuild-easyblocks/pull/2841))
    - also run unit tests with Python 3.11 ([#2844](https://github.com/easybuilders/easybuild-easyblocks/pull/2844))
    - tweak docstring in some generic easyblocks so it renders nicely in auto-generated documentation ([#2849](https://github.com/easybuilders/easybuild-easyblocks/pull/2849))
    - update copyright lines for 2023 ([#2850](https://github.com/easybuilders/easybuild-easyblocks/pull/2850))

**easyconfigs**

- added easyconfigs for `foss/2022b`, `intel/2022b` common toolchains ([#16961](https://github.com/easybuilders/easybuild-easyconfigs/pull/16961) and [#16962](https://github.com/easybuilders/easybuild-easyconfigs/pull/16962))

    - see also <https://docs.easybuild.io/en/latest/Common-toolchains.html>

- added easyconfigs for NVHPC-based toolchains `nvompi/2022.07` and `nvofbf/2022.07` ([#16724](https://github.com/easybuilders/easybuild-easyconfigs/pull/16724))

- added example easyconfig files for 107 new software packages:

    - Alfred ([#16780](https://github.com/easybuilders/easybuild-easyconfigs/pull/16780)), attrdict3 ([#16856](https://github.com/easybuilders/easybuild-easyconfigs/pull/16856)), bamFilters ([#16735](https://github.com/easybuilders/easybuild-easyconfigs/pull/16735)), bcl-convert ([#16351](https://github.com/easybuilders/easybuild-easyconfigs/pull/16351)), Beagle ([#346](https://github.com/easybuilders/easybuild-easyconfigs/pull/346)), Boost.MPI ([#15757](https://github.com/easybuilders/easybuild-easyconfigs/pull/15757)),
    captum ([#16477](https://github.com/easybuilders/easybuild-easyconfigs/pull/16477)), CAT-BAT ([#16577](https://github.com/easybuilders/easybuild-easyconfigs/pull/16577), [#16634](https://github.com/easybuilders/easybuild-easyconfigs/pull/16634)), cdo-bindings ([#16669](https://github.com/easybuilders/easybuild-easyconfigs/pull/16669)), Chemaxon-Marvin ([#13954](https://github.com/easybuilders/easybuild-easyconfigs/pull/13954)), CliMetLab ([#16842](https://github.com/easybuilders/easybuild-easyconfigs/pull/16842)),
    CloudCompare ([#16944](https://github.com/easybuilders/easybuild-easyconfigs/pull/16944)), cmocean ([#16659](https://github.com/easybuilders/easybuild-easyconfigs/pull/16659)), COBRApy ([#16616](https://github.com/easybuilders/easybuild-easyconfigs/pull/16616)), CodAn ([#16902](https://github.com/easybuilders/easybuild-easyconfigs/pull/16902)), CoSymLib ([#17049](https://github.com/easybuilders/easybuild-easyconfigs/pull/17049)), CPPE ([#16749](https://github.com/easybuilders/easybuild-easyconfigs/pull/16749)),
    cryoCARE ([#16534](https://github.com/easybuilders/easybuild-easyconfigs/pull/16534)), CTPL ([#16498](https://github.com/easybuilders/easybuild-easyconfigs/pull/16498)), CUDA-Samples ([#16914](https://github.com/easybuilders/easybuild-easyconfigs/pull/16914)), cwltool ([#16503](https://github.com/easybuilders/easybuild-easyconfigs/pull/16503)), Cytoscape ([#16682](https://github.com/easybuilders/easybuild-easyconfigs/pull/16682)), DeepLabCut ([#16391](https://github.com/easybuilders/easybuild-easyconfigs/pull/16391)),
    DeepMod2 ([#17008](https://github.com/easybuilders/easybuild-easyconfigs/pull/17008)), Dice ([#16752](https://github.com/easybuilders/easybuild-easyconfigs/pull/16752)), dlb ([#16845](https://github.com/easybuilders/easybuild-easyconfigs/pull/16845)), DRAGMAP ([#16532](https://github.com/easybuilders/easybuild-easyconfigs/pull/16532)), ecBuild ([#16842](https://github.com/easybuilders/easybuild-easyconfigs/pull/16842)), EGTtools ([#16704](https://github.com/easybuilders/easybuild-easyconfigs/pull/16704)),
    ESM-2 ([#16528](https://github.com/easybuilders/easybuild-easyconfigs/pull/16528)), flair-NLP ([#15588](https://github.com/easybuilders/easybuild-easyconfigs/pull/15588)), FMS ([#16965](https://github.com/easybuilders/easybuild-easyconfigs/pull/16965)), Godon ([#16574](https://github.com/easybuilders/easybuild-easyconfigs/pull/16574)), gsw ([#16643](https://github.com/easybuilders/easybuild-easyconfigs/pull/16643)), HighFive ([#16737](https://github.com/easybuilders/easybuild-easyconfigs/pull/16737)), humann ([#16853](https://github.com/easybuilders/easybuild-easyconfigs/pull/16853)),
    HyperQueue ([#16753](https://github.com/easybuilders/easybuild-easyconfigs/pull/16753)), IJulia ([#16494](https://github.com/easybuilders/easybuild-easyconfigs/pull/16494), [#16665](https://github.com/easybuilders/easybuild-easyconfigs/pull/16665)), infercnvpy ([#16712](https://github.com/easybuilders/easybuild-easyconfigs/pull/16712)), InParanoid ([#16572](https://github.com/easybuilders/easybuild-easyconfigs/pull/16572)), jupyter-server ([#14844](https://github.com/easybuilders/easybuild-easyconfigs/pull/14844)),
    KaHIP ([#16861](https://github.com/easybuilders/easybuild-easyconfigs/pull/16861)), KITE ([#16550](https://github.com/easybuilders/easybuild-easyconfigs/pull/16550)), lagrangian-filtering ([#16654](https://github.com/easybuilders/easybuild-easyconfigs/pull/16654)), LHAPDF ([#17028](https://github.com/easybuilders/easybuild-easyconfigs/pull/17028)), librttopo ([#16856](https://github.com/easybuilders/easybuild-easyconfigs/pull/16856)), libwpe ([#16088](https://github.com/easybuilders/easybuild-easyconfigs/pull/16088)),
    Magics ([#16842](https://github.com/easybuilders/easybuild-easyconfigs/pull/16842)), matlab-proxy ([#14270](https://github.com/easybuilders/easybuild-easyconfigs/pull/14270)), mcu ([#16566](https://github.com/easybuilders/easybuild-easyconfigs/pull/16566)), MEMOTE ([#16772](https://github.com/easybuilders/easybuild-easyconfigs/pull/16772)), memtester ([#16763](https://github.com/easybuilders/easybuild-easyconfigs/pull/16763)), meson-python ([#16911](https://github.com/easybuilders/easybuild-easyconfigs/pull/16911)),
    minizip ([#16856](https://github.com/easybuilders/easybuild-easyconfigs/pull/16856)), MITgcmutils ([#16623](https://github.com/easybuilders/easybuild-easyconfigs/pull/16623)), MONAI ([#16519](https://github.com/easybuilders/easybuild-easyconfigs/pull/16519)), MOOSE ([#13824](https://github.com/easybuilders/easybuild-easyconfigs/pull/13824)), mstore ([#16892](https://github.com/easybuilders/easybuild-easyconfigs/pull/16892), [#17029](https://github.com/easybuilders/easybuild-easyconfigs/pull/17029)),
    MultilevelEstimators ([#15630](https://github.com/easybuilders/easybuild-easyconfigs/pull/15630), [#16665](https://github.com/easybuilders/easybuild-easyconfigs/pull/16665)), n2v ([#16535](https://github.com/easybuilders/easybuild-easyconfigs/pull/16535)), NanoLyse ([#16575](https://github.com/easybuilders/easybuild-easyconfigs/pull/16575)), napari ([#16468](https://github.com/easybuilders/easybuild-easyconfigs/pull/16468)), NECI ([#16751](https://github.com/easybuilders/easybuild-easyconfigs/pull/16751)),
    nf-core-mag ([#16613](https://github.com/easybuilders/easybuild-easyconfigs/pull/16613)), oceanspy ([#16640](https://github.com/easybuilders/easybuild-easyconfigs/pull/16640)), olego ([#16909](https://github.com/easybuilders/easybuild-easyconfigs/pull/16909)), OmegaFold ([#16698](https://github.com/easybuilders/easybuild-easyconfigs/pull/16698)), OVITO ([#16811](https://github.com/easybuilders/easybuild-easyconfigs/pull/16811)), Panedr ([#16564](https://github.com/easybuilders/easybuild-easyconfigs/pull/16564)),
    Parcels ([#16838](https://github.com/easybuilders/easybuild-easyconfigs/pull/16838)), polars ([#16989](https://github.com/easybuilders/easybuild-easyconfigs/pull/16989)), PsiCLASS ([#16906](https://github.com/easybuilders/easybuild-easyconfigs/pull/16906)), pyccel ([#16823](https://github.com/easybuilders/easybuild-easyconfigs/pull/16823)), PyCheMPS2 ([#16710](https://github.com/easybuilders/easybuild-easyconfigs/pull/16710)), PyDamage ([#16576](https://github.com/easybuilders/easybuild-easyconfigs/pull/16576)),
    PyImageJ ([#16757](https://github.com/easybuilders/easybuild-easyconfigs/pull/16757)), pysteps ([#16783](https://github.com/easybuilders/easybuild-easyconfigs/pull/16783)), python-libsbml ([#16610](https://github.com/easybuilders/easybuild-easyconfigs/pull/16610)), python-telegram-bot ([#16442](https://github.com/easybuilders/easybuild-easyconfigs/pull/16442)), pyWannier90 ([#16447](https://github.com/easybuilders/easybuild-easyconfigs/pull/16447)),
    resolos ([#16649](https://github.com/easybuilders/easybuild-easyconfigs/pull/16649)), RLCard ([#16695](https://github.com/easybuilders/easybuild-easyconfigs/pull/16695)), SAP ([#5200](https://github.com/easybuilders/easybuild-easyconfigs/pull/5200)), scikit-misc ([#16457](https://github.com/easybuilders/easybuild-easyconfigs/pull/16457)), scvi-tools ([#16457](https://github.com/easybuilders/easybuild-easyconfigs/pull/16457)), SELFIES ([#17032](https://github.com/easybuilders/easybuild-easyconfigs/pull/17032)),
    SeuratDisk ([#16951](https://github.com/easybuilders/easybuild-easyconfigs/pull/16951)), sfftk ([#16466](https://github.com/easybuilders/easybuild-easyconfigs/pull/16466)), simint ([#16886](https://github.com/easybuilders/easybuild-easyconfigs/pull/16886)), SISSO++ ([#15759](https://github.com/easybuilders/easybuild-easyconfigs/pull/15759)), slamdunk ([#15197](https://github.com/easybuilders/easybuild-easyconfigs/pull/15197)), spaCy ([#17027](https://github.com/easybuilders/easybuild-easyconfigs/pull/17027)),
    Sphinx-RTD-Theme ([#16736](https://github.com/easybuilders/easybuild-easyconfigs/pull/16736)), SPOOLES ([#16756](https://github.com/easybuilders/easybuild-easyconfigs/pull/16756)), Squidpy ([#16880](https://github.com/easybuilders/easybuild-easyconfigs/pull/16880)), svist4get ([#16505](https://github.com/easybuilders/easybuild-easyconfigs/pull/16505)), task-spooler ([#17048](https://github.com/easybuilders/easybuild-easyconfigs/pull/17048)),
    TBA ([#16497](https://github.com/easybuilders/easybuild-easyconfigs/pull/16497)), TensorFlow-Datasets ([#16421](https://github.com/easybuilders/easybuild-easyconfigs/pull/16421)), TFEA ([#16476](https://github.com/easybuilders/easybuild-easyconfigs/pull/16476)), TinyXML ([#16992](https://github.com/easybuilders/easybuild-easyconfigs/pull/16992)), tokenizers ([#15587](https://github.com/easybuilders/easybuild-easyconfigs/pull/15587)),
    torchsampler ([#16464](https://github.com/easybuilders/easybuild-easyconfigs/pull/16464)), trimesh ([#16858](https://github.com/easybuilders/easybuild-easyconfigs/pull/16858)), UCX-ROCm ([#17033](https://github.com/easybuilders/easybuild-easyconfigs/pull/17033)), wpebackend-fdo ([#16093](https://github.com/easybuilders/easybuild-easyconfigs/pull/16093)), xmitgcm ([#16637](https://github.com/easybuilders/easybuild-easyconfigs/pull/16637))

- added additional easyconfigs for various supported software packages, including:

    - Albumentations 1.3.0, ANSYS 2022R2, AOCC 4.0.0, archspec 0.1.4, ArviZ 0.12.1, ASAP 2.1, astropy 5.1.1,
    basemap 1.3.6, BBMap 39.01, BEDOPS 2.4.41, Blender 3.3.1, Blosc 1.21.3, Blosc2 2.4.3, bokeh 2.4.3, Bonnie++ 2.00a,
    boto3 1.26.37, BRAKER 2.1.6, CDO 2.1.1, cdsapi 0.5.1, CharLS 2.4.1, CheMPS2 1.8.12, CMake 3.24.3, CubeGUI 4.8,
    CubeLib 4.8, CubeWriter 4.8, CUDA 11.8.0 + 12.0.0, cuDNN 8.6.0.163 + 8.7.0.84, cURL 7.86.0, cutadapt 4.2,
    cuTENSOR 1.6.1.5, dask 2022.10.0, DAS_Tool 1.1.3, DBus 1.15.2, dcm2niix 1.0.20220720, DCMTK 3.6.7, deepdiff 5.8.1,
    dm-reverb 0.7.0, double-conversion 3.2.1, Doxygen 1.9.5, ecCodes 2.27.0, exiv2 0.27.5, Fiji 2.9.0, Filtlong 0.2.1,
    FLANN 1.9.1, FlexiBLAS 3.2.1, fontconfig 2.14.1, FreeXL 1.0.6, g2clib 1.7.0, GATK 4.3.0.0, GD 2.75, GDCM 3.0.20,
    Gdk-Pixbuf 2.42.10, GeneMark-ET 4.71, gensim 4.2.0, geopandas 0.12.2, gettext 0.21.1, gh 2.20.2, Ghostscript 10.0.0,
    git 2.38.1, GLib 2.75.0, GlobalArrays 5.8.2, GnuTLS 3.7.8, GObject-Introspection 1.74.0, GRASS 8.2.0, GTK3 3.24.35,
    HarfBuzz 5.3.1, HTSeq 2.0.2, hwloc 2.8.0, Hyperopt 0.2.7, ICU 72.1, imagecodecs 2022.9.26, imageio 2.22.2,
    ImageMagick 7.1.0-53, imbalanced-learn 0.9.0, JasPer 4.0.0, jax 0.3.23, JupyterLab 3.5.0, Leptonica 1.83.0,
    libavif 0.11.1, libdap 3.20.11, libdeflate 1.15, libdrm 2.4.114, libfabric 1.16.1, libffi 3.4.4, libglvnd 1.6.0,
    libgpg-error 1.46, libidn 1.41, libjpeg-turbo 2.1.4, LibLZF 3.6, libpciaccess 0.17, libpng 1.6.38, librsvg 2.55.1,
    LibSoup 3.0.8, libspatialindex 1.9.3, libspatialite 5.0.1, libtasn1 4.19.0, LibTIFF 4.4.0, libxml2 2.10.3,
    libxml2-python 2.9.13, line_profiler 4.0.0, LittleCMS 2.14, LLVM 15.0.5, lz4 1.9.4, makedepend 1.0.7, Mako 1.2.4,
    MATLAB-Engine 2021b, Mesa 22.2.4, Meson 0.64.0, MIGRATE-N 5.0.4, Miniconda3 4.12.0, mold 1.7.1, Molden 7.1,
    MotionCor2 1.5.0, MoviePy 1.0.3, MRChem 1.1.1, MRCPP 1.4.1, nano 7.0, NanoFilt 2.8.0, nanoget 1.18.1,
    nanomath 1.2.1, ncbi-vdb 3.0.0, NCCL 2.16.2, NCCL-tests 2.13.6, NCO 5.1.3, nglview 3.0.3, NiBabel 4.0.2,
    Ninja 1.11.1, nodejs 18.12.1, NSPR 4.35, NSS 3.85, NVHPC 22.7, NVSHMEM 2.7.0, Octave 7.1.0, OPARI2 2.0.7,
    OpenFOAM 10, OpenFold 1.0.1, OpenImageIO 2.3.17.0, OpenMolcas 22.10, openpyxl 3.0.10, openslide-python 1.2.0,
    OpenStackClient 6.0.0, OSU-Micro-Benchmarks 6.2, OTF2 3.0.2, Pango 1.50.12, PAPI 7.0.0, pauvre 0.2.3, PETSc 3.17.4,
    phonopy 2.16.3, pigz 2.7, Pillow 9.2.0, Pint 0.19.2, pixman 0.42.2, PMIx 4.2.2, poppler 22.12.0, psutil 5.9.3,
    pybedtools 0.9.0, PyBerny 0.6.3, pydantic 1.10.2, pydicom 2.3.0, pyproj 3.4.0, PyQt5 5.15.5, pytest 7.1.3,
    Python 3.10.8, python-isal 1.1.0, PyTorch 1.12.1, PyTorch-Geometric 2.1.0, PyTorch-Lightning 1.8.4, QCA 2.3.5,
    QGIS 3.28.1, QIIME2 2022.8, QScintilla 2.11.6, Qt5 5.15.7, Qtconsole 5.3.2, QtKeychain 0.13.2, QtPy 2.2.1,
    rasterio 1.3.4, re2c 3.0, ReFrame 3.12.0, RStudio-Server 2022.07.2+576, Ruby 3.0.5, Rust 1.65.0, SAP 1.1.3,
    scanpy 1.9.1, scikit-image 0.19.3, SCons 4.4.0, Score-P 8.0, Seaborn 0.12.1, SentencePiece 0.1.97, Seurat 4.3.0,
    SignalP 6.0g, SimPEG 0.18.1, SLEPc 3.17.2, SNAP 2.0.1, SpaceRanger 2.0.0, SQLite 3.39.4, STAR-CCM+ 17.06.007,
    SuperLU_DIST 8.1.0, tensorboardX 2.5.1, TensorFlow 2.8.4, tensorflow-probability 0.16.0, tesseract 5.3.0,
    texinfo 6.8, TM-align 20190822, tmux 3.3a, TOBIAS 0.14.0, TOML-Fortran 0.3.1, Transformers 4.24.0,
    typing-extensions 4.4.0, UCC 1.1.0, UCX-CUDA 1.13.1, util-linux 2.38.1, Valgrind 3.20.0, Vim 9.0.0950, VTK 9.2.2,
    wandb 0.13.6, WebKitGTK+ 2.37.1, WPS 4.4, WRF 4.4, wxPython 4.2.0, wxWidgets 3.2.0, X11 20221110, xarray 2022.9.0,
    XCFun 2.1.1, XGBoost 1.7.2, Xmipp 3.22.07, XZ 5.2.7, yaml-cpp 0.7.0, zarr 2.13.3, zlib-ng 2.0.6

- minor enhancements, including:

    - enable building of dev tools in recent PyQt5 easyconfigs ([#16469](https://github.com/easybuilders/easybuild-easyconfigs/pull/16469))
    - add extensions to R v4.2.1: LMERConvenienceFunctions ([#16512](https://github.com/easybuilders/easybuild-easyconfigs/pull/16512)), HGNChelper 4.2.1 ([#16744](https://github.com/easybuilders/easybuild-easyconfigs/pull/16744))
    - add extensions to R-bundle-Bioconductor 3.15: SPOTlight ([#16569](https://github.com/easybuilders/easybuild-easyconfigs/pull/16569)), HiCcompare ([#16581](https://github.com/easybuilders/easybuild-easyconfigs/pull/16581)), ROntoTools ([#16636](https://github.com/easybuilders/easybuild-easyconfigs/pull/16636)),
    scDblFinder ([#16686](https://github.com/easybuilders/easybuild-easyconfigs/pull/16686)), numbat ([#16777](https://github.com/easybuilders/easybuild-easyconfigs/pull/16777)), HiCBricks ([#16913](https://github.com/easybuilders/easybuild-easyconfigs/pull/16913)), zellkonverter ([#16952](https://github.com/easybuilders/easybuild-easyconfigs/pull/16952))
    - add libmad dependency to SoX v14.4.2 ([#16758](https://github.com/easybuilders/easybuild-easyconfigs/pull/16758))
    - also install subtree support in recent git easyconfigs ([#16784](https://github.com/easybuilders/easybuild-easyconfigs/pull/16784), [#16785](https://github.com/easybuilders/easybuild-easyconfigs/pull/16785))
    - add extensions to ESM-2 to enhance it for esmfold ([#16841](https://github.com/easybuilders/easybuild-easyconfigs/pull/16841))
    - add libwebp dependency to Pillow-SIMD 9.2.0 to add webp support ([#16844](https://github.com/easybuilders/easybuild-easyconfigs/pull/16844))
    - add KaHIP dependency to OpenFOAM v2206 ([#16974](https://github.com/easybuilders/easybuild-easyconfigs/pull/16974))
    - enable dataset support for recent versions of Arrow ([#16956](https://github.com/easybuilders/easybuild-easyconfigs/pull/16956))

- various bug fixes, including:

    - define `$JUPYTER_PATH` via modextrapaths rather than modextravars for IRkernel 1.x ([#15776](https://github.com/easybuilders/easybuild-easyconfigs/pull/15776))
    - add patches to fix PyTorch 1.10.0 build on POWER ([#15904](https://github.com/easybuilders/easybuild-easyconfigs/pull/15904))
    - fix installation of Python 2.7.18 with GCCcore/11.2.0 (was broken due to 0.0.0 version for some extensions) ([#16485](https://github.com/easybuilders/easybuild-easyconfigs/pull/16485))
    - add patch for M4 1.4.18 to fix glibc v2.34 `SIGSTKSZ` compatibility ([#16486](https://github.com/easybuilders/easybuild-easyconfigs/pull/16486))
    - add patch for pybind11 2.6.0 to fix failing test due to extra whitespace ([#16487](https://github.com/easybuilders/easybuild-easyconfigs/pull/16487))
    - work around installation problem for extensions in Python 2.7.16 easyconfig due to missing build-backend spec in pyproject.toml ([#16490](https://github.com/easybuilders/easybuild-easyconfigs/pull/16490))
    - fix libsanitzer for glibc 2.36 to build GCCcore 10.x and 11.x ([#16502](https://github.com/easybuilders/easybuild-easyconfigs/pull/16502))
    - add OpenBLAS patches to disable FMA in `[cz]cal` and fix crash in `zdot` ([#16510](https://github.com/easybuilders/easybuild-easyconfigs/pull/16510))
    - add missing Perl build dependency GStreamer + add patch to skip trying to make files suid ([#16516](https://github.com/easybuilders/easybuild-easyconfigs/pull/16516))
    - build nodejs with OpenSSL and ICU provided as proper dependencies ([#16529](https://github.com/easybuilders/easybuild-easyconfigs/pull/16529))
    - also define `$JUPYTER_CONFIG_PATH` in IPython and JupyterLab easyconfigs ([#16556](https://github.com/easybuilders/easybuild-easyconfigs/pull/16556))
    - define `$GTKDOCIZE` as `'echo'` before generating configure script for recent HarfBuzz versions ([#16570](https://github.com/easybuilders/easybuild-easyconfigs/pull/16570))
    - disable use of `-Werror` in recent NSS easyconfigs ([#16571](https://github.com/easybuilders/easybuild-easyconfigs/pull/16571))
    - use 'cpan.metacpan.org' rather than 'www.cpan.org' in extension source_urls for recent Perl easyconfigs ([#16611](https://github.com/easybuilders/easybuild-easyconfigs/pull/16611))
    - avoid that zlib + htslib are downloaded and built during installation of MetaBAT ([#16624](https://github.com/easybuilders/easybuild-easyconfigs/pull/16624))
    - add patch to fix installation of MetaBAT 2.15 on non-x86_64 systems ([#16633](https://github.com/easybuilders/easybuild-easyconfigs/pull/16633))
    - add missing pyWannier90 dependency for mcu + enhance sanity check ([#16667](https://github.com/easybuilders/easybuild-easyconfigs/pull/16667))
    - fix `source_urls` for colossalai 0.1.8 (no longer available via PyPI, only via GitHub repo) ([#16693](https://github.com/easybuilders/easybuild-easyconfigs/pull/16693))
    - add patches to fix or skip PyTorch 1.12.1 tests ([#16793](https://github.com/easybuilders/easybuild-easyconfigs/pull/16793))
    - fix checksum for cell2location 0.05-alpha and add missing build dependency on flex ([#16819](https://github.com/easybuilders/easybuild-easyconfigs/pull/16819))
    - upgrade dependency on libdeflate to common v1.8 in fastp and vt easyconfigs using GCC(core)/10.3.0 ([#16839](https://github.com/easybuilders/easybuild-easyconfigs/pull/16839))
    - fix checksum for dlllogger extension in OpenFold v1.0.0 ([#16694](https://github.com/easybuilders/easybuild-easyconfigs/pull/16694))
    - make sure that Python dependency is actually used for VTK 9.0.1 ([#16741](https://github.com/easybuilders/easybuild-easyconfigs/pull/16741))
    - fix homepage for pocl v1.8 ([#16857](https://github.com/easybuilders/easybuild-easyconfigs/pull/16857))
    - fix source_urls in MUMPS easyconfigs ([#16931](https://github.com/easybuilders/easybuild-easyconfigs/pull/16931), [#16932](https://github.com/easybuilders/easybuild-easyconfigs/pull/16932))
    - fix installation of Bowtie2 v2.4.4+ on non-x86_64 systems ([#16946](https://github.com/easybuilders/easybuild-easyconfigs/pull/16946))
    - add missing OpenSSL dependency to DCMTK 3.6.7 ([#16979](https://github.com/easybuilders/easybuild-easyconfigs/pull/16979))
    - fix source URL for PCRE2 ([#16987](https://github.com/easybuilders/easybuild-easyconfigs/pull/16987))
    - add pkgconf dependency for ICU and add patch to avoid trouble with long path names for nodejs-16.15.1/GCCcore-11.3.0 ([#16990](https://github.com/easybuilders/easybuild-easyconfigs/pull/16990))
    - add patch for libwpe 1.13.3 to avoid build issues on CentOS 7 ([#17001](https://github.com/easybuilders/easybuild-easyconfigs/pull/17001))
    - add missing zlib and zstd to GnuTLS ([#17013](https://github.com/easybuilders/easybuild-easyconfigs/pull/17013))
    - add missing pkgconf build dependency to Transformers v4.24.0 ([#17020](https://github.com/easybuilders/easybuild-easyconfigs/pull/17020))
    - fix checksums for `xxx-rocm-4.5.0.tar.gz` source tarballs for Clang-AOMP 4.5.0 ([#17042](https://github.com/easybuilders/easybuild-easyconfigs/pull/17042))
    - replace useless test step for simint 0.7 with (lightweight) sanity check command ([#17044](https://github.com/easybuilders/easybuild-easyconfigs/pull/17044))

- other changes:

    - only give read permissions in GitHub Actions workflows ([#16263](https://github.com/easybuilders/easybuild-easyconfigs/pull/16263))
    - remove ExomeDepth from recent R-bundle-Bioconductor easyconfigs ([#16492](https://github.com/easybuilders/easybuild-easyconfigs/pull/16492))
    - include tqdm as extension in the idemux bundle to avoid multivariant deps on GCCcore-10.2.0 ([#16578](https://github.com/easybuilders/easybuild-easyconfigs/pull/16578))
    - use new EasyBuild logo in README ([#16641](https://github.com/easybuilders/easybuild-easyconfigs/pull/16641))
    - rename hyperopt to Hyperopt, to be consistent with existing Hyperopt easyconfigs ([#16697](https://github.com/easybuilders/easybuild-easyconfigs/pull/16697))
    - automatically cancel Github Action workflow runs for outdated commits ([#16754](https://github.com/easybuilders/easybuild-easyconfigs/pull/16754))
    - use geo moduleclass for SimPEG 0.14.1 ([#16847](https://github.com/easybuilders/easybuild-easyconfigs/pull/16847))


## EasyBuild v4.6.2 (October 21st 2022) {: #release_notes_eb462 }

bugfix/update release

**framework**

- various enhancements, including:
    - add support for easystack file that contains easyconfig
        filenames + implement parsing of configuration options
        ([#4021](https://github.com/easybuilders/easybuild-framework/pull/4021))
    - skip over unset `$EB_PYTHON`/`$EB_INSTALLPYTHON` in eb wrapper
        script
        ([#4080](https://github.com/easybuilders/easybuild-framework/pull/4080))
    - add `GITHUB_RELEASE` and `GITHUB_LOWER_RELEASE` templates
        ([#4084](https://github.com/easybuilders/easybuild-framework/pull/4084))
    - add `%(cuda_cc_cmake)s` template
        ([#4087](https://github.com/easybuilders/easybuild-framework/pull/4087))
- various bug fixes, including:
    - make `check_sha256_checksums` verify all checksums if they're
        specified as a dict value
        ([#4076](https://github.com/easybuilders/easybuild-framework/pull/4076))
    - replace use of symlink with copied files in `alt_location` tests
        to fix failing EasyBuild installation on BeeGFS
        ([#4083](https://github.com/easybuilders/easybuild-framework/pull/4083))
    - fix trying to generate RPATH wrappers for Clang
        ([#4088](https://github.com/easybuilders/easybuild-framework/pull/4088))
    - make sure that GitPython version is a proper version before
        checking minimal required version
        ([#4090](https://github.com/easybuilders/easybuild-framework/pull/4090),
        [#4091](https://github.com/easybuilders/easybuild-framework/pull/4091))
    - first look for patch in `alt_location` when it is specified
        ([#4093](https://github.com/easybuilders/easybuild-framework/pull/4093))
- other changes:
    - make scripts executable
        ([#4081](https://github.com/easybuilders/easybuild-framework/pull/4081))
    - make `--inject-checksums` inject dictionary value for checksums
        which maps filename to SHA256 checksum
        ([#4085](https://github.com/easybuilders/easybuild-framework/pull/4085))
    - update to v3 of actions/checkout and actions/setup-python in CI
        workflows
        ([#4089](https://github.com/easybuilders/easybuild-framework/pull/4089))
    - use `SYSTEM` template constant in dependencies instead of `True`
        in framework tests
        ([#4094](https://github.com/easybuilders/easybuild-framework/pull/4094))

**easyblocks**

- 2 new software-specific easyblock:
    - CUDA compatibility libraries
        ([#2764](https://github.com/easybuilders/easybuild-easyblocks/pull/2764))
        and mamba
        ([#2808](https://github.com/easybuilders/easybuild-easyblocks/pull/2808))
- minor enhancements and updates, including:
    - update OpenFOAM easyblock to support OpenFOAM 10 + clean up
        variant/version checks
        ([#2766](https://github.com/easybuilders/easybuild-easyblocks/pull/2766))
    - added support for ESMPy in ESMF
        ([#2789](https://github.com/easybuilders/easybuild-easyblocks/pull/2789))
    - enhance OpenBLAS easyblock to support running LAPACK test
        suite + checking how many tests fail
        ([#2801](https://github.com/easybuilders/easybuild-easyblocks/pull/2801))
    - make numexpr easyblock aware of toolchain with GCC + imkl
        ([#2810](https://github.com/easybuilders/easybuild-easyblocks/pull/2810))
    - add sanity check commands for netCDF
        ([#2811](https://github.com/easybuilders/easybuild-easyblocks/pull/2811))
- various bug fixes, including:
    - handle problems copying symlink that points to CUDA folder that
        is not created for non CUDA builds of SuiteSparse
        ([#2790](https://github.com/easybuilders/easybuild-easyblocks/pull/2790))
    - don't install docs (to avoid trouble with Java) + add Rocky
        support for ABAQUS
        ([#2792](https://github.com/easybuilders/easybuild-easyblocks/pull/2792))
    - correctly count the number of failing tests (not failing test
        suites) in PyTorch builds
        ([#2794](https://github.com/easybuilders/easybuild-easyblocks/pull/2794),
        [#2803](https://github.com/easybuilders/easybuild-easyblocks/pull/2803))
    - fix docstring for PyTorch easyblock
        ([#2795](https://github.com/easybuilders/easybuild-easyblocks/pull/2795))
    - handle iterative builds with MakeCp easyblock
        ([#2798](https://github.com/easybuilders/easybuild-easyblocks/pull/2798))
    - accept both `None` and empty value for optarch to let OpenCV
        detect host CPU
        ([#2804](https://github.com/easybuilders/easybuild-easyblocks/pull/2804))
    - enhance EasyBuildMeta easyblock: auto-enable installing with
        pip + fix setup.py of easyconfigs package so installation with
        setuptools >= 61.0 works
        ([#2805](https://github.com/easybuilders/easybuild-easyblocks/pull/2805))
    - use `python -m pip` instead of `pip` in PythonPackage easyblock
        ([#2807](https://github.com/easybuilders/easybuild-easyblocks/pull/2807))
- other changes:
    - make the test output from PythonPackage less verbose by
        disabling default search for error patterns done by `run_cmd`
        ([#2797](https://github.com/easybuilders/easybuild-easyblocks/pull/2797))

**easyconfigs**

- add easyconfig for intel/2022.09 toolchain
    ([#16435](https://github.com/easybuilders/easybuild-easyconfigs/pull/16435))
- added example easyconfig files for 25 new software packages:
    - AGAT
        ([#16261](https://github.com/easybuilders/easybuild-easyconfigs/pull/16261)),
        AMAPVox
        ([#16438](https://github.com/easybuilders/easybuild-easyconfigs/pull/16438)),
        Avogadro2
        ([#16257](https://github.com/easybuilders/easybuild-easyconfigs/pull/16257)),
        buildingspy
        ([#16308](https://github.com/easybuilders/easybuild-easyconfigs/pull/16308)),
        CDBtools
        ([#16436](https://github.com/easybuilders/easybuild-easyconfigs/pull/16436)),
        Compress-Raw-Zlib
        ([#16307](https://github.com/easybuilders/easybuild-easyconfigs/pull/16307)),
        CUDAcompat
        ([#15892](https://github.com/easybuilders/easybuild-easyconfigs/pull/15892)),
        CWIPI
        ([#16342](https://github.com/easybuilders/easybuild-easyconfigs/pull/16342)),
        enchant-2
        ([#16082](https://github.com/easybuilders/easybuild-easyconfigs/pull/16082),
        [#16319](https://github.com/easybuilders/easybuild-easyconfigs/pull/16319)),
        f90wrap
        ([#16346](https://github.com/easybuilders/easybuild-easyconfigs/pull/16346)),
        Imath
        ([#16276](https://github.com/easybuilders/easybuild-easyconfigs/pull/16276)),
        Mamba
        ([#16432](https://github.com/easybuilders/easybuild-easyconfigs/pull/16432)),
        Miller
        ([#16221](https://github.com/easybuilders/easybuild-easyconfigs/pull/16221)),
        nghttp2
        ([#16096](https://github.com/easybuilders/easybuild-easyconfigs/pull/16096)),
        ngtcp2
        ([#16098](https://github.com/easybuilders/easybuild-easyconfigs/pull/16098)),
        NVSHMEM
        ([#16254](https://github.com/easybuilders/easybuild-easyconfigs/pull/16254)),
        pairsnp
        ([#16331](https://github.com/easybuilders/easybuild-easyconfigs/pull/16331)),
        paladin
        ([#16320](https://github.com/easybuilders/easybuild-easyconfigs/pull/16320)),
        PyMOL
        ([#16394](https://github.com/easybuilders/easybuild-easyconfigs/pull/16394)),
        python-irodsclient
        ([#16328](https://github.com/easybuilders/easybuild-easyconfigs/pull/16328)),
        ruffus
        ([#16428](https://github.com/easybuilders/easybuild-easyconfigs/pull/16428)),
        TELEMAC-MASCARET
        ([#16274](https://github.com/easybuilders/easybuild-easyconfigs/pull/16274)),
        torchdata
        ([#16344](https://github.com/easybuilders/easybuild-easyconfigs/pull/16344)),
        Waylandpp
        ([#16092](https://github.com/easybuilders/easybuild-easyconfigs/pull/16092)),
        x13as
        ([#16163](https://github.com/easybuilders/easybuild-easyconfigs/pull/16163))
- added additional easyconfigs for various supported software
    packages, including:
    - Amber 22.0, AMS 2022.102, ASE 3.22.1, atools 1.5.1, Beast 2.6.7,
        biogeme 3.2.10, Boost.Python 1.79.0, ccache 4.6.3, dbus-glib
        0.112, Delly 1.1.5, ESMF 8.3.0, expat 2.4.9, FDS 6.7.9, file
        5.43, FLTK 1.3.8, FTGL 2.4.0, gc 8.2.2, GitPython 3.1.27, Go
        1.18.3, GPAW 22.8.0, Guile 3.0.8, htop 3.2.1, hunspell 1.7.1,
        IPython 8.5.0, jq 1.6, Julia 1.8.2, LDC 1.30.0, libcint 5.1.6,
        libconfig 1.7.3, libreadline 8.2, LibSoup 3.0.7, LIBSVM 3.30,
        libwebp 1.2.4, likwid 5.2.2, MariaDB 10.9.3, matplotlib 3.5.2,
        ncdu 1.17, netcdf4-python 1.6.1, Nextflow 22.10.0, NFFT 3.5.3,
        Nipype 1.8.5, numactl 2.0.16, onedrive 2.4.21, OpenCV 4.6.0,
        OpenEXR 3.1.5, OpenJPEG 2.5.0, OpenMM 7.7.0, OpenPGM 5.2.122,
        OpenSSL 1.1.1q, Perl 5.36.0, Pillow-SIMD 9.2.0, pkgconf 1.9.3,
        PostgreSQL 14.4, PyCharm 2022.2.2, PyTorch 1.12.0, PyTorch
        1.12.0, PyTorch-Lightning 1.7.7, RDFlib 6.2.0, SAMtools 1.16.1,
        scikit-learn 1.1.2, Score-P 7.1, SDL2 2.0.22, spaln 2.4.12,
        spglib-python 2.0.0, SuiteSparse 5.13.0, SUNDIALS 6.3.0, sympy
        1.11.1, tensorboard 2.10.0, torchvision 0.13.1, TRIQS 3.1.1,
        TRIQS-cthyb 3.1.0, TRIQS-dft_tools 3.1.0, TRIQS-tprf 3.1.1,
        TRUST4 1.0.7, TurboVNC 3.0.1, typing-extensions 4.3.0, UCX
        1.13.1, umap-learn 0.5.3, VEP 107, VMD 1.9.4a57, Wayland 1.21.0,
        wxWidgets 3.2.1, xprop 1.2.5
- minor enhancements, including:
    - configure recent pocl versions with `-DLLC_HOST_CPU=native` to
        avoid CPU auto-detection
        ([#16246](https://github.com/easybuilders/easybuild-easyconfigs/pull/16246))
    - add multi-dep exception to easyconfigs test suite for
        ncbi-vdb-3.0.0 which requires HDF5 1.10.x
        ([#16316](https://github.com/easybuilders/easybuild-easyconfigs/pull/16316))
    - enable running of LAPACK tests for recent OpenBLAS easyconfigs +
        add patch to fix failing LAPACK tests due to use of
        `-ftree-vectorize`
        ([#16406](https://github.com/easybuilders/easybuild-easyconfigs/pull/16406))
    - add `GITHUB_(LOWER_)RELEASE` to known constants in `setup.cfg`
        ([#16422](https://github.com/easybuilders/easybuild-easyconfigs/pull/16422))
    - add AMAPVox extension to R v4.2.1
        ([#16439](https://github.com/easybuilders/easybuild-easyconfigs/pull/16439))
    - add OpenEXR dependency to POV-Ray 3.7.0.10
        ([#16408](https://github.com/easybuilders/easybuild-easyconfigs/pull/16408))
- various bug fixes, including:
    - add patch for OpenBLAS 0.3.7-0.3.12 to fix miscomputation on
        POWER
        ([#16199](https://github.com/easybuilders/easybuild-easyconfigs/pull/16199))
    - skip flaky test in PyTorch 1.9.0
        ([#16258](https://github.com/easybuilders/easybuild-easyconfigs/pull/16258))
    - add `--with-versioned-syms` to ncurses 6.2 and 6.3
        ([#16270](https://github.com/easybuilders/easybuild-easyconfigs/pull/16270))
    - add missing pkg-config build dependency to Guile
        ([#16317](https://github.com/easybuilders/easybuild-easyconfigs/pull/16317))
    - add patches to fix incompatibilites between ASE and other
        packages in 2022a toolchain
        ([#16332](https://github.com/easybuilders/easybuild-easyconfigs/pull/16332))
    - add patches to fix PyTorch 1.11 on POWER
        ([#16339](https://github.com/easybuilders/easybuild-easyconfigs/pull/16339))
    - add patches for Ambertools 21 to Amber 20.11 to work with
        updated Amber easyblock
        ([#16343](https://github.com/easybuilders/easybuild-easyconfigs/pull/16343))
    - use Intel MPI from EasyBuild toolchain in AMS
        ([#16363](https://github.com/easybuilders/easybuild-easyconfigs/pull/16363))
    - fix execution permissions for `bin/ngm*` for NextGenMap v0.5.5
        ([#16383](https://github.com/easybuilders/easybuild-easyconfigs/pull/16383))
    - fix using provided Qhull and freetype dependencies for
        matplotlib 3.5.2 by creating `mplsetup.cfg` rather than
        `setup.cfg`
        ([#16396](https://github.com/easybuilders/easybuild-easyconfigs/pull/16396))
    - fix GitHub download link in for libpsl 0.21.1
        ([#16397](https://github.com/easybuilders/easybuild-easyconfigs/pull/16397))
    - stick to http in source URL for `stride.tar.gz` in VMD 1.9.4a51
        easyconfigs due to problems with SSL certificate
        ([#16403](https://github.com/easybuilders/easybuild-easyconfigs/pull/16403))
    - add patch to detect available cores and remove unneeded deps for
        Unicycler 0.5.0
        ([#16407](https://github.com/easybuilders/easybuild-easyconfigs/pull/16407))
    - add missing ICU + libunistring dependencies for libpsl 0.21.1 w/
        GCCcore/10.3.0
        ([#16410](https://github.com/easybuilders/easybuild-easyconfigs/pull/16410))
    - add patch to GCC 11.x + 12.x to fix vectorizer bug
        ([#16411](https://github.com/easybuilders/easybuild-easyconfigs/pull/16411))
    - fix checksum for GULP 6.1
        ([#16423](https://github.com/easybuilders/easybuild-easyconfigs/pull/16423))
    - add bzip2 and libxml2 as dependencies for netCDF 4.9.0
        ([#16450](https://github.com/easybuilders/easybuild-easyconfigs/pull/16450))
- other changes:
    - drop Java dep from ABAQUS 2022
        ([#16314](https://github.com/easybuilders/easybuild-easyconfigs/pull/16314))
    - deprecate use of `True` in favour of `SYSTEM` for
        system-toolchain dependencies in easyconfigs using a recent
        toolchain version (>2019b)
        ([#16384](https://github.com/easybuilders/easybuild-easyconfigs/pull/16384))
    - update easyconfigs to use `SYSTEM` template constant instead of
        `True` in dependencies
        ([#16386](https://github.com/easybuilders/easybuild-easyconfigs/pull/16386),
        [#16418](https://github.com/easybuilders/easybuild-easyconfigs/pull/16418))
    - update libxml2 + libxslt easyconfigs to use `gnome.org` source
        URL
        ([#16429](https://github.com/easybuilders/easybuild-easyconfigs/pull/16429))


## EasyBuild v4.6.1 (September 12th 2022) {: #release_notes_eb461 }

bugfix/update release

**framework**

- various enhancements, including:
    - add script to find dependencies of Python packages
        ([#3839](https://github.com/easybuilders/easybuild-framework/pull/3839))
    - add `ai` default module class
        ([#4053](https://github.com/easybuilders/easybuild-framework/pull/4053))
- various bug fixes, including:
    - fix code style issues reported by recent flake8 linter
        ([#4049](https://github.com/easybuilders/easybuild-framework/pull/4049))
    - stick to autopep8 < 1.7.0 with Python 2.7
        ([#4055](https://github.com/easybuilders/easybuild-framework/pull/4055))
    - ensure we call `EasyBlock.patch_step` for `postinstallpatches`
        ([#4063](https://github.com/easybuilders/easybuild-framework/pull/4063))
    - fix leaked handles in `set_columns`, `complete_cmd`,
        `run_cmd_qa`, `det_terminal_size functions` + tests
        ([#4066](https://github.com/easybuilders/easybuild-framework/pull/4066))
    - fix `quote_str` when string with both `'` and `"` ends with a
        double quote
        ([#4068](https://github.com/easybuilders/easybuild-framework/pull/4068))
    - fix type-checking of patches to allow dict values + correctly
        handle patches specified as dict values in `--new-pr`
        ([#4070](https://github.com/easybuilders/easybuild-framework/pull/4070))
    - relax toolchain test by accepting both `-march=native` (x86_64)
        and `-mcpu=native` (aarch64)
        ([#4071](https://github.com/easybuilders/easybuild-framework/pull/4071))
- other changes:
    - run python in the same process as `eb` wrapper script by using
        `exec`
        ([#4048](https://github.com/easybuilders/easybuild-framework/pull/4048))
    - add `get_linked_libs_raw` function, and use it from both
        `check_linked_shared_libs` and `sanity_check_rpath`
        ([#4051](https://github.com/easybuilders/easybuild-framework/pull/4051))
    - update CI workflows (except container tests) to use Ubuntu
        20.04, since Ubuntu 18.04 is deprecated
        ([#4064](https://github.com/easybuilders/easybuild-framework/pull/4064))
    - use `SYSTEM` constant for dependency that uses system toolchain
        in dumped easyconfig
        ([#4069](https://github.com/easybuilders/easybuild-framework/pull/4069))

**easyblocks**

- minor enhancements and updates, including:
    - update LAMMPS easyblock for LAMMPS/23Jun22
        ([#2213](https://github.com/easybuilders/easybuild-easyblocks/pull/2213))
    - reduce the number of command line options for `cmake` command in
        CMakeMake generic easyblock
        ([#2514](https://github.com/easybuilders/easybuild-easyblocks/pull/2514))
    - update libQGLViewer easyblock to take into account changes in
        the shared library names depending on Qt versions they are
        compiled with
        ([#2730](https://github.com/easybuilders/easybuild-easyblocks/pull/2730))
    - improve PLUMED detection in GROMACS easyblock
        ([#2749](https://github.com/easybuilders/easybuild-easyblocks/pull/2749))
    - make `$LD_LIBRARY_PATH` detection more robust for LAMMPS
        ([#2765](https://github.com/easybuilders/easybuild-easyblocks/pull/2765))
    - enhance NVHPC easyblock to avoid superfluous warning
        ([#2767](https://github.com/easybuilders/easybuild-easyblocks/pull/2767))
    - enhance PyTorch easyblock to also capture tests failing with
        signal
        ([#2768](https://github.com/easybuilders/easybuild-easyblocks/pull/2768))
    - enhance PythonPackage easyblock to make sure all test command
        output makes it to the EasyBuild log, also when
        `return_output_ec=True`
        ([#2770](https://github.com/easybuilders/easybuild-easyblocks/pull/2770))
    - set `$NVHPC_CUDA_HOME` for NVHPC 22.7+
        ([#2776](https://github.com/easybuilders/easybuild-easyblocks/pull/2776))
- various bug fixes, including:
    - make Amber easyblock aware of FlexiBLAS
        ([#2720](https://github.com/easybuilders/easybuild-easyblocks/pull/2720))
    - update PyTorch easyblock to configure without breakpad support
        on POWER
        ([#2763](https://github.com/easybuilders/easybuild-easyblocks/pull/2763))
    - use `lib*` in `post_install` step of FFTW.MPI easyblock to fix
        paths not being found on Linux distros favouring lib64 (like
        Suse/SLES)
        ([#2771](https://github.com/easybuilders/easybuild-easyblocks/pull/2771))
    - use `det_cmake_version` function to determine CMake version in
        CMakeMake generic easyblock
        ([#2772](https://github.com/easybuilders/easybuild-easyblocks/pull/2772))
    - don't enable building of `ld.gold` when installing binutils on
        a RISC-V system + don't configure GCC to use gold as default
        linker on a RISC-V system
        ([#2780](https://github.com/easybuilders/easybuild-easyblocks/pull/2780))
    - tweak Amber(Tools) easyblock to run tests from top-level
        directory
        ([#2781](https://github.com/easybuilders/easybuild-easyblocks/pull/2781))
    - fix version check for NVPTX library in sanity check of Clang
        easyblock
        ([#2783](https://github.com/easybuilders/easybuild-easyblocks/pull/2783))
- other changes:
    - update CI workflows to use Ubuntu 20.04 (since Ubuntu 18.04 is
        deprecated)
        ([#2779](https://github.com/easybuilders/easybuild-easyblocks/pull/2779))

**easyconfigs**

- added example easyconfig files for 37 new software packages:
    - AptaSUITE
        ([#8583](https://github.com/easybuilders/easybuild-easyconfigs/pull/8583)),
        BigDFT
        ([#15860](https://github.com/easybuilders/easybuild-easyconfigs/pull/15860)),
        colossalai
        ([#15971](https://github.com/easybuilders/easybuild-easyconfigs/pull/15971)),
        CrystFEL
        ([#8407](https://github.com/easybuilders/easybuild-easyconfigs/pull/8407)),
        Dakota
        ([#15883](https://github.com/easybuilders/easybuild-easyconfigs/pull/15883),
        [#16210](https://github.com/easybuilders/easybuild-easyconfigs/pull/16210)),
        FastFold
        ([#15972](https://github.com/easybuilders/easybuild-easyconfigs/pull/15972)),
        fastparquet
        ([#15020](https://github.com/easybuilders/easybuild-easyconfigs/pull/15020)),
        FOX-Toolkit
        ([#15986](https://github.com/easybuilders/easybuild-easyconfigs/pull/15986)),
        GLM-AED
        ([#15879](https://github.com/easybuilders/easybuild-easyconfigs/pull/15879)),
        hiredis
        ([#16071](https://github.com/easybuilders/easybuild-easyconfigs/pull/16071)),
        how_are_we_stranded_here
        ([#16220](https://github.com/easybuilders/easybuild-easyconfigs/pull/16220),
        [#16227](https://github.com/easybuilders/easybuild-easyconfigs/pull/16227)),
        indicators
        ([#16209](https://github.com/easybuilders/easybuild-easyconfigs/pull/16209)),
        JavaFX
        ([#8583](https://github.com/easybuilders/easybuild-easyconfigs/pull/8583)),
        json-fortran
        ([#15979](https://github.com/easybuilders/easybuild-easyconfigs/pull/15979)),
        jupyter-resource-usage
        ([#15834](https://github.com/easybuilders/easybuild-easyconfigs/pull/15834)),
        libev
        ([#16086](https://github.com/easybuilders/easybuild-easyconfigs/pull/16086)),
        libmad
        ([#16067](https://github.com/easybuilders/easybuild-easyconfigs/pull/16067)),
        libplinkio
        ([#13040](https://github.com/easybuilders/easybuild-easyconfigs/pull/13040)),
        LuaJIT2-OpenResty
        ([#16047](https://github.com/easybuilders/easybuild-easyconfigs/pull/16047)),
        MetaMorpheus
        ([#15825](https://github.com/easybuilders/easybuild-easyconfigs/pull/15825)),
        mgltools
        ([#16226](https://github.com/easybuilders/easybuild-easyconfigs/pull/16226)),
        miniasm
        ([#15858](https://github.com/easybuilders/easybuild-easyconfigs/pull/15858)),
        muMerge
        ([#16115](https://github.com/easybuilders/easybuild-easyconfigs/pull/16115)),
        nano
        ([#16198](https://github.com/easybuilders/easybuild-easyconfigs/pull/16198)),
        nghttp3
        ([#16097](https://github.com/easybuilders/easybuild-easyconfigs/pull/16097)),
        olaFlow
        ([#16021](https://github.com/easybuilders/easybuild-easyconfigs/pull/16021)),
        OpenFAST
        ([#15983](https://github.com/easybuilders/easybuild-easyconfigs/pull/15983),
        [#15983](https://github.com/easybuilders/easybuild-easyconfigs/pull/15983)),
        OpenFold
        ([#15971](https://github.com/easybuilders/easybuild-easyconfigs/pull/15971)),
        Phantompeakqualtools
        ([#15871](https://github.com/easybuilders/easybuild-easyconfigs/pull/15871)),
        pyGenomeTracks
        ([#16143](https://github.com/easybuilders/easybuild-easyconfigs/pull/16143)),
        QuickPIC
        ([#15978](https://github.com/easybuilders/easybuild-easyconfigs/pull/15978)),
        RheoTool
        ([#16077](https://github.com/easybuilders/easybuild-easyconfigs/pull/16077)),
        Satsuma2
        ([#16068](https://github.com/easybuilders/easybuild-easyconfigs/pull/16068)),
        SMC++
        ([#16017](https://github.com/easybuilders/easybuild-easyconfigs/pull/16017)),
        stripy
        ([#15866](https://github.com/easybuilders/easybuild-easyconfigs/pull/15866)),
        UCC-CUDA
        ([#15956](https://github.com/easybuilders/easybuild-easyconfigs/pull/15956)),
        VESTA
        ([#16217](https://github.com/easybuilders/easybuild-easyconfigs/pull/16217))
- added additional easyconfigs for various supported software
    packages, including:
    - alevin-fry 0.6.0, AmberTools 22.3, arrow-R 8.0.0, ASE 3.22.1,
        BBMap 38.98, BCFtools 1.15.1, binutils 2.39, BLAST+ 2.13.0,
        Bowtie2 2.4.5, BUSCO 5.4.3, CapnProto 0.10.2, Cartopy 0.20.3,
        ccache 4.6.1, cclib 1.7.2, CDO 2.0.5, CellRanger-ATAC 2.1.0,
        CoordgenLibs 3.0.1, cURL 7.84.0, cuTENSOR 1.6.0.3, einops 0.4.1,
        Elk 8.5.2, Emacs 28.1, Embree 3.13.4, FFmpeg 4.4.2 + 5.0.1, fio
        3.32, Flask 2.2.2, Flye 2.9.1, fmt 9.1.0, FORD 6.1.15,
        FreeSurfer 7.3.2, GATE 9.2, GATK 4.2.6.1, GCC(core) 12.2.0, GDB
        12.1, Geant4 11.0.2, GetOrganelle 1.7.6.1, gifsicle 1.93, GLFW
        3.3.8, glib-networking 2.72.1, Globus-CLI 3.6.0, gnuplot 5.4.4,
        gperftools 2.10, Graphviz 5.0.0, Gurobi 9.5.2, HDF5 1.12.2,
        HTSlib 1.15.1, Hypre 2.25.0, Jansson 2.14, jax 0.3.14, Kalign
        3.3.2, kim-api 2.3.0, LAMMPS 23Jun2022, libcerf 2.1, libdwarf
        0.4.1, Libint 2.7.2, libQGLViewer 2.8.0, LibSoup 2.74.0, libzip
        1.9.2, Lua 5.4.4, lxml 4.9.1, maeparser 1.3.0, matplotlib 3.5.2,
        MATSim 14.0, MDAnalysis 2.2.0, medaka 1.6.0, Megalodon 2.5.0,
        Mercurial 6.2, MetaEuk 6, Mini-XML-3.3.1, MUMmer 4.0.0rc1, MUMPS
        5.5.1, netCDF-Fortran 4.6.0, NGSpeciesID 0.1.2.1, ont-remora
        1.0.0, OpenFOAM v2206, OTF2 3.0, parallel 20220722, ParaView
        5.10.1, patchelf 0.15.0, Perl 5.36.0, pftoolsV3 3.2.12, PLINK
        2.00a3.6, pretty-yaml 21.10.1, PRSice 2.3.5, pugixml 1.12.1,
        Pyomo 6.4.2, PyOpenCL 2021.2.13, Pysam 0.19.1, PyStan 3.5.0,
        PyYAML 6.0, RDKit 2022.03.5, scikit-bio 0.5.7, scikit-build
        0.15.0, scikit-learn 1.1.2, scikit-optimize 0.9.0, SCOTCH 7.0.1,
        SIONlib 1.7.7, SISSO 3.1, spglib-python 2.0.0, Stacks 2.62,
        Stata 17, SUMO 1.14.1, tbb 2021.5.0, tqdm 4.64.0, Transformers
        4.21.1, Trycycler 0.5.3, Unicycler 0.5.0, Valgrind 3.19.0,
        ViennaRNA 2.5.1, VTune 2022.3.0.eb, wxPython 4.1.1, x264
        20220620, Z3 4.10.2, zfp 1.0.0
- minor enhancements, including:
    - add alternate download URL for Voro++
        ([#15898](https://github.com/easybuilders/easybuild-easyconfigs/pull/15898))
    - add extra symlinks and sanity checks for libtinfo in ncurses
        ([#15903](https://github.com/easybuilders/easybuild-easyconfigs/pull/15903))
    - include some easyconfig constants in flake8 configuration file
        ([#16040](https://github.com/easybuilders/easybuild-easyconfigs/pull/16040))
    - add pigz dependency for cutadapt v3.4 + v3.5
        ([#16056](https://github.com/easybuilders/easybuild-easyconfigs/pull/16056))
    - add sanity check commands for recent gettext versions (>=
        0.20.x)
        ([#16091](https://github.com/easybuilders/easybuild-easyconfigs/pull/16091))
- various bug fixes, including:
    - use correct Matlab Runtime Compiler (v8.4) for FreeSurfer v7.1.1
        ([#13375](https://github.com/easybuilders/easybuild-easyconfigs/pull/13375))
    - fix set-alias statements for MaxQuant v2.0.3.0
        ([#15743](https://github.com/easybuilders/easybuild-easyconfigs/pull/15743))
    - add Autotools build dependency to R 4.2.0 w/ foss 2021b
        ([#15822](https://github.com/easybuilders/easybuild-easyconfigs/pull/15822))
    - add patch for BLIS to fix auto-detection of POWER
        ([#15826](https://github.com/easybuilders/easybuild-easyconfigs/pull/15826))
    - downgrade SPAdes dependency to v3.13.1 for Unicycler 0.4.9 since
        v3.15.3 is too new
        ([#15840](https://github.com/easybuilders/easybuild-easyconfigs/pull/15840))
    - explicitly enable HDF5 from kallisto v0.46.2 onwards
        ([#15843](https://github.com/easybuilders/easybuild-easyconfigs/pull/15843))
    - add CVE patch for XZ 5.2.5 + attempt to fix symbol patch for all
        OSs
        ([#15856](https://github.com/easybuilders/easybuild-easyconfigs/pull/15856))
    - use build environment set by EasyBuild and add missing
        dependency on zlib to minimap2
        ([#15859](https://github.com/easybuilders/easybuild-easyconfigs/pull/15859))
    - add missing dependencies and execute tests on Trycycler v0.5.2
        ([#15864](https://github.com/easybuilders/easybuild-easyconfigs/pull/15864))
    - add patch for AlphaFold v2.2.2 to fix NaN problem with jax 0.3.9
        ([#15874](https://github.com/easybuilders/easybuild-easyconfigs/pull/15874))
    - exclude (flaky) `fault_tolerance_test` and fix non-x86 build for
        TensorFlow 2.7.1
        ([#15882](https://github.com/easybuilders/easybuild-easyconfigs/pull/15882))
    - work around miscompilation of OpenBLAS on POWER by compiling
        with `-fstack-protector-strong`
        ([#15885](https://github.com/easybuilders/easybuild-easyconfigs/pull/15885))
    - fix tests on POWER9 for BLIS 0.9.0 + fix auto-detect for POWER10
        for BLIS (AMD) v2.0 + v3.0
        ([#15889](https://github.com/easybuilders/easybuild-easyconfigs/pull/15889))
    - add and fix patches for PyTorch 1.9.0 on POWER
        ([#15919](https://github.com/easybuilders/easybuild-easyconfigs/pull/15919))
    - exclude Binary, PackedBinary and JAR easyblocks from binutils
        build requirements
        ([#15932](https://github.com/easybuilders/easybuild-easyconfigs/pull/15932))
    - consistently add libffi + elfutils dependencies to recent Clang
        easyconfigs
        ([#15935](https://github.com/easybuilders/easybuild-easyconfigs/pull/16935),
        [#16225](https://github.com/easybuilders/easybuild-easyconfigs/pull/16225))
    - add patch to fix broken test on POWER for numpy in SciPy-bundle
        2022.05
        ([#15968](https://github.com/easybuilders/easybuild-easyconfigs/pull/15968))
    - refactor checksum test for extensions to use
        `collect_exts_file_info`
        ([#15973](https://github.com/easybuilders/easybuild-easyconfigs/pull/15973))
    - fix dependency on FOX Toolkit in SUMO
        ([#15986](https://github.com/easybuilders/easybuild-easyconfigs/pull/15986))
    - add missing SciPy-bundle dependency for rMATS-turbo
        ([#15988](https://github.com/easybuilders/easybuild-easyconfigs/pull/15988))
    - explicitly download wannier90 source tarball from wannier90
        GitHub repository in QuantumESPRESSO 7.1 easyconfigs
        ([#15993](https://github.com/easybuilders/easybuild-easyconfigs/pull/15993))
    - restore ploteig in EIGENSOFT 7.2.1
        ([#15996](https://github.com/easybuilders/easybuild-easyconfigs/pull/15996))
    - add alternative checksum for plot3Drgl extension in R v4.1.x +
        v4.2.0 easyconfigs
        ([#16011](https://github.com/easybuilders/easybuild-easyconfigs/pull/16011))
    - add patch to fix missing sync in LINCS and SETTLE CUDA kernels
        for GROMACS 2020
        ([#16027](https://github.com/easybuilders/easybuild-easyconfigs/pull/16027))
        and 2021
        ([#16026](https://github.com/easybuilders/easybuild-easyconfigs/pull/16026))
    - exclude failing test in TensorFlow 2.4.1
        ([#16042](https://github.com/easybuilders/easybuild-easyconfigs/pull/16042))
    - skip NASA performance and remote server tests in netCDF v4.9.0
        ([#16050](https://github.com/easybuilders/easybuild-easyconfigs/pull/16050),
        [#16158](https://github.com/easybuilders/easybuild-easyconfigs/pull/16158))
    - use versioned symbols in ncurses built with system toolchain (by
        adding `--with-versioned-syms` configure option)
        ([#16064](https://github.com/easybuilders/easybuild-easyconfigs/pull/16064))
    - add patch to fix pkgconfig file for Blitz++ v1.0.2
        ([#16102](https://github.com/easybuilders/easybuild-easyconfigs/pull/16102))
    - add missing BCFtools dependency for recent medaka versions
        ([#16107](https://github.com/easybuilders/easybuild-easyconfigs/pull/16107))
    - add GTK2 v2.24.33 as a dependency for Ghostscript v9.56.1
        ([#16112](https://github.com/easybuilders/easybuild-easyconfigs/pull/16112))
    - fix checksum for Stacks v2.62 (due to silent re-release without
        version bump)
        ([#16134](https://github.com/easybuilders/easybuild-easyconfigs/pull/16134))
    - fix libsanitzer for glibc 2.36 to build GCCcore 11.3.0
        ([#16145](https://github.com/easybuilders/easybuild-easyconfigs/pull/16145))
    - fix top level Makefile for AmberTools 20 and enable tests
        ([#16150](https://github.com/easybuilders/easybuild-easyconfigs/pull/16150))
    - add missing patches + enable running tests for AmberTools 21
        with intel/2021a
        ([#16151](https://github.com/easybuilders/easybuild-easyconfigs/pull/16151))
        and intel/2021b
        ([#16152](https://github.com/easybuilders/easybuild-easyconfigs/pull/16152))
    - replace HDF5 v1.13.1 with v1.12.1 as dependency, since we
        shouldn't use odd minor versions of HDF5 which are not stable
        releases
        ([#16153](https://github.com/easybuilders/easybuild-easyconfigs/pull/16153))
    - remove modextrapaths to add top-level install directory to
        `$PATH`for recent InterProScan easyconfigs (now done by default
        by Binary easyblock)
        ([#16167](https://github.com/easybuilders/easybuild-easyconfigs/pull/16167))
    - fix sources + source URL + homepage for Molekel v5.4.0
        ([#16219](https://github.com/easybuilders/easybuild-easyconfigs/pull/16219))
    - consistently add maeparser + CoordgenLibs dependencies to
        OpenBabel 3.1.1 easyconfigs
        ([#16231](https://github.com/easybuilders/easybuild-easyconfigs/pull/16231))
    - fix checksum for CUDA 11.4.1 aarch64 installer
        ([#16234](https://github.com/easybuilders/easybuild-easyconfigs/pull/16234))
    - remove incorrect comment for Boost dependency in OpenBabel 3.1.1
        easyconfigs
        ([#16238](https://github.com/easybuilders/easybuild-easyconfigs/pull/16238))
    - add direct Pango dependency in recent ImageMagick easyconfigs
        ([#16237](https://github.com/easybuilders/easybuild-easyconfigs/pull/16237))
- other changes:
    - remove superfluous `-DCMAKE_BUILD_TYPE=Release`, use of
        `build_type = Release`, or enabling `separate_build_dir` from
        easyconfigs using CMakeMake easyblock
        ([#13384](https://github.com/easybuilders/easybuild-easyconfigs/pull/13384))
    - synchronize ncurses easyconfigs using system toolchain
        ([#15903](https://github.com/easybuilders/easybuild-easyconfigs/pull/15903))
    - stick to Java/11 as dependency for Bazel 5.1.1 (which is
        available for x86_64, aarch64, ppc64le)
        ([#15906](https://github.com/easybuilders/easybuild-easyconfigs/pull/15906))
    - speed up OpenMPI 4.1.4 configure by not running
        `autogen.pl --force`, but only running required Autotools
        commands
        ([#15957](https://github.com/easybuilders/easybuild-easyconfigs/pull/15957))
    - replace sed commands by upstreamed patches for BLIS built with
        intel-compilers toolchain
        ([#15958](https://github.com/easybuilders/easybuild-easyconfigs/pull/15958))
    - simplify AlphaFold foss/2021a easyconfigs by using a fleshed out
        patched OpenMM dependency
        ([#15981](https://github.com/easybuilders/easybuild-easyconfigs/pull/15981))
    - update Java/11 to 11.0.16 and Java/17 to 17.0.4
        ([#16001](https://github.com/easybuilders/easybuild-easyconfigs/pull/16001))
    - remove unnecessary patch in recent JupyterLab
        ([#16030](https://github.com/easybuilders/easybuild-easyconfigs/pull/16030))
    - update CI workflows to use Ubuntu 20.04 (since Ubuntu 18.04 is
        deprecated)
        ([#16070](https://github.com/easybuilders/easybuild-easyconfigs/pull/16070))
    - make check for toolchain value in dependency spec in easyconfigs
        test suite aware that dumped easyconfig uses `SYSTEM` constant
        ([#16126](https://github.com/easybuilders/easybuild-easyconfigs/pull/16126))

## EasyBuild v4.6.0 (July 8th 2022) {: #release_notes_eb460 }

feature release

**framework**

- various enhancements, including:
    - allow searching for sources/patches in alternative location by
        specifying '`alt_location`' in source/patch spec
        ([#3994](https://github.com/easybuilders/easybuild-framework/pull/3994))
    - show URLs used for download attempts in trace output
        ([#4026](https://github.com/easybuilders/easybuild-framework/pull/4026))
    - add support for setting environment variables via '`pushenv`'
        with `modextravars`
        ([#4030](https://github.com/easybuilders/easybuild-framework/pull/4030))
    - add support for OneAPI compilers using toolchain option
        '`oneapi`'
        ([#4031](https://github.com/easybuilders/easybuild-framework/pull/4031),
        [#4032](https://github.com/easybuilders/easybuild-framework/pull/4032),
        [#4039](https://github.com/easybuilders/easybuild-framework/pull/4039))
    - make `check_linked_shared_libs` more robust by taking into
        account that '`ldd`' may fail
        ([#4033](https://github.com/easybuilders/easybuild-framework/pull/4033))
    - fall back to sequential extension install if parallel install is
        not implemented
        ([#4034](https://github.com/easybuilders/easybuild-framework/pull/4034))
    - add support for using template values in name/version of
        extensions
        ([#4036](https://github.com/easybuilders/easybuild-framework/pull/4036))
- various bug fixes, including:
    - make sure that `ARCH` constant has '`aarch64`' (rather than
        '`arm64`') as value on macOS ARM
        ([#4018](https://github.com/easybuilders/easybuild-framework/pull/4018))
    - tweak '`eb`' wrapper script to correctly handle errors when
        python command being considered fails to run
        ([#4019](https://github.com/easybuilders/easybuild-framework/pull/4019))
    - tweak `is_patch_for` function to make it more robust
        ([#4028](https://github.com/easybuilders/easybuild-framework/pull/4028))
- other changes:
    - update Lmod used to run tests to version 8.7.6
        ([#4027](https://github.com/easybuilders/easybuild-framework/pull/4027),
        [#4030](https://github.com/easybuilders/easybuild-framework/pull/4030))
    - tweak `apply_patch` to not create `.orig files` (by default)
        when applying patch files
        ([#4038](https://github.com/easybuilders/easybuild-framework/pull/4038))

**easyblocks**

- new software-specific easyblock for STAR-CCM+
    ([#1613](https://github.com/easybuilders/easybuild-easyblocks/pull/1613))
- minor enhancements and updates, including:
    - update Siesta EasyBlock to support GCC 10+ by adding
        `-fallow-argument-mismatch` Fortran compiler option
        ([#2690](https://github.com/easybuilders/easybuild-easyblocks/pull/2690))
    - enable building of shared library for Libint 2.7+
        ([#2738](https://github.com/easybuilders/easybuild-easyblocks/pull/2738))
    - allow some PyTorch tests to fail + print warning if one or more
        tests fail
        ([#2742](https://github.com/easybuilders/easybuild-easyblocks/pull/2742))
    - also support OpenSSL 3.0 in OpenSSL wrapper easyblock
        ([#2746](https://github.com/easybuilders/easybuild-easyblocks/pull/2746))
    - add more logging to `install_pc_files` method of OpenSSL wrapper
        easyblock
        ([#2752](https://github.com/easybuilders/easybuild-easyblocks/pull/2752))
    - make WPS easyblock aware of `(pre)buildopts`
        ([#2754](https://github.com/easybuilders/easybuild-easyblocks/pull/2754))
    - add Abseil system dependency for TensorFlow 2.9+
        ([#2757](https://github.com/easybuilders/easybuild-easyblocks/pull/2757))
    - disable altivec when building FFTW versions < 3.4 with
        single-precision with GCC on POWER
        ([#2758](https://github.com/easybuilders/easybuild-easyblocks/pull/2758))
- various bug fixes, including:
    - make VEP easyblock compatible with `--sanity-check-only`
        ([#2743](https://github.com/easybuilders/easybuild-easyblocks/pull/2743))
    - update Rosetta easyblock to take into account that
        `$LD_LIBRARY_PATH`, `$CPATH`, `$PATH` may not be defined
        ([#2744](https://github.com/easybuilders/easybuild-easyblocks/pull/2744))
    - only load temporary module file during sanity check for pybind11
        for stand-alone installations, so it can be installed as
        extension
        ([#2747](https://github.com/easybuilders/easybuild-easyblocks/pull/2747))
    - make sure that `CMakeMakeCp` uses correct build dir
        ([#2748](https://github.com/easybuilders/easybuild-easyblocks/pull/2748))
    - enhance Bazel easyblock to avoid writing to `$HOME` in sanity
        check
        ([#2756](https://github.com/easybuilders/easybuild-easyblocks/pull/2756))

**easyconfigs**

- added easyconfigs for `foss/2022a`, `intel/2022a` common toolchains
    ([#15755](https://github.com/easybuilders/easybuild-easyconfigs/pull/15755))

    - see also
        <https://docs.easybuild.io/en/latest/Common-toolchains.html>

- add easyconfig for `gfbf/2022a` toolchain
    ([#15653](https://github.com/easybuilders/easybuild-easyconfigs/pull/15653),
    [#15755](https://github.com/easybuilders/easybuild-easyconfigs/pull/15755))

- added example easyconfig files for 24 new software packages:

    - BLT
        ([#15624](https://github.com/easybuilders/easybuild-easyconfigs/pull/15624)),
        category_encoders
        ([#15638](https://github.com/easybuilders/easybuild-easyconfigs/pull/15638)),
        fio
        ([#10321](https://github.com/easybuilders/easybuild-easyconfigs/pull/10321)),
        FSON
        ([#15721](https://github.com/easybuilders/easybuild-easyconfigs/pull/15721)),
        G-PhoCS
        ([#7619](https://github.com/easybuilders/easybuild-easyconfigs/pull/7619)),
        GCTA
        ([#15649](https://github.com/easybuilders/easybuild-easyconfigs/pull/15649)),
        Gibbs2
        ([#15702](https://github.com/easybuilders/easybuild-easyconfigs/pull/15702)),
        InterProScan_data
        ([#15717](https://github.com/easybuilders/easybuild-easyconfigs/pull/15717)),
        Jorg
        ([#15346](https://github.com/easybuilders/easybuild-easyconfigs/pull/15346)),
        libopus
        ([#15682](https://github.com/easybuilders/easybuild-easyconfigs/pull/15682)),
        Minipolish
        ([#15713](https://github.com/easybuilders/easybuild-easyconfigs/pull/15713)),
        mm-common
        ([#15764](https://github.com/easybuilders/easybuild-easyconfigs/pull/15764)),
        MONA
        ([#15696](https://github.com/easybuilders/easybuild-easyconfigs/pull/15696)),
        NetPyNE
        ([#15606](https://github.com/easybuilders/easybuild-easyconfigs/pull/15606)),
        pfind
        ([#15685](https://github.com/easybuilders/easybuild-easyconfigs/pull/15685)),
        regionmask
        ([#15786](https://github.com/easybuilders/easybuild-easyconfigs/pull/15786)),
        samplot
        ([#15686](https://github.com/easybuilders/easybuild-easyconfigs/pull/15686)),
        SISSO
        ([#15766](https://github.com/easybuilders/easybuild-easyconfigs/pull/15766)),
        sklearn-pandas
        ([#15637](https://github.com/easybuilders/easybuild-easyconfigs/pull/15637)),
        STAR-CCM+
        ([#7398](https://github.com/easybuilders/easybuild-easyconfigs/pull/7398)),
        SWIPE
        ([#6795](https://github.com/easybuilders/easybuild-easyconfigs/pull/6795)),
        topaz
        ([#15739](https://github.com/easybuilders/easybuild-easyconfigs/pull/15739)),
        uncertainty-calibration
        ([#15612](https://github.com/easybuilders/easybuild-easyconfigs/pull/15612)),
        Virtuoso-opensource
        ([#14102](https://github.com/easybuilders/easybuild-easyconfigs/pull/14102))

- added additional easyconfigs for various supported software
    packages, including:

    - AlphaFold 2.2.2, Arriba 2.3.0, Arrow 8.0.0, Bracken 2.7,
        CellRanger 7.0.0, Clp 1.17.7, CoinUtils 2.11.6, cppy 1.2.1,
        deal.II 9.3.3, double-conversion 3.2.0, Doxygen 1.9.4, FLAC
        1.3.4, fmt 7.1.1, FSL 6.0.5.1, GDAL 3.5.0, gdbm 1.21, geopandas
        0.11.0, GEOS 3.10.3, Ghostscript 9.56.1, GLibmm 2.66.4, Groovy
        4.0.3, GULP 6.1, h5py 3.7.0, HDF5 1.13.1, hifiasm 0.16.1,
        IGMPlot 2.6.9b, ImageMagick 7.1.0-37, InterProScan 5.55-88.0,
        IRkernel 1.3, jemalloc 5.3.0, JsonCpp 1.9.5, Julia 1.7.3,
        Leptonica 1.82.0, libgeotiff 1.7.1, libgit2 1.4.3, libiconv
        1.17, libRmath 4.2.0, libsigc++ 2.10.8, libsndfile 1.1.0, libxc
        5.2.3, libxml++ 2.42.1, line_profiler 3.5.1, LittleCMS 2.13.1,
        MaSuRCA 4.0.9, mayavi 4.7.4, MetaEuk 5, mold 1.3.0, NCCL
        2.12.12, netCDF 4.9.0, nettle 3.8, networkx 2.8.4, NEURON 7.8.2,
        NLopt 2.7.1, nodejs 16.15.1, NSPR 4.34, NSS 3.79, nsync 1.25.0,
        nvtop 2.0.2, Osi 0.108.7, p4est 2.8, parasail 2.5, Pillow 9.1.1,
        PLUMED 2.8.0, PnetCDF 1.12.3, PRISMS-PF 2.2, PROJ 9.0.0,
        protobuf 3.19.4, protobuf-python 3.19.4, pyfaidx 0.7.0, PyOpenGL
        3.1.6, pyproj 3.3.1, PyTorch 1.11.0, Qhull 2020.2, Qt5 5.15.5,
        QuantumESPRESSO 7.1, Qwt 6.2.0, R 4.2.1, rasterio 1.2.10,
        Ray-project 1.13.0, RE2 2022-06-01, redis-py 4.3.3, ReFrame
        3.11.2, rioxarray 0.11.1, RNA-SeQC 2.4.2, Schrodinger 2022-2,
        Shapely 1.8.2, Siesta 4.1.5, SimpleITK 2.1.1.2, SpectrA 1.0.1,
        TensorFlow 2.7.1, Tk 8.6.12, Tkinter 3.10.4, Transformers
        4.20.1, UCX-CUDA 1.12.1, utf8proc 2.7.0, WhatsHap 1.4, WPS
        3.9.1, Xvfb 21.1.3

- minor enhancements, including:

    - add extensions to R v4.2.0: hypergeo
        ([#15701](https://github.com/easybuilders/easybuild-easyconfigs/pull/15701)),
        rtdists
        ([#15734](https://github.com/easybuilders/easybuild-easyconfigs/pull/15734)),
        geeM
        ([#15810](https://github.com/easybuilders/easybuild-easyconfigs/pull/15810))
    - add patch for GCCcore 11.3.0 to support using `-fuse-ld=mold`
        ([#15715](https://github.com/easybuilders/easybuild-easyconfigs/pull/15715))
    - add patch for porefoam to fix hardcoded `mpirun` command and
        take into account `$POREFOAM_MPIRUN_CMD`
        ([#15730](https://github.com/easybuilders/easybuild-easyconfigs/pull/15730))

- various bug fixes, including:

    - switch to Rust 1.60.0 build dependency for bamtofastq, since
        build fails with Rust 1.52.1
        ([#15636](https://github.com/easybuilders/easybuild-easyconfigs/pull/15636))
    - avoid that pygmo v2.18.0 installs stuff in Python installation
        directory + add custom sanity check paths to pygmo easyconfigs
        ([#15657](https://github.com/easybuilders/easybuild-easyconfigs/pull/15657))
    - add patch for Mmg v5.6.0 to remove library CI tests that point
        to external sources
        ([#15691](https://github.com/easybuilders/easybuild-easyconfigs/pull/15691))
    - correct configopts in deal.II v9.1.1 easyconfig
        ([#15692](https://github.com/easybuilders/easybuild-easyconfigs/pull/15692))
    - add missing Python dependency for HPDBSCAN to fix unresolved
        `%(pyshortver)s` template
        ([#15694](https://github.com/easybuilders/easybuild-easyconfigs/pull/15694))

- other changes:

    - disable flaky GPU test for TensorFlow 2.6.0
        ([#15824](https://github.com/easybuilders/easybuild-easyconfigs/pull/15824))

## EasyBuild v4.5.5 (June 8th 2022) {: #release_notes_eb455 }

bugfix/update release

**framework**

- various enhancements, including:
    - add toolchain definitions for `nvompi` (NVHPC + OpenMPI)
        ([#3969](https://github.com/easybuilders/easybuild-framework/pull/3969)),
        `nvpsmpi` (NVHPC + ParaStationMPI)
        ([#3970](https://github.com/easybuilders/easybuild-framework/pull/3970)),
        `gfbf` (GCC, FlexiBLAS, FFTW)
        ([#4006](https://github.com/easybuilders/easybuild-framework/pull/4006))
    - add support for `FFTW.MPI` toolchain component (`$FFT*DIR`
        variables)
        ([#4012](https://github.com/easybuilders/easybuild-framework/pull/4012))
    - add support for customizing EasyBuild command used in jobs via
        `--job-eb-cmd`
        ([#4016](https://github.com/easybuilders/easybuild-framework/pull/4016))
- various bug fixes, including:
    - fix copying of easyconfig file with `--copy-ec` without
        `--rebuild` if module is already installed
        ([#3993](https://github.com/easybuilders/easybuild-framework/pull/3993))
    - ignore deprecation warnings regarding cryptography in Python
        3.6 + Blowfish with Python 3.10 in test suite output
        ([#3999](https://github.com/easybuilders/easybuild-framework/pull/3999))
    - fix typo in debug log message in `easyblock.py`
        ([#4000](https://github.com/easybuilders/easybuild-framework/pull/4000))
    - fix printing of list of attempted download URLs when url-encoded
        characters are used in URL
        ([#4005](https://github.com/easybuilders/easybuild-framework/pull/4005))
    - set `$FFT(W)_LIB_DIR` to imkl-FFTW's lib path in build
        environment if usempi toolchain option is enabled
        ([#4011](https://github.com/easybuilders/easybuild-framework/pull/4011))
    - correctly identify Apple Silicon M1 as Arm 64-bit by also
        considering arm64 next to aarch64
        ([#4014](https://github.com/easybuilders/easybuild-framework/pull/4014))
    - fix '`eb --show-system-info`' on Apple M1 system
        ([#4015](https://github.com/easybuilders/easybuild-framework/pull/4015))
- other changes:
    - change '`eb`' command to `import easybuild.framework` to check
        if EasyBuild framework is available
        ([#3995](https://github.com/easybuilders/easybuild-framework/pull/3995),
        [#3998](https://github.com/easybuilders/easybuild-framework/pull/3998))

**easyblocks**

- new software-specific easyblock for FFTW.MPI
    ([#2724](https://github.com/easybuilders/easybuild-easyblocks/pull/2724))
- minor enhancements and updates, including:
    - update NEURON easyblock to use CMakeMake for recent versions
        ([#2304](https://github.com/easybuilders/easybuild-easyblocks/pull/2304))
    - enhance Clang easyblock to add support for building with AMDGPU
        offload
        ([#2684](https://github.com/easybuilders/easybuild-easyblocks/pull/2684),
        [#2729](https://github.com/easybuilders/easybuild-easyblocks/pull/2729))
    - update sanity check in OpenMPI easyblock to support OpenMPI
        v5.0.0
        ([#2709](https://github.com/easybuilders/easybuild-easyblocks/pull/2709))
    - don't use `gold` linker by default for GCC >= 11.3
        ([#2711](https://github.com/easybuilders/easybuild-easyblocks/pull/2711))
    - update sanity check in R easyblock for versions >= 4.2.0, since
        S.h is not included anymore
        ([#2713](https://github.com/easybuilders/easybuild-easyblocks/pull/2713))
    - update ABAQUS easyblock for ABAQUS 2022
        ([#2716](https://github.com/easybuilders/easybuild-easyblocks/pull/2716))
    - update LLVM easyblock for LLVM v14.0.x
        ([#2718](https://github.com/easybuilders/easybuild-easyblocks/pull/2718))
    - update Mesa easyblock to remove swr driver configopts for
        versions 22+
        ([#2719](https://github.com/easybuilders/easybuild-easyblocks/pull/2719))
    - enhance Clang easyblock to support also installing Python
        bindings
        ([#2721](https://github.com/easybuilders/easybuild-easyblocks/pull/2721),
        [#2725](https://github.com/easybuilders/easybuild-easyblocks/pull/2725))
    - enhance SuperLU easyblock to support building on top of
        FlexiBLAS and be compatible with SuperLU v5.3
        ([#2722](https://github.com/easybuilders/easybuild-easyblocks/pull/2722))
    - update TensorFlow easyblock for version 2.8.0
        ([#2723](https://github.com/easybuilders/easybuild-easyblocks/pull/2723))
    - modify FFTW's sanity check step to allow checking only for MPI
        parts of FFTW installation
        ([#2724](https://github.com/easybuilders/easybuild-easyblocks/pull/2724))
    - add support to ConfigureMake for tweaking (first part of) test
        command via '`test_cmd`'
        ([#2726](https://github.com/easybuilders/easybuild-easyblocks/pull/2726),
        [#2737](https://github.com/easybuilders/easybuild-easyblocks/pull/2737))
    - enhance MrBayes easyblock with custom sanity check command
        ([#2727](https://github.com/easybuilders/easybuild-easyblocks/pull/2727))
    - update cudnnarch string templates used to compose source tarball
        names from cuDNN 8.3.3 onwards
        ([#2728](https://github.com/easybuilders/easybuild-easyblocks/pull/2728))
    - add sanity check command to OpenSSL wrapper easyblock to verify
        that system certificates are available to OpenSSL
        ([#2735](https://github.com/easybuilders/easybuild-easyblocks/pull/2735))
    - ignore exit code of `pkg-config` command in OpenSSL wrapper
        easyblock, since with `pkgconf` they exit with a non-zero exit
        code if the OS package is not installed
        ([#2736](https://github.com/easybuilders/easybuild-easyblocks/pull/2736))
- various bug fixes, including:
    - remove system-compiled binutils dirs from `$LDFLAGS` in binutils
        easyblock
        ([#2712](https://github.com/easybuilders/easybuild-easyblocks/pull/2712))
    - fix for FreeSurfer easyblock: define `$FREESURFER` needed by
        recon_all
        ([#2717](https://github.com/easybuilders/easybuild-easyblocks/pull/2717))
    - also symlink `cert.pem` in from-source OpenSSL installation (if
        it exists)
        ([#2735](https://github.com/easybuilders/easybuild-easyblocks/pull/2735))

**easyconfigs**

- add candidates for 2022a common toolchains: `foss/2022.05`
    ([#15561](https://github.com/easybuilders/easybuild-easyconfigs/pull/15561)),
    intel/2022.05
    ([#15485](https://github.com/easybuilders/easybuild-easyconfigs/pull/15485))
- added example easyconfig files for 35 new software packages:
    - Albumentations
        ([#15302](https://github.com/easybuilders/easybuild-easyconfigs/pull/15302)),
        AMPtk
        ([#15435](https://github.com/easybuilders/easybuild-easyconfigs/pull/15435)),
        arosics
        ([#15249](https://github.com/easybuilders/easybuild-easyconfigs/pull/15249)),
        CellTypist
        ([#15530](https://github.com/easybuilders/easybuild-easyconfigs/pull/15530)),
        detectron2
        ([#15442](https://github.com/easybuilders/easybuild-easyconfigs/pull/15442)),
        EigenExa
        ([#15234](https://github.com/easybuilders/easybuild-easyconfigs/pull/15234)),
        Fastaq
        ([#15332](https://github.com/easybuilders/easybuild-easyconfigs/pull/15332)),
        FFTW.MPI
        ([#15561](https://github.com/easybuilders/easybuild-easyconfigs/pull/15561)),
        FreeBarcodes
        ([#15350](https://github.com/easybuilders/easybuild-easyconfigs/pull/15350)),
        gcloud
        ([#15443](https://github.com/easybuilders/easybuild-easyconfigs/pull/15443)),
        GST-plugins-bad
        ([#15446](https://github.com/easybuilders/easybuild-easyconfigs/pull/15446)),
        gsutil
        ([#15507](https://github.com/easybuilders/easybuild-easyconfigs/pull/15507)),
        GTK4
        ([#15447](https://github.com/easybuilders/easybuild-easyconfigs/pull/15447)),
        hector
        ([#15397](https://github.com/easybuilders/easybuild-easyconfigs/pull/15397)),
        i7z
        ([#15236](https://github.com/easybuilders/easybuild-easyconfigs/pull/15236)),
        libde265
        ([#15395](https://github.com/easybuilders/easybuild-easyconfigs/pull/15395)),
        libheif
        ([#15395](https://github.com/easybuilders/easybuild-easyconfigs/pull/15395)),
        ModelTest-NG
        ([#15448](https://github.com/easybuilders/easybuild-easyconfigs/pull/15448)),
        num2words
        ([#15473](https://github.com/easybuilders/easybuild-easyconfigs/pull/15473)),
        OGDF
        ([#15407](https://github.com/easybuilders/easybuild-easyconfigs/pull/15407)),
        panito
        ([#15314](https://github.com/easybuilders/easybuild-easyconfigs/pull/15314)),
        parameterized
        ([#15481](https://github.com/easybuilders/easybuild-easyconfigs/pull/15481)),
        purge_dups
        ([#15385](https://github.com/easybuilders/easybuild-easyconfigs/pull/15385)),
        redis-py
        ([#15475](https://github.com/easybuilders/easybuild-easyconfigs/pull/15475)),
        ruamel.yaml
        ([#15531](https://github.com/easybuilders/easybuild-easyconfigs/pull/15531)),
        SCGid
        ([#15065](https://github.com/easybuilders/easybuild-easyconfigs/pull/15065)),
        scPred
        ([#15575](https://github.com/easybuilders/easybuild-easyconfigs/pull/15575)),
        slow5tools
        ([#15457](https://github.com/easybuilders/easybuild-easyconfigs/pull/15457)),
        smooth-topk
        ([#15506](https://github.com/easybuilders/easybuild-easyconfigs/pull/15506)),
        SPOTPY
        ([#15326](https://github.com/easybuilders/easybuild-easyconfigs/pull/15326)),
        tmap
        ([#14601](https://github.com/easybuilders/easybuild-easyconfigs/pull/14601)),
        UCC
        ([#14291](https://github.com/easybuilders/easybuild-easyconfigs/pull/14291)),
        Wayland
        ([#11107](https://github.com/easybuilders/easybuild-easyconfigs/pull/11107)),
        XGrafix
        ([#15268](https://github.com/easybuilders/easybuild-easyconfigs/pull/15268)),
        XPLOR-NIH
        ([#15479](https://github.com/easybuilders/easybuild-easyconfigs/pull/15479))
- added additional easyconfigs for various supported software
    packages, including:
    - ABAQUS 2022, Arb 2.22.1, ARGoS 3.0.0, Arriba 2.2.1, astropy
        5.0.4, ATK 2.38.0, Autotools 20220317, Bader 1.04, Bazel 4.2.2 +
        5.1.1, BDBag 1.6.3, binutils 2.38, biom-format 2.1.12, BLIS
        0.9.0, Boost 1.79.0, breseq 0.36.1, bx-python 0.8.13, cairo
        1.17.4, CellRanger-ARC 2.0.1, CMake 3.23.1, cryoDRGN 1.0.0, CUDA
        11.7.0, cuDNN 8.4.1.50, cURL 7.83.0, DBus 1.14.0, eggnog-mapper
        2.1.7, elfutils 0.187, EvidentialGene 2022.01.14, expat 2.4.8,
        FlexiBLAS 3.2.0, FLINT 2.8.4, fontconfig 2.14.0, freebayes
        1.3.6, freeglut 3.2.2, freetype 2.12.1, FriBidi 1.0.12, GCC
        9.5.0 + 11.3.0 + GCC 12.1.0, Gdk-Pixbuf 2.42.8, geopandas
        0.10.2, git 2.36.0, GLib 2.72.1, GMAP-GSNAP 2021-21-17, Go
        1.18.1, GObject-Introspection 1.72.0, Graphene 1.10.8,
        GST-plugins-base 1.20.2, GStreamer 1.20.2, GTDB-Tk 2.0.0, GTK3
        3.24.33, gzip 1.12, HarfBuzz 4.2.1, help2man 1.49.2, hwloc
        2.7.1, hypothesis 6.46.7, Hypre 2.24.0, ICU 71.1, IGV 2.12.3,
        IMB 2021.3, inferCNV 1.10.1, InterProScan 5.52, IQ-TREE 2.2.1,
        jax 0.3.9, json-c 0.16, LAPACK 3.10.1, libarchive 3.6.1,
        libdeflate 1.10, libdrm 2.4.110, libedit 20210910, libepoxy
        1.5.10, libfabric 1.15.1, libglvnd 1.4.0, libjpeg-turbo 2.1.3,
        libreadline 8.1.2, librsb 1.3.0.1, librsvg 2.52.8, libtool
        2.4.7, libunwind 1.6.2, libxml2 2.9.13, LLVM 14.0.3, LocARNA
        1.9.2.3, MACS2 2.2.7.1, magma 2.6.2, Mako 1.2.0, Mathematica
        13.0.0, MCL 14.137, MCR R2022a.1, Mesa 22.0.3, Meson 0.62.1,
        MIRA 5.0rc2, Mmg 5.6.0, mold 1.2.1, mosdepth 0.3.3, MrBayes
        3.2.7a, MultiQC 1.12, MUMPS 5.5.0, muParser 2.3.3, ncurses 6.3,
        neptune-client 0.16.2, Nextflow 22.04.0, Nim 1.6.6, NTPoly
        2.7.1, OpenMPI 4.1.4, openpyxl 3.0.9, OpenSSL 1.1.1n,
        OpenStackClient 5.8.0, OSU-Micro-Benchmarks 5.9, pagmo 2.18.0,
        Pango 1.50.7, parallel-fastq-dump 0.6.7, PCRE2 10.40, Perl
        5.34.1, Pillow 9.1.0, PLINK 2.00a3.1, PMIx 4.1.2, PyAMG 4.2.3,
        pybind11 2.9.2, PyCairo 1.21.0, pygmo 2.18.0, PyGObject 3.42.1,
        Python 3.10.4, R 4.2.0, RAxML-NG 1.1.0, R-bundle-Bioconductor
        3.15, ReFrame 3.11.0, RNA-Bloom 1.4.3, rnaQUAST 2.2.2, Rust
        1.60.0, Sambamba 0.8.2, SAMtools 1.15.1, ScaLAPACK 2.2.0,
        SciPy-bundle 2022.05, SeqKit 2.2.0, Shapely 1.8.1.post1,
        SpaceRanger 1.3.1, Spack 0.17.2, Spark 3.2.1, SQLite 3.38.3,
        StringTie 2.2.1, SUMO 1.12.0, SuperLU 5.3.0, tbl2asn 20220427,
        Tcl 8.6.12, TCLAP 1.2.5, tcsh 6.24.01, texlive 20220321, ToFu
        1.5.0, UCX 1.12.1, util-linux 2.38, VEP 105, ViennaRNA 2.5.0,
        vsc-mympirun 5.2.11, worker 1.6.13, X11 2022050, YAXT 0.9.2.1,
        Z3 4.8.16, Zip 3.0, zlib 1.2.12, zstd 1.5.2
- minor enhancements, including:
    - use OpenSSL wrapper dependency for CMake 3.18.4 with system
        toolchain
        ([#15227](https://github.com/easybuilders/easybuild-easyconfigs/pull/15227))
    - also build BLIS backend for FlexiBLAS v3.0.4 with GCC/10.3.0
        ([#15347](https://github.com/easybuilders/easybuild-easyconfigs/pull/15347))
    - add extensions to R v4.1.2 + v4.2.0 easyconfigs:
        - Hmsc
            ([#15393](https://github.com/easybuilders/easybuild-easyconfigs/pull/15393)),
            MonteCarlo + RhpcBLASctl
            ([#15438](https://github.com/easybuilders/easybuild-easyconfigs/pull/15438)),
            chkptstanr
            ([#15540](https://github.com/easybuilders/easybuild-easyconfigs/pull/15540)),
            chkptstanr + MLmetrics + renv
            ([#15573](https://github.com/easybuilders/easybuild-easyconfigs/pull/15573))
    - add extensions to R-bundle-Bioconductor 3.14 easyconfig:
        DNABarcodes
        ([#15405](https://github.com/easybuilders/easybuild-easyconfigs/pull/15405))
    - use redist source_urls for cuDNN > 7.5
        ([#15411](https://github.com/easybuilders/easybuild-easyconfigs/pull/15411))
    - add download_instructions to Java 1.8 > 200
        ([#15412](https://github.com/easybuilders/easybuild-easyconfigs/pull/15412))
    - update Arrow to use EB versions of some dependencies and enable
        all compression codecs
        ([#15512](https://github.com/easybuilders/easybuild-easyconfigs/pull/15512))
    - add csh -> tcsh symlink in recent tcsh easyconfigs
        ([#15571](https://github.com/easybuilders/easybuild-easyconfigs/pull/15571))
    - allow external tools to be located elsewhere for ETE
        ([#15578](https://github.com/easybuilders/easybuild-easyconfigs/pull/15578))
    - add additional sanity check commands for IQ-TREE v2.2.1
        ([#15596](https://github.com/easybuilders/easybuild-easyconfigs/pull/15596))
- various bug fixes, including:
    - fix source URL for freetype 2.6.5 with `foss/2016b`
        ([#14204](https://github.com/easybuilders/easybuild-easyconfigs/pull/14204))
    - fix installation of easybuild-easyconfigs with setuptools>=61
        by explicitly declaring there are no Python packages
        ([#15206](https://github.com/easybuilders/easybuild-easyconfigs/pull/15206))
    - use x.py to bootstrap Rust so that build options are properly
        passed through
        ([#15211](https://github.com/easybuilders/easybuild-easyconfigs/pull/15211))
    - fix RepeatMasker-4.1.2-p1 easyconfig by moving the database
        configure command to postinstallcmds
        ([#15280](https://github.com/easybuilders/easybuild-easyconfigs/pull/15280),
        [#15615](https://github.com/easybuilders/easybuild-easyconfigs/pull/15615))
    - add hwloc dependency to tbb v2021.4.0
        ([#15294](https://github.com/easybuilders/easybuild-easyconfigs/pull/15294))
    - tweak find command used in preconfigopts in easyconfig for
        pkg-config v0.29.2 with system toolchain to avoid descending
        into other filesystems
        ([#15313](https://github.com/easybuilders/easybuild-easyconfigs/pull/15313))
    - remove pkg-config use from SeqLib configure patch (avoids
        problem due to faulty autoconf macro)
        ([#15316](https://github.com/easybuilders/easybuild-easyconfigs/pull/15316))
    - update source URL for isl in GCCcore easyconfigs
        ([#15320](https://github.com/easybuilders/easybuild-easyconfigs/pull/15320))
    - update source URLs for YAXT 0.9.x to fix download
        ([#15323](https://github.com/easybuilders/easybuild-easyconfigs/pull/15323))
    - define `$HHLIB` as path to HH-suite installation directory,
        required by Perl scripts
        ([#15324](https://github.com/easybuilders/easybuild-easyconfigs/pull/15324))
    - add missing parallel and tbl2asn dependencies for prokka 1.14.5
        ([#15360](https://github.com/easybuilders/easybuild-easyconfigs/pull/15360),
        [#15381](https://github.com/easybuilders/easybuild-easyconfigs/pull/15381))
    - add missing dependencies for libheif (libpng, libjpeg-turbo)
        ([#15408](https://github.com/easybuilders/easybuild-easyconfigs/pull/15408))
    - switch to configuring build of libheif with CMake so libde265
        dependency is picked up
        ([#15408](https://github.com/easybuilders/easybuild-easyconfigs/pull/15408))
    - disable use of `-ftree-vectorize` for OpenFOAM v2112 with
        `foss/2021b`
        ([#15495](https://github.com/easybuilders/easybuild-easyconfigs/pull/15495))
    - add patch for OpenMPI 4.1.1 to support building using
        `--with-cuda=internal`
        ([#15528](https://github.com/easybuilders/easybuild-easyconfigs/pull/15528),
        [#15589](https://github.com/easybuilders/easybuild-easyconfigs/pull/15589))
    - add patch to fix support for external PMIx v3.1 in OpenMPI
        v3.1.3
        ([#15566](https://github.com/easybuilders/easybuild-easyconfigs/pull/15566))
    - also build shared library + fix `$PYTHONPATH` for gmsh 4.9.0
        ([#15579](https://github.com/easybuilders/easybuild-easyconfigs/pull/15579))
    - add patch for GLib 2.68.2 to fix use of close_range
        ([#15594](https://github.com/easybuilders/easybuild-easyconfigs/pull/15594))
    - fix download of thrift 0.12.0 for Arrow 0.16.0
        ([#15597](https://github.com/easybuilders/easybuild-easyconfigs/pull/15597))
    - add Bison and flex build dependencies to SCOTCH 6.1.x
        ([#15618](https://github.com/easybuilders/easybuild-easyconfigs/pull/15618))
    - add alternative checksums for class, nnet, spatial extensions in
        R v4.2.0 easyconfig
        ([#15619](https://github.com/easybuilders/easybuild-easyconfigs/pull/15619))
    - add missing dependencies + switch to non-static build for Arriba
        v2.1.0
        ([#15623](https://github.com/easybuilders/easybuild-easyconfigs/pull/15623))
- other changes:
    - add R dependency to vcflib 1.0.3, and move from GCC/11.2.0 to
        `foss/2021b` toochain
        ([#15216](https://github.com/easybuilders/easybuild-easyconfigs/pull/15216))
    - update fallback version for OpenSSL 1.1 wrapper to v1.1.1o
        ([#15592](https://github.com/easybuilders/easybuild-easyconfigs/pull/15592))
    - install sklearn meta-package with scikit-learn v1.0.1
        ([#15613](https://github.com/easybuilders/easybuild-easyconfigs/pull/15613))
    - switch from `pkg-config` to `pkgconf` as build dependency for
        OpenSSL wrapper easyconfigs
        ([#15616](https://github.com/easybuilders/easybuild-easyconfigs/pull/15616),
        [#15617](https://github.com/easybuilders/easybuild-easyconfigs/pull/15617))

## EasyBuild v4.5.4 (March 31st 2022) {: #release_notes_eb454 }

bugfix/update release

**framework**

- various enhancements, including:
    - warn about potentially missing patches in `--new-pr`
        ([#3759](https://github.com/easybuilders/easybuild-framework/pull/3759),
        [#3966](https://github.com/easybuilders/easybuild-framework/pull/3966))
    - add support for '`clone_into`' field in git_config source spec
        to specify different name for top-level directory
        ([#3949](https://github.com/easybuilders/easybuild-framework/pull/3949))
    - add bash completion for easyconfigs from local dir but not robot
        search path
        ([#3953](https://github.com/easybuilders/easybuild-framework/pull/3953))
    - add a 'sync pr' message when the PR has a mergeable state but
        is showing a failed status for the test suite on the last commit
        ([#3967](https://github.com/easybuilders/easybuild-framework/pull/3967))
    - add `gmpit` toolchain definition (GCC + MPItrampoline)
        ([#3971](https://github.com/easybuilders/easybuild-framework/pull/3971))
    - use '`zypper search -i`' to check whether specified OS
        dependency is installed on openSUSE + make sure that rpm is
        considered for checking OS dependencies on RHEL8
        ([#3973](https://github.com/easybuilders/easybuild-framework/pull/3973))
    - add support for post-install patches
        ([#3974](https://github.com/easybuilders/easybuild-framework/pull/3974))
    - add support for '`download_instructions`' easyconfig parameter
        key to specify some download or installation steps for user in
        case of complicated way of obtaining needed files
        ([#3976](https://github.com/easybuilders/easybuild-framework/pull/3976),
        [#3981](https://github.com/easybuilders/easybuild-framework/pull/3981))
    - also try collecting AMD GPU info (via `rocm-smi`) for
        `--show-system-info`
        ([#3978](https://github.com/easybuilders/easybuild-framework/pull/3978),
        [#3982](https://github.com/easybuilders/easybuild-framework/pull/3982))
- various bug fixes, including:
    - ensure `--review-pr` can find dependencies included in PR
        ([#3979](https://github.com/easybuilders/easybuild-framework/pull/3979))
    - run '`apt-get update`' in GitHub Actions workflow for
        container tests to update container package list before
        installing anything
        ([#3985](https://github.com/easybuilders/easybuild-framework/pull/3985))
- other changes:
    - enable code linting check for all supported Python versions
        ([#3725](https://github.com/easybuilders/easybuild-framework/pull/3725))
    - update copyright lines for 2022
        ([#3986](https://github.com/easybuilders/easybuild-framework/pull/3986))

**easyblocks**

- minor enhancements and updates, including:
    - update Clang-AOMP easyblock to add support for ROCm v5.0
        ([#2681](https://github.com/easybuilders/easybuild-easyblocks/pull/2681))
    - enable system SSL certificates in OpenSSL installations
        ([#2683](https://github.com/easybuilders/easybuild-easyblocks/pull/2683))
    - enhance MRtrix easyblock: build in parallel + enable OpenMP
        support for MRtrix >= 3.0
        ([#2685](https://github.com/easybuilders/easybuild-easyblocks/pull/2685))
    - avoid dependency on '`which`' command in sanity check for
        Python, use '`command -v`' instead
        ([#2687](https://github.com/easybuilders/easybuild-easyblocks/pull/2687))
    - enhance Tarball easyblock to support using it for installing
        extensions
        ([#2688](https://github.com/easybuilders/easybuild-easyblocks/pull/2688))
    - update wxPython easyblock to support wxPython v4.1
        ([#2689](https://github.com/easybuilders/easybuild-easyblocks/pull/2689))
    - enhance Gurobi easyblock to also update `$MATLABPATH`
        ([#2691](https://github.com/easybuilders/easybuild-easyblocks/pull/2691))
    - build single-file shared libraries for imkl so it can be used as
        FlexiBLAS backend via `$FLEXIBLAS_LIBRARY_PATH`
        ([#2694](https://github.com/easybuilders/easybuild-easyblocks/pull/2694))
- various bug fixes, including:
    - added regex to replace /lib/cpp with cpp in OpenFOAM's wmake
        rules file
        ([#2331](https://github.com/easybuilders/easybuild-easyblocks/pull/2331))
    - set `$NINJAFLAGS` to make sure Ninja doesn't use all visible
        cores when building Qt5
        ([#2338](https://github.com/easybuilders/easybuild-easyblocks/pull/2338))
    - update Siesta EasyBlock to use serial FFTW
        ([#2662](https://github.com/easybuilders/easybuild-easyblocks/pull/2662))
    - fix support for imkl for numexpr 2.8.0+ in numexpr easyblock
        ([#2678](https://github.com/easybuilders/easybuild-easyblocks/pull/2678))
    - make sure TensorFlow doesn't see the `nvptx-none` dir when
        searching for `gcc` include dir
        ([#2682](https://github.com/easybuilders/easybuild-easyblocks/pull/2682))
    - force use of bash for Anaconda install script
        ([#2692](https://github.com/easybuilders/easybuild-easyblocks/pull/2692))
    - add guess for path to add to `$MANPATH` for intel-compilers
        ([#2696](https://github.com/easybuilders/easybuild-easyblocks/pull/2696))
    - change permissions of the Java build directory to avoid
        permission denied error
        ([#2698](https://github.com/easybuilders/easybuild-easyblocks/pull/2698))
    - also consider `$MKLROOT/lib/pkgconfig` for `$PKG_CONFIG_PATH`
        for imkl
        ([#2701](https://github.com/easybuilders/easybuild-easyblocks/pull/2701))
    - close log after installing Bundle component
        ([#2702](https://github.com/easybuilders/easybuild-easyblocks/pull/2702))
        - fixes problem of log leaking across installations
            ([framework issue
            #3533](https://github.com/easybuilders/easybuild-framework/issues/3533))
    - replace hardcoded /tmp to make sure that Bazel build respects
        `$TMPDIR`
        ([#2703](https://github.com/easybuilders/easybuild-easyblocks/pull/2703))
- other changes:
    - minor code cleanup in numexpr easyblock
        ([#2679](https://github.com/easybuilders/easybuild-easyblocks/pull/2679))
    - update copyright lines for 2022
        ([#2705](https://github.com/easybuilders/easybuild-easyblocks/pull/2705))

**easyconfigs**

- added example easyconfig files for 29 new software packages:
    - Abseil
        ([#15102](https://github.com/easybuilders/easybuild-easyconfigs/pull/15102)),
        AMS
        ([#13155](https://github.com/easybuilders/easybuild-easyconfigs/pull/13155)),
        ArchR
        ([#15119](https://github.com/easybuilders/easybuild-easyconfigs/pull/15119)),
        CMAverse
        ([#14963](https://github.com/easybuilders/easybuild-easyconfigs/pull/14963)),
        CmdStanR
        ([#15198](https://github.com/easybuilders/easybuild-easyconfigs/pull/15198)),
        CONN
        ([#15052](https://github.com/easybuilders/easybuild-easyconfigs/pull/15052)),
        Devito
        ([#14984](https://github.com/easybuilders/easybuild-easyconfigs/pull/14984),
        [#15009](https://github.com/easybuilders/easybuild-easyconfigs/pull/15009)),
        GraphMap
        ([#10299](https://github.com/easybuilders/easybuild-easyconfigs/pull/10299)),
        gRPC
        ([#14728](https://github.com/easybuilders/easybuild-easyconfigs/pull/14728)),
        Hydra
        ([#15025](https://github.com/easybuilders/easybuild-easyconfigs/pull/15025)),
        jupyter-server-proxy
        ([#14844](https://github.com/easybuilders/easybuild-easyconfigs/pull/14844)),
        M1QN3
        ([#15002](https://github.com/easybuilders/easybuild-easyconfigs/pull/15002)),
        MAGeCK
        ([#15082](https://github.com/easybuilders/easybuild-easyconfigs/pull/15082)),
        matplotlib-inline
        ([#15084](https://github.com/easybuilders/easybuild-easyconfigs/pull/15084)),
        MEGAN
        ([#15064](https://github.com/easybuilders/easybuild-easyconfigs/pull/15064)),
        MNE-Python
        ([#15174](https://github.com/easybuilders/easybuild-easyconfigs/pull/15174)),
        ONNX
        ([#15158](https://github.com/easybuilders/easybuild-easyconfigs/pull/15158)),
        ONNX-Runtime
        ([#15158](https://github.com/easybuilders/easybuild-easyconfigs/pull/15158)),
        ont-remora
        ([#15162](https://github.com/easybuilders/easybuild-easyconfigs/pull/15162)),
        Optuna
        ([#15021](https://github.com/easybuilders/easybuild-easyconfigs/pull/15021)),
        patch
        ([#15035](https://github.com/easybuilders/easybuild-easyconfigs/pull/15035)),
        porefoam
        ([#15067](https://github.com/easybuilders/easybuild-easyconfigs/pull/15067)),
        presto
        ([#15119](https://github.com/easybuilders/easybuild-easyconfigs/pull/15119)),
        PyFrag
        ([#15184](https://github.com/easybuilders/easybuild-easyconfigs/pull/15184)),
        skorch
        ([#15175](https://github.com/easybuilders/easybuild-easyconfigs/pull/15175)),
        SlamDunk
        ([#15197](https://github.com/easybuilders/easybuild-easyconfigs/pull/15197)),
        SPM
        ([#15050](https://github.com/easybuilders/easybuild-easyconfigs/pull/15050)),
        STRique
        ([#14980](https://github.com/easybuilders/easybuild-easyconfigs/pull/14980)),
        XML-Compile
        ([#15177](https://github.com/easybuilders/easybuild-easyconfigs/pull/15177))
- added additional easyconfigs for various supported software
    packages, including:
    - ABAQUS 2021, AlphaFold 2.1.2, AmberTools 21, archspec 0.1.3,
        Bandage 0.9.0, BLIS 3.1, c-ares 1.18.1, CCL 1.12.1, CharLS
        2.3.4, Clang-Python-bindings 13.0.1, dcm2niix 1.0.20211006,
        DFTB+ 21.1, DIRAC 22.0, ELPA 2021.11.001, FlexiBLAS 3.1.3,
        FLUENT 2021R2, GATK 4.2.5.0, GetOrganelle 1.7.5.3, IgBLAST
        1.18.0, IntelClusterChecker 2021.5.0, intervaltree-python 3.1.0,
        ITSx 1.1.3, Julia 1.7.2, kallisto 0.48.0, KMC 3.2.1, libobjcryst
        2021.1.2, libtree 3.0.3, loompy 3.0.7, matplotlib 3.5.1, MCR
        R2022a, MDAnalysis 1.1.1+ 2.0.0, MDTraj 1.9.7, medaka 1.5.0,
        meshalyzer 20200308, MRtrix 3.0.3, NiBabel 3.2.2, NLTK 3.7,
        numexpr 2.8.1, ont-fast5-api 4.0.2, OpenAI-Gym 0.21.0, OpenBLAS
        0.3.20, ORCA 5.0.3, parallel-fastq-dump 0.6.6, PIPITS 2.8, pocl
        1.8, pycocotools 2.0.4, pyEGA3 4.0.0, pyobjcryst 2.2.1, RE2
        2022-02-01, SAMtools 1.15, SBCL 2.2.1, shovill 1.1.0, SKESA
        2.4.0, SOCI 4.0.3, sympy 1.9, TensorFlow 2.5.3, VirtualGL 3.0,
        vsc-mympirun 5.2.10, VSEARCH 2.21.1, VTK 9.1.0, VTune 2022.2.0,
        XGBoost 1.5.0
- minor enhancements, including:
    - add Flask-Session to Flask v1.1.4 and Flask v2.0.2
        ([#15027](https://github.com/easybuilders/easybuild-easyconfigs/pull/15027))
    - add check to verify that patch files touched in PRs have a
        description in place
        ([#15061](https://github.com/easybuilders/easybuild-easyconfigs/pull/15061))
    - add extensions to R v4.1.2 easyconfig: hash
        ([#15098](https://github.com/easybuilders/easybuild-easyconfigs/pull/15098)),
        nabor + harmony
        ([#15117](https://github.com/easybuilders/easybuild-easyconfigs/pull/15117)),
        apluster, DataCombine, docstring, gdalUtils, openair, mstate,
        SNFtool, and deps
        ([#15141](https://github.com/easybuilders/easybuild-easyconfigs/pull/15141))
    - also install rMATS_P commands in rMATS-turbo easyconfig
        ([#15113](https://github.com/easybuilders/easybuild-easyconfigs/pull/15113))
    - add extensions to Bioconductor v3.14 easyconfig: chromVAR
        ([#15118](https://github.com/easybuilders/easybuild-easyconfigs/pull/15118)),
        EnsDb.Hsapiens.v79
        ([#15154](https://github.com/easybuilders/easybuild-easyconfigs/pull/15154)),
        WGCNA
        ([#15178](https://github.com/easybuilders/easybuild-easyconfigs/pull/15178))
    - add extensions to Perl v5.34.0 easyconfigs: Sys::Info,
        HTML::Template, Log::Report
        ([#15176](https://github.com/easybuilders/easybuild-easyconfigs/pull/15176)),
        Sys::<Info::Driver>::Unknown, Sys::<Info::Driver>::Linux,
        Unix::Processors
        ([#15190](https://github.com/easybuilders/easybuild-easyconfigs/pull/15190))
    - enable running of tests for MEME with `gompi/2021b`
        ([#15191](https://github.com/easybuilders/easybuild-easyconfigs/pull/15191),
        [#15199](https://github.com/easybuilders/easybuild-easyconfigs/pull/15199))
- various bug fixes, including:
    - add missing xxd build dependency for recent PLUMED versions
        (2.6.2, 2.7.x)
        ([#14847](https://github.com/easybuilders/easybuild-easyconfigs/pull/14847))
    - downgrade dependency on nodejs + use jupyter-server-proxy in
        jupyter-matlab-proxy and configurable-http-proxy easyconfigs
        using `GCCcore/10.3.0` toolchain
        ([#14942](https://github.com/easybuilders/easybuild-easyconfigs/pull/14942))
    - add additional valid checksum for extensions in R 4.1.0 and
        4.1.2 easyconfigs: norm
        ([#14987](https://github.com/easybuilders/easybuild-easyconfigs/pull/14987)),
        optmatch
        ([#14993](https://github.com/easybuilders/easybuild-easyconfigs/pull/14993))
    - avoid pollution in the tmp directory when running the AlphaFold
        tests
        ([#14989](https://github.com/easybuilders/easybuild-easyconfigs/pull/14989))
    - consistently enable usempi toolchain option in
        OSU-Micro-Benchmarks easyconfigs
        ([#15039](https://github.com/easybuilders/easybuild-easyconfigs/pull/15039))
    - fix GBprocesS easyconfig by switching to source tarball created
        using `git_config`
        ([#15048](https://github.com/easybuilders/easybuild-easyconfigs/pull/15048))
