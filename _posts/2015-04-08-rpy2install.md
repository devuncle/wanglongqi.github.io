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
You can compile and install rpy2 under Windows by following this article.

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

	python setup.py build --r-home C:\PROGRA~1\R\R-31~1.2

5. Done. 

Run `python setup.py install` as your wish.

