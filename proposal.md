# Community Software Analysis Proposal

## Software: *DOLFINx*

*DOLFINx is a problem solving environment building upon the Finite Element Method platform FENICSx. FENICSx offers support for high level languages (such as Python) and also includes tools for high-performance applications. Within the FENICSx suite are a handful of other libraries, such as basix, ffcx, and ufl. Unified Form Language (UFL) is used to provide a mathematical-like description of the discretized variational form and the associated finite element spaces ($\mathcal{V}^h$). The FEniCSx Form Compiler (FFCx) is then used to convert this high-level UFL code into low-level C code. The Basix library provides helpful tools for working with many different finite element basis functions, including function and derivative evaluations, reference and physical space mappings, and interpolation between different finite element spaces. DOLFINx makes use of these libraries a full finite element workflow. These libraries also allow for high-performance code to be generated, with very little additional work required by the user. Because of the customizability and focus on high-performance capability, this library is targetted towards researchers in numerical PDEs, rather than specific industry applications.*

### Stats

| Description | Your answer |
|---------|-----------|
| Repository URL |  https://github.com/FEniCS/dolfinx  |
| Main/documentation website |  https://docs.fenicsproject.org/dolfinx/main/python/  |
| Year project was started | 2003 |
| Number of contributors in the past year | 27 |
| Number of contributors in the lifetime of the project | 144 |
| Number of distinct affiliations | 5-10 |
| Where do development discussions take place? | Slack, Github issues |
| Typical number of emails/comments per week? | 25 on website, 3-5 on slack |
| Typical number of commits per week? | 3 |
| Typical commit size | a few changes, but varies to large sizes |
| How does the project accept contributions? | pull requests |
| Does the project have an automated test suite? | yes |
| Does the project use continuous integration? | yes |
| Are any legal/licensing steps required to contribute? | no |

### Install and run

Check the following boxes when complete or add a note below if you
encountered a problem.

- [x] I have installed the software
- [x] I have run at least one example
- [ ] I have run the test suite
- [ ] The test suite passes

Notes on install: spent 20+ hours trying to build on a fresh wsl, encountering the following problems (with this package, let alone all the dependencies):

1. Libboost was messing up MPI by downloading a potential second version (openmpi vs mpich). James helped me find this problem and suggested that it warranted a post somewhere for others to find.
```
-- Could NOT find MPI_CXX (missing: MPI_CXX_WORKS) (Required is at least version "3")
CMake Error at /usr/share/cmake-3.16/Modules/FindPackageHandleStandardArgs.cmake:146 (message):
  Could NOT find MPI (missing: MPI_CXX_FOUND) (found suitable version "3.1",
  minimum required is "3")
Call Stack (most recent call first):
  /usr/share/cmake-3.16/Modules/FindPackageHandleStandardArgs.cmake:393 (_FPHSA_FAILURE_MESSAGE)
  /usr/share/cmake-3.16/Modules/FindMPI.cmake:1688 (find_package_handle_standard_args)
  CMakeLists.txt:75 (find_package)
```


2. Needed to update from Ubuntu 20.04 to 22.04 for suitable compiler version.

3. Packages ffcx, ufl, basix, dolfinx clashed, and I had to download all of these and install them together, rather than separately one-by-one. More on that issue [here](https://fenicsproject.discourse.group/t/installation-error-with-ufcx/9086/6).

4. PyPi: `pip install fenics-ffx` only has up to version 0.5.0 of ffcx while version 0.6 is required. Clarified a thread on [discourse](https://fenicsproject.discourse.group/t/installation-of-dolfinx-on-ubuntu22-04-from-source-file/9063/9)

5. I'm not sure how to run the test suite. I can run some of the demos that do not require dolfinx (just ufl and basix). However, running `import dolfinx` in a python script gives the following error:
```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/home/grant/.local/lib/python3.10/site-packages/dolfinx/__init__.py", line 29, in <module>
    from dolfinx import common
  File "/home/grant/.local/lib/python3.10/site-packages/dolfinx/common.py", line 10, in <module>
    from dolfinx import cpp as _cpp
ImportError: /usr/local/lib/libdolfinx.so.0.6: undefined symbol: libmetis__rsmalloc
```


### Notes/concerns/risks

I'm concerned with my build/install working, despite there not being errors on this process. There are other ways to use dolfinx, but a local build is really what should be done.

#### Note on copyright
Students retain copyright on any work done in completion of a CU
course, so you are authorized to sign a [contributor license
agreement (CLA)](https://en.wikipedia.org/wiki/Contributor_License_Agreement),
affirm a [developer's certificate of
origin (DCO)](https://en.wikipedia.org/wiki/Developer_Certificate_of_Origin),
etc.  If you have concerns about this, please note them and/or reach
out to Jed directly.
