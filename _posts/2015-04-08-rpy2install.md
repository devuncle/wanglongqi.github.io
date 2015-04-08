---
author: Longqi
comments: true
date: 2015-04-08 15:55:45
layout: post
slug: ffmpegcn
title: Install Rpy2 on Windows
categories: [R]
tags:
- R
- Python
- Rpy2
- Mingw32
---
[Christoph Gohlke](http://www.lfd.uci.edu/~gohlke/pythonlibs/#rpy2) provides a page to release unofficial binaries of python packages. However, for `rpy2` and `pycuda` you may have to use exactly the same version of `R` or `cuda toolkit` to use the binary. Therefore, if you do not want to use that version, you may have to compile the package yourself. For the case of `rpy2`, the process is quite simple. Since the offical `rpy2` site does not offer any suggestion on howto build it under Windows, you can compile and install `rpy2` under Windows by following this article.

1. Change `unixcompiler.py`

	Change following codes in `unixcompiler.py` under `distutils` folder.

	    compiler = os.path.basename(sysconfig.get_config_var("CC"))
	    if sys.platform[:6] == "darwin":

	Search for similar code in the file, and change these lines to:

	    #compiler = os.path.basename(sysconfig.get_config_var("CC"))
	    compiler = 'gcc'
	    if sys.platform[:6] == "darwin":

	Yes, we simply bypass the command, and give the right answer.

2. Set R_HOME and R_USER

	The default installation the R_HOME is `C:\PROGRA~1\R\R-31~1.2`.

3. pip install singledispatch

4. Pass r-home when build rpy2

	`python setup.py build --r-home C:\PROGRA~1\R\R-31~1.2`

5. Done. 

	Run `python setup.py install` as your wish.

Finally, if you do not want compile `rpy2`. There is a package named `pyper` written by Xia. The package is quite light-weighted and well-written. If you do not want heavily use of R in python, but only make a few communication, `pyper` is the right choice to go.

BTW, I found many people are not installed rpy2 successfully due to their tool chain. If you are absolutely new to Python, or never build package from source, you should probably first start up a suitable tool chain before trying to build other package. You can download a sample Cython file to test your tool chain. Normally, a suitable tool chain can compile regular Cython files. You will also need fortran compiler for some packages.

 