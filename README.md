# pym - python package manager

Works like npm (nodejs package manager) but for python.

## Features

- Dependecies are installed locally (per project) with `venv` in `./python_module`

- Dependencies are added to `requirements.txt` automatically

- This cli tool is a single executable file, you can name it whatever you want, e.g. pym, py, pm, or just p

## Usage

```
pym - python package manager
version: 0.1

Usage: pym [command]

Commands:

  version:
    (Alias: v, -v, --version)
    Show version of this cli tool

  help:
    (Alias: h, -h, --help)
    Show this help message

  init:
    Setup dependecy environment with venv in python_modules

  install:
    (Alias: i, add, a)
    Install dependecy packages locally with venv project, auto init if needed

  run:
    (Alias: r)
    Run the python script within virtual envrionment, auto init if needed
```

## Why this name?

As inspired by npm (nodejs package manager), I named this tool ppm (python package manager) initially.

Later I checked with pacman (archlinux package manager) and found the package plan9port has already registered an executable named ppm, hence renamed to avoid name clash.

## Todo

Look into [PEP 582 - Python local packages directory](https://www.python.org/dev/peps/pep-0582) with [PDM](https://github.com/pdm-project/pdm).
Introduction see: [this article](https://www.infoworld.com/article/3654196/pdm-a-smarter-way-to-manage-python-packages.html)
