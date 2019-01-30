---
layout: page_project
title: HPC libraries for solving dense symmetric eigenvalue problems
date: 2016-03-23
updated:
navbar: Research
subnavbar: Projects
project_url:
status: running
topics:
  - numerics
keywords:
  - dense symmetric eigensolver
  - porting
  - performance evaluation
head: imamura_t
members:
  - gutheil_i
---

## Research topic and goals

Many applications for example in Density Functional Theory (DFT) used in physics, chemistry, and materials science have to compute eigenvalues and eigenvectors of dense symmetric matrices.
There are several libraries available for that task in high performance computing: ScaLAPACK, EigenExa, ELPA, and Elemental.
On the other hand there exist different supercomputers like K-computer, BlueGene/Q, and Intel clusters with XeonPhi accelerators or with GPU accelerators.
The eigensolver routines from the different libraries behave differently on the different computer architectures.
In the first step, we evaluate the several aspects of the routines on the existing production and prototype supercomputers available to give the users recommendations which routine to use for their specific task.
At the moment, evaluation is planned with respect to performance, accuracy and reproducibility in hybrid parallel execution. In the next step, we adapt the routines to the architectures.

We expect to provide the JLESC community with an overview of pros and cons of existing software, and a perspective view of better adaptation to present and planned computers and accelerators.

For the goal of the project, we want to publish results of the evaluations so that users can choose the best software for their computer.
In the next step tuning of the existing software should be done and the new results are made available to the community.


## Results for 2015/2016

This project was submitted in August 2015, and started from January 2016, officially.
The porting process has already started for couple of eigensolver libraries and on couple of systems.
We selected three libraries, ELPA, Elemental and EigenExa, and available resources, the K computer, JUQUEEN, and JURECA.

The present status is summarized in the following table.
We confirmed the libraries are ported and perform on the systems;
*Hybrid* means MPI/OpenMP hybrid parallel mode,
*Pure MPI* means only MPI parallel mode.

{:.table.table-sm}
| HW Platform | ELPA (2015.11) | Elemental (0.85) | EigenExa (2.4a) |
|:--+:---:+:---:+:---:|
| K | Hybrid [^1] | NA [^2] | Hybrid |
| JUQUEEN | Hybrid | Pure MPI [^3] | Hybrid |
| JURECA | Hybrid | Hybrid | Hybrid |

[^1]: On the K computer, ELPA2 performs in a hybrid parallel fashion, but we confirmed that ELPA1 performs in the pure MPI mode.
[^2]: Elemental needs C++10, but C++10 functionality is not supported on the current compiler on the K computer.
[^3]: Running in the pure MPI mode is confirmed on JUQUEEN and JURECA at the moment.

## Results for 2016/2017

1. We have done benchmarks using EigenExa, ELPA, and Elemental on available platforms, K, JUQUEEN and JURECA.
1. Some of the combinations are not available due to compilation problems or runtime software. We will also continue the compilation if we get a new version or a new compiler environment.
1. On the latter half of 2016/2017, we analyzed the correlation between the number of expected eigenspectrum and computing time cost. It affects to select best dense eigensolver for application users.
 * EigenExa very good if the full eigenspectrum is wanted
 * Libraries have to be tuned for the architecture
 * Best performance with the library tuned for the machine
 * On JUQUEEN and JURECA hybrid parallelization with moderate OpenMP part preferred
 * On K computer EigenExa best with as little MPI parallelization as necessary
 * On K computer ELPA2 best with pure MPI parallelization
 * If only 5 percent of eigenspectrum needed even on K computer ELPA2 pure MPI becomes fastest

1. GPU or accelerator-based eigenvalue solver like MAGMA or ELPA must be examined in 2017/2018. Currently, we have not yet confirmed to build the ELPA GPU extension on JURECA. Also, we would enhance the EigenExa library with an acceleration of GPUs.

## Results for 2017/2018

1. We have done benchmarks using EigenExa, ELPA, and Elemental on available platforms, K, JUQUEEN and JURECA and lately on JURECA Booster module.
1. As JUQUEEN will be put out of operation by end of March 2018 we only completed old benchmarks. The old compiler does not support C++/11 and the latest Fortran, thus it was not possible to install newer versions of Elemental and ELPA.
1. We inspected new versions of ELPA and EigenExa that support KNL processors.
1. Support for Elemental is temporarily stopped with version 0.87.7, which is the last stable version and runs on JURECA in pure MPI mode, thus there are only results for JURECA for this version.
1. Results are still the same as 2016/17
 * EigenExa very good if the full eigenspectrum is wanted
 * Libraries have to be tuned for the architecture
 * Best performance with the library tuned for the machine
 * On JUQUEEN and JURECA hybrid parallelization with moderate OpenMP part preferred
 * On K computer EigenExa best with as little MPI parallelization as necessary
 * On K computer ELPA2 best with pure MPI parallelization
 * If only 5 percent of eigenspectrum needed even on K computer ELPA2 pure MPI becomes fastest
1. No results for GPU
1. First results for KNL on JURECA booster, similar to the results for JURECA

## Results for 2018/2019

1. (Cont.) Distributed MPI/OpenMP Parallel
 * On four nodes a combination with 16 MPI processes per node and four OpenMP threads per MPI process is as fast as the pure MPI parallelization for ELPA on a KNL system.
 * On a single KNL node pure MPI parallelization was better than hybrid.
 * Plan update with respect to the machine replacement in very future!!
 
1. (Cont.) GPU extensions (standalone/cluster)
 * No update up to now
 
1. (UPDATE) Manycore extensions (KNL, PEZY SCx, etc.)
 * Wilkinson512/Kevd specialized for 2,4,8-wide SIMD intrinsic : 2 versions Wilkinson and Dongarra-Wilkinson
 * Parameter survey for NB of Back-transform


### Software update and descriptions:

* EigenExa : 2.4p1
* ELPA : 2017.11.001
       includes support for KNL and GPU, new user interface
* Elemental: 0.87.7
           allows to compute arbitrary part of the eigenspectrum


## Visits and meetings

In the 4th JLESC meeting at Bonn, we had a pre-meeting of this project with regard to a research update and planning in 2016 of each member.

Frequent e-mail exchanges between Toshiyuki Imamura and Inge Gutheil.
In the 5th JLESC meeting at Lyon,  both met and discussed about this project.
Also, 6th JLESC meeting was hosted by AICS and Inge Gutheil visited AICS.
Toshiyuki Imamura visited the 7th JLESC workshop in UIUC Urbana and
the 8th JLESC workshop in Barcelona. He visited Juelich in 24/07/2017 after ISC'17
to talk about KNL usage.
They organized a minisymposium and presented a talk titled 'Performance benchmark of standard eigensolver on KNL systems', at the PMAA2018 conference, Zurich.
In 2019, Toshiyuki visited Juelich again in 24-25/01/2019 and talked about GPU usage on ELPA and EigenExa libraries.
Toshiyuki will join the 9th JLESC meeting in Tennessee Knoxville.


## Impact and publications

We have no publication yet.


<!--
{% comment %}
=============================
== CITING OWN PUBLICATIONS ==
=============================

You can list your own publications below in case you did not cite them in the text
(which you should do, though).
Use the Liquid citing syntax as explained in the wiki:
https://github.com/JLESC/jlesc.github.io/wiki/Markup-Language#cite-and-list-publications
Remember to use the `--file jlesc.bib` with the `cite` tag.

=====================================
== START HERE WITH YOUR ADDITIONAL REFERENCES ==
{% endcomment %}



{% comment %}
== NO MORE BELOW THIS ==
========================
{% endcomment %}
-->

{% bibliography --cited --file jlesc.bib %}


## Future plans

<!-- In 2016, we divide the first year into 1st and 2nd halves on the management of this project.
For each half, we plan to do as follow.

* 1st 6 months: performance measurements on the available resources

* 2nd 6 months: tuning the existing libraries on the available computers -->

<!--We plan a minisymposium at PMAA 2018 in Zuerich with the title

 *Performance benchmark of standard eigensolver on KNL systems -->

Apply to the computational resource such as 
"Large-scale HPC Challenge" Project, Joint Center for Advanced High Performance Computing (JCAHPC).

Benchmarking on GPU accelration systems.

## References

{% bibliography --file external/dense_eigen_project.bib %}
