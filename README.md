# pym - python package manager

Works like npm (nodejs package manager) but for python.

## Features

- Dependecies are installed locally (per project) with `venv` in `./python_module`

- Dependencies are added to `requirements.txt` automatically

- Cross platform: it works on Linux, Mac, and Windows (with git bash)

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

## License

This project is licensed with [BSD-2-Clause](./LICENSE)

This is free, libre, and open-source software. It comes down to four essential freedoms [[ref]](https://seirdy.one/2021/01/27/whatsapp-and-the-domestication-of-users.html#fnref:2):

- The freedom to run the program as you wish, for any purpose
- The freedom to study how the program works, and change it so it does your computing as you wish
- The freedom to redistribute copies so you can help others
- The freedom to distribute copies of your modified versions to others
