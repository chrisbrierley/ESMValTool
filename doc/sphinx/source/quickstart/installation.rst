.. _install:

************
Installation
************

ESMValTool 2.0 requires a Unix(-like) operating system and Python 3.6+.

The ESMValTool supports three different installation methods:

* Installation through Conda package manager (see https://www.continuum.io);

* Deployment through a Docker container (see https://www.docker.com);

* From the source code available at https://github.com/ESMValGroup/ESMValTool.

The next sections will detail the procedure to install ESMValTool for each of
this methods.


Conda installation
==================

In order to install the Conda package, you will need both conda and Julia
pre-installed, this is because Julia cannot be installed from conda.
For a minimal conda installation go to https://conda.io/miniconda.html.
Installation instructions for Julia can be found on the
`Julia download page <https://julialang.org/downloads/>`_.

Once you have installed the above prerequisites, you can install ESMValTool by running:

.. code-block:: bash

    conda install esmvaltool -c esmvalgroup -c conda-forge

Here ``conda`` is the executable calling the Conda package manager to install
``esmvaltool`` and the ``-c`` flag specifies the software channels in which ``esmvaltool``
and its dependencies can be found.

Installation of subpackages
---------------------------

The diagnostics bundled in ESMValTool are scripts in four different programming languages: Python, NCL, R, and Julia.

There are four language specific packages available:

* ``esmvaltool-julia``
* ``esmvaltool-ncl``
* ``esmvaltool-python``
* ``esmvaltool-r``

The main ``esmvaltool`` package contains all four subpackages listed above.

If you only need to run a recipe with diagnostics in some of these languages, it is possible to install only the dependencies needed to do just that.

* The diagnostic script(s) used in each recipe, are documented in :ref:`recipes`. The extension of the diagnostic script can be used to see in which language a diagnostic script is written.
* Some of the CMORization scripts are written in Python, while others are written in  NCL. Therefore, both ``esmvaltool-pyhon`` and ``esmvaltool-ncl`` need to be installed in order to be able to run all CMORization scripts.

For example, to only install support for diagnostics written in Python and NCL, run

.. code-block:: bash

    conda install esmvaltool-python esmvaltool-ncl -c esmvalgroup -c conda-forge

Note that it is only necessary to install Julia prior to the conda installation if you are going to install the ``esmvaltool-julia`` package.

Note that the ESMValTool source code is contained in the ``esmvaltool-python`` package, so this package will always be installed as a dependency if you install one or more of the packages for other languages.

Docker installation
===================

.. warning::
    Docker section to be added


Install from source
===================


Obtaining the source code
-------------------------

The ESMValTool source code is available on a public GitHub repository:
https://github.com/ESMValGroup/ESMValTool

The easiest way to obtain it is to clone the repository using git
(see https://git-scm.com/). To clone the public repository:

.. code-block:: bash

    git clone https://github.com/ESMValGroup/ESMValTool.git

It is also possible to work in one of the ESMValTool private repositories, e.g.:

.. code-block:: bash

    git clone https://github.com/ESMValGroup/ESMValTool-private.git

By default, this command will create a folder called ESMValTool containing the
source code of the tool.

GitHub also allows one to download the source code in as a tar.gz or zip file. If
you choose to use this option, download the compressed file and extract its
contents at the desired location.


Prerequisites
-------------

It is recommended to use conda to manage ESMValTool dependencies.
For a minimal conda installation go to https://conda.io/miniconda.html. To
simplify the installation process, an environment definition file is provided
in the repository (``environment.yml`` in the root folder).

.. attention::
    Some systems provide a preinstalled version of conda (e.g., via the module environment).
    However, several users reported problems when installing NCL with such versions. It is
    therefore preferable to use a local, fully user-controlled conda installation.
    Using an older version of conda can also be a source of problems, so if you have conda
    installed already, make sure it is up to date by running ``conda update -n base conda``.

To enable the ``conda`` command, please source the appropriate configuration file
from your ``~/.bashrc``  file:

.. code-block:: bash

    source <prefix>/etc/profile.d/conda.sh

or ``~/.cshrc``/``~/.tcshrc`` file:

.. code-block:: bash

    source <prefix>/etc/profile.d/conda.csh

where ``<prefix>`` is the install location of your anaconda or miniconda
(e.g. ``/home/$USER/anaconda3`` or ``/home/$USER/miniconda3``).


.. note::
    Note that during the installation, conda will ask you
    if you want the installation to be automatically sourced from your
    ``.bashrc`` or ``.bash-profile`` files; if you answered yes, then conda
    will write bash directives to those files and everytime you get to your
    shell, you will automatically be inside conda's ``(base)`` environment.
    To deactivate this feature, look for the ``# >>> conda initialize >>>``
    code block in your ``.bashrc`` or ``.bash-profile`` and comment the whole block out.


The ESMValTool conda environment file can also be used as a requirements list
for those cases in which a conda installation is not possible or advisable.
From now on, we will assume that the installation is going to be done through
conda.

Ideally, you should create a conda environment for ESMValTool, so it is
independent from any other Python tools present in the system.

Note that it is advisable to update conda to the latest version before
installing ESMValTool, using the command (as mentioned above)

.. code-block:: bash

    conda update --name base conda

To create an environment, go to the directory containing the ESMValTool source
code (called ESMValTool if you did not choose a different name) and run

.. code-block:: bash

    conda env create --name esmvaltool --file environment.yml

This installs the ESMValCore package from conda as a dependency.

The environment is called ``esmvaltool`` by default, but it is possible to use
the option ``--name SOME_ENVIRONMENT_NAME`` to define a custom name. You should then activate
the environment using the command:

.. code-block:: bash

    conda activate esmvaltool

It is also possible to update an existing environment from the environment
file. This may be useful when updating an older installation of ESMValTool:

.. code-block:: bash

    conda env update --name esmvaltool --file environment.yml

but if you run into trouble, please try creating a new environment.

.. attention::
    From now on, we assume that the conda environment for ESMValTool is
    activated.

Software installation
---------------------

Once all prerequisites are fulfilled, ESMValTool can be installed by running
the following commands in the directory containing the ESMValTool source code
(called ESMValTool if you did not choose a different name):

.. code-block:: bash

    pip install -e '.[develop]'

If you would like to run Julia diagnostic scripts, you will also need to
`install Julia <https://julialang.org/downloads/>`_ and the Julia dependencies:

.. code-block:: bash

    julia esmvaltool/install/Julia/setup.jl

If you would like to run R diagnostic scripts, you will also need to install the R
dependencies. Install the R dependency packages:

.. code-block:: bash

    Rscript esmvaltool/install/R/setup.R

The next step is to check that the installation works properly.
To do this, run the tool with:

.. code-block:: bash

    esmvaltool --help

If everything was installed properly, ESMValTool should have printed a
help message to the console.

For a more complete installation verification, run the automated tests and
confirm that no errors are reported:

.. code-block:: bash

    python setup.py test


