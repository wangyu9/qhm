# Variational quasi-harmonic maps for computing diffeomorphisms

This repo accompanies the paper: 

*	**Variational Quasi-Harmonic Maps for Computing Diffeomorphisms**.
  
	Yu Wang, Minghao Guo, Justin Solomon.

	_ACM Trans. on Graph. 42(4)_. 
	_ACM SIGGRAPH 2023 (Journal Track)_. 
	[OpenAccessPaper](https://dl.acm.org/doi/pdf/10.1145/3592105)  [Dropbox](https://www.dropbox.com/s/zye5ec41ejtk4pi/Variational_Quasi_Harmonic_Maps.pdf?dl=0)


# Usage 

See the demo.m file. This demo takes in a triangle mesh and computes a deformed mesh (hopefully) without inverted triangles, under a prescribed boundary curve. 

If the code runs successfully, a mesh without inverted triangles will be produced. You may have to adjust the hyperparameters, especially the `number of iterations`, `learning rates` (step size) and the `type of parameterization` (of matrix A(x)), as described in details in the paper. The demo does not use the optinal post-processing joint-space Newton step (Sec. 9.2.1 in the paper), which is only necessary for very few ill conditioned examples; if useful you can refer to oracle_joint_hessian.m for that step. 

# Installation

There are two dependencies: gptoolbox and SuiteSparse. 

```
git clone https://github.com/alecjacobson/gptoolbox.git  # download the gptoolbox 
```

I have copied the relevant gptoolbox functions to the repo, so you do not have to install gptoolbox anymore. 

Following the instruction to install SuiteSparse 7.0.1 (note the latest the version of SuiteSparse removes some dependent functions such as the sparse2 function)

https://github.com/DrTimothyAldenDavis/SuiteSparse/tree/v7.0.1?tab=readme-ov-file#quick-start-for-matlab-users-linux-or-mac

## TL;DR for installing SuiteSparse in matlab

Take Mac for example: 

### First,  install SuiteSparse's dependencies mpfr and gmp

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"  # install brew if necessary
brew install mpfr
brew install gmp
``` 

### Second, compile SuiteSparse

Following SuiteSparse's instuction, e.g. 

```
make gbmatlab
make install
```

### Finally, compile *.mex files in matlab

Only for Mac: install Xcode and accept the license in order to compile *.mex files in the next step.

In Matlab, run:

```
cd ~/workspace/tools/SuiteSparse-7.0.1/		% cd to the folder, change it to your own path
SuiteSparse_install	% compile all *.mex files
```

The mex functions that our code repo relies on are `sparse2` and `analyze`. 

