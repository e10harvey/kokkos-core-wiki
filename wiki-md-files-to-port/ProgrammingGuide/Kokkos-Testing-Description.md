## Scope of Kokkos Testing

This chapter develops the primary focus of the document, the Kokkos Testing Workflow. Software testing accompanies all development activities and is performed by each Kokkos developer as part of their daily tasks: implementation of new features, debugging, development of test problems, user support and documentation. The end use of the Kokkos software - integration into a host application to improve performance (i.e., performance reduction is unallowable) - establishes a hierarchy of considerations that are all intimately dependent on software testing: inclusion of developers work into the _develop_ branch through an approval process whose aim is the maintenance of software quality/integrity; integration of the fully-tested and clean _develop_ branch into Trilinos without producing additional failures in Trilinos testing. (Trilinos is a tight-woven collection of software packages of which Kokkos is a member and on which many other packages depend. Trilinos packages are designed/developed for integration into other applications). This latter aspect of Kokkos testing is called (Trilinos) __Promotion Testing__ and is the primary focus of this section; it is presented in detail (an attachment) as this task must be performed exactly as described for a successful promotion.

## Kokkos Routine/Daily/Nightly Testing

Testing is a through-going aspect of software development, touching all phases of a software project. Bringing together the test scripts, the test problems and repository management ( previous chapter), a team methodology has evolved that evaluates the correctness and speed of the development product prior to commit. Each developer will use a combination of existing unit and performance tests, or newly written tests, in combination with existing or standalone test scripts to evaluate bugfixes, new features and and different approaches for improving performance (since performance reduction is not an option). Submission of a commit with a pull request will initiate a software review followed by suggestions for improvement or approval of the pull request.

Nightly testing is another aspect of routine testing. Using the Jenkins continuous integration software, the jenkins_test_driver script builds test jobs to (batch) submit to the platforms identified in Table 2-1. The Jenkins job, itself cron-based (initiated at a specific time), builds makefiles to be run within Jenkins test jobs that exercise a range of compilers, Kokkos backends and combinations of test problems. Results from these tests run for the current develop branch of Kokkos become the standard for evaluating the daily integrity of this Kokkos branch. Note that the Jenkins jobs have test coverage for the full range of architectures and compilers that Kokkos supports.    

## Other Testing

A set of tutorial problems have been developed for use in hands-on instruction exercises. These are not part of a scheduled test regimen, although they are run and performance data updated periodically when Kokkos capabilities have changed significantly or new compilers and architectures are added to our repertoire. Module choices, scripts and script options for these problems have been collected so that they can be built into the Kokkos repository.

## Kokkos Promotion Testing and Promotion Processes

Promotion testing refers to the process developed by the Kokkos team that leads to integration of the stand-alone version of the Kokkos software back into the parent Trilinos software as a package (the basic unit of software identity within the Trilinos project). The promotion testing process was developed to satisfy the requirements for pushing Kokkos software updates into Trilinos with the confidence that these updates will not adversely affect the integrity of other packages that depend on Kokkos, nor will it adversely affect the stability of the Trilinos software repository itself.
 
Promotion testing is conducted normally at four-to-eight week intervals (depending on Kokkos software commits and team commitments). The Kokkos _develop_ branch is the remote repository to which accepted new features, bug-fixes and upgrades/improvements are committed. _origin/master_ is the primary remote branch of Kokkos, the pristine version of the Kokkos software, that serves as the source for cloning and forking of the repository. It is not the version of Kokkos that will be integrated into Trilinos during the promotion process; it is the Kokkos _develop_ branch that is merged into the Kokkos _master_ branch after a successful promotion into Trilinos.  For promotion of the _develop_ branch into Trilinos to take place, the _develop_ branch of Kokkos must first pass all Kokkos tests; when satisfactorily completed, the Kokkos _develop_ branch must then pass all the Trilinos tests! This process requires comparative testing of two (_develop_) branches of Trilinos, one containing the current (at the time of testing) Kokkos package in Trilinos (called the _pristine_ branch) and the other with a current _develop_ branch of Kokkos snapshotted into it (called the _updated_ branch). (_Snapshotting_ is a re-integration process accomplished by the script _snapshot.py_.) These two versions of the Trilinos repository are then run through all tests appropriate for the Trilinos-Kokkos package tests. The scripts used in testing the updated and pristine Trilinos versions are identified in Table 2.2 and run on platforms _shepard_ and _white_. The goal in testing these two versions of Trilinos is that the updated version of Trilinos will not introduce additional/new failures or differences into the Trilinos test suite relative relative to those exhibited by the current pristine version of Trilinos. When this goal is completed satisfactorily, a _(git) push_ of the Kokkos _develop_ branch into Trilinos will be made; this is followed by a push of Kokkos _develop_ to Kokkos _master_ .
  
This section has provided a description of the promotion testing process and a mention of its many components. As the process of testing, snapshotting, testing and committing to Trilinos and pushing to (Kokkos) master is quite tedious, its multiple steps have been scripted. A step-by-step description of the workflow is provided in document (a txt file) in document __kokkos-promotion__ and also as an attachment. The attachment documents/describes the testing by script and platform as well as the git commands required to successfully carry out a Kokkos promotion.

 