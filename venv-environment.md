# Python Virtual Environment Set-up

Whilst my favourite package managers is Conda, I'm presently working on a Manning Live Project where the Python `venv` is being used. As a consequence, I have made the following notes.

Unlike Conda, the Python virtual environment `venv` does not have a prescriptive default installation directory, rather there is variation both in where the environment is installed as well as naming convention. Common patterns of usage include installing the environment under the project installation and naming the directory as either `.venv` or `venv`.

Installation of the virtual environment is similar to other package managers, however stipulation of the installation directory by either initialising under the project root directory, or by passing in a directory path is necessary.

## Installation of the virtual environment

### Prerequisite tasks

The `venv` replies on Python being installed on the host system. This can be determined by opening a terminal (or command prompt) and checking the python version. For Ubuntu and other Linux distributions, you can check  the `version`. On my Ubuntu 20.04 workstation this results in...

```bash
$ python3 --version

Python 3.8.10
```

Alternatively, you could also use the `which`

```bash
$ which python3

/usr/bin/python3
```

There are a few initial tasks that are dependent on the operating system for which venv is being installed. I have made notes only on Ubuntu so far, but hope to fill out any additional tasks for Windows at some point in the future.

#### Ubuntu

In order to run venv on Ubuntu, `ensurepip` needs to be installed. Installing `ensurepip` requires executing from the terminal

```bash
sudo apt install python3.8-venv
```

Creation of the venv environment is very straightforward with the issuing of a single command. If you are creating the environment under your project directory, from the project root directory within a terminal run

```bash
python3 -m venv .venv/
```

That creates the virtual environment using the same version of Python as your system versionl

> If using Git for your project source control, ensure you place an entry in the .gitignore file to exclude the virtual environment files.

## Activation and deactivation

Activating the virtual environment is straightforward. From the project root, run the terminal command

```bash
source .venv/bin/activate
```

Like other environment managers, the terminal line has the virtual environment name prefixed.

```bash
(.venv) %
```

To deactivate the environment, from the project root, run the terminal command

```bash
(.venv) % deactivate
```

## Installation of environment dependencies

As per other familiar environment managers, once the environment is activated, you can use `pip` to install the necessary project packages. 

> For installing Jupyter Notebook on Ubuntu after creating and activating my virtual environment, I had to install wheel first up in order to get notebook to install without an error.

```bash
pip install wheel
```

For this project, the installed packages are

| Library                                              | Command line             | Version installed  |
| ---------------------------------------------------- | ------------------------ | ------------------ |
| [Jupyter Notebook](https://jupyter.org/install.html) | `pip install notebook`   | `notebook-6.4.3`   |
| [Numpy](https://numpy.org/)                          | `pip install numpy`      | `numpy-1.21.1`     |
| [Pandas](https://pandas.pydata.org/)                 | `pip install pandas`     | `pandas-1.3.1`     |
| [Matplotlib](https://matplotlib.org/)                | `pip install matplotlib` | `matplotlib-3.4.3` |
| [Seaborn](https://seaborn.pydata.org/)               | `pip install seaborn`    | `seaborn-0.11.1`   |

### Testing

To determine whether the Jupyter Notebook was successfully installed, with the python virtual environment still activated, run the Jupyter Notebook command

```bash
(.venv) jupyter notebook
```

After a brief server start-up period, Jupyter Notebook will open in your default browser if the installation is successful. Closing the Notebook is simply performed by closing the browser tab. If you are finished, the server can be turned off within the terminal it was started by entering `Ctrl + C`

## Sharing the project

In order to share (or rebuild) an existing environment, after all the necessary packages are installed, with the environment activated and from the project root, run the following command in the terminal

`pip freeze > requirements.txt`

> A word on sharing...make sure to have a `.gitignore` entry preventing including the `.venv` directory contents to the project repository. Instead, just rely on the `requirements.txt` file to create the environment

To recreate the environment, from scratch, create a venv environment under the new project source, ensure the requirements.txt is present under the project's root directory, activate the environment and enter in the terminal, the command

 `pip install -r requirements.txt`

This completes the description of setting up a virtual environment using `venv`
