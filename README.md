# How to Perfect Your Python Development Setup

## Effective py environment

Your shell is more than a prebuilt program provided to you as-is. It’s a framework on which you can build an ecosystem. This ecosystem will come to fit your needs so that you can spend less time fiddling and more time thinking about the next big project you’re working on.

pyenv:
pyenv is a mature tool for installing and managing multiple Python versions on macOS. I recommend installing it with Homebrew. If you’re using Windows, you can use pyenv-win. After you’ve got pyenv installed, you can install multiple versions of Python into your Python environment with a few short commands.

conda:
If you’re in the data science community, you might already be using Anaconda (or Miniconda). Anaconda is a sort of one-stop shop for data science software that supports more than just Python.

Enter virtual environments. You can think of a virtual environment as a carbon copy of a base version of Python. If you’ve installed Python 3.7.3, for example, then you can create many virtual environments based off of it. When you install a package in a virtual environment, you do it in isolation from other Python environments you may have. Each virtual environment has its own copy of the python executable.

venv:
venv ships with Python versions 3.3+. You can create virtual environments just by passing it a path at which to store the environment’s python, installed packages, and so on.

```shell
python -m venv ~/.virtualenvs/my-env

source ~/.virtualenvs/my-env/bin/activate
~/.virtualenvs/my-env/Scripts/activate

deactivate
```

venv is built on the wonderful work and successes of the independent virtualenv project. virtualenv still provides a few interesting features of its own, but venv is nice because it provides the utility of virtual environments without requiring you to install additional software. You can probably get pretty far with it if you’re working mostly in a single Python version in your Python environment.

pyenv-virtualenv:
If you’re using pyenv, then pyenv-virtualenv enhances pyenv with a subcommand for managing virtual environments

```shell
// Create virtual environment
pyenv virtualenv 3.7.3 my-env

// Activate virtual environment
pyenv activate my-env

// Exit virtual environment
pyenv deactivate
```

pipenv:
pipenv is a relatively new tool that seeks to combine package management (more on this in a moment) with virtual environment management. It mostly abstracts the virtual environment management from you, which can be great as long as things go smoothly.

## Packege Management

For many of the projects you work on, you’ll probably need some number of third-party packages. Those packages may have their own dependencies in turn. In the early days of Python, using packages involved manually downloading files and pointing Python at them. Today, we’re fortunate to have a variety of package management tools available to us.

pip:
pip (pip installs packages) has been the de facto standard for package management in Python for several years. It was heavily inspired by an earlier tool called easy_install. Python incorporated pip into the standard distribution starting in version 3.4. pip automates the process of downloading packages and making Python aware of them.

A common way to specify project dependencies for pip is with a requirements.txt file. Each line in the file specifies a package name and, optionally, the version to install.

```python 
python -m pip install -r requirements.txt 
```
pipenv:
pipenv has most of the same basic operations as pip but thinks about packages a bit differently. Remember the Pipfile that pipenv creates? When you install a package, pipenv adds that package to Pipfile and also adds more detailed information to a new lock file called Pipfile.lock. Lock files act as a snapshot of the precise set of packages installed, including direct dependencies as well as their sub-dependencies.

pipenv also distinguishes between development dependencies and production (regular) dependencies. You may need some tools during development, such as black or flake8, that you don’t need when you run your application in production. You can specify that a package is for development when you install it.

## Python Environment Tips and Tricks

Know your current virtual environment:
As mentioned earlier, it’s a great idea to display the active Python version or virtual environment in your command prompt. Most tools will do this for you, but if not (or if you want to customize the prompt), the value is usually contained in the VIRTUAL_ENV environment variable.

Disable unnecessary, temporary files:
Have you ever noticed *.pyc files all over your project directories? These files are pre-compiled Python bytecode—they help Python start your application faster. In production, these are a great idea because they’ll give you some performance gain. During local development, however, they’re rarely useful. Set PYTHONDONTWRITEBYTECODE=1 to disable this behavior. If you find use cases for them later, then you can easily remove this from your Python environment.

Customize your Python interpreter:
You can affect how the REPL behaves using a startup file. Python will read this startup file and execute the code it contains before entering the REPL. Set the PYTHONSTARTUP environment variable to the path of your startup file. (Mine’s at ~/.pystartup.) If you’d like to hit Up for command history and Tab for completion like your shell provides, then give this startup file a try.1 