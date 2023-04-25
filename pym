#!/bin/bash
set -e
set -o pipefail

function show-version {
  echo "pym - python package manager"
  echo "version: 0.1"
}

function show-help {
  show-version
  echo "
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
"
}

function find-python {
  if [ "$python" != "" ]; then
    return
  fi
  local o=$IFS
  IFS=$(echo -en "\n\b")
  for dir in $(echo "$PATH" | sed 's/:/\n/g' | grep -v npm); do
    if [ -d "$dir" ]; then
      for python in $(find "$dir" \
        -not -path '*node_modules*' \
        -not -path '*npm*' \
        -name 'python*' \
        -not -name '*-config' \
        -not -name '*-tex' \
        -perm +111 2>/dev/null ||
        true); do
        if [ -f "$python" ] || [ -l "$python" ]; then
          break
        fi
      done
    fi
  done
  IFS=$o
  if [ "$python" == "" ]; then
    python="python"
  else
    echo "using $python"
  fi
}

function select-python {
  if [ "$python" == "" ]; then
    hash python 2>/dev/null && python=python || true
  fi
  if [ "$python" == "" ]; then
    hash python3 2>/dev/null && python=python3 || true
  fi
  if [ "$python" == "" ]; then
    find-python
  fi
}

function setup-gitignore {
  if [ $(git status -u | grep python_modules | wc -l | awk '{print $1}') != '0' ]; then
    echo python_modules >>.gitignore
  fi
}

function init {
  if [ ! -f requirements.txt ]; then
    touch requirements.txt
  fi
  if [ ! -d python_modules ]; then
    select-python
    echo "setting up venv"
    "$python" -m venv python_modules
  fi
  setup-gitignore 2>/dev/null || true
}

function install-dep {
  init
  source python_modules/bin/activate
  echo "installing packages in requirements.txt"
  pip install -r requirements.txt
  for dep in $@; do
    if [ $(grep -iE "^$dep=" requirements.txt | wc -l | awk '{print $1}') == '0' ]; then
      echo "installing $dep"
      pip install $dep
      pip list | grep -i "^$dep " | awk '{print $1 "==" $2}' >>requirements.txt
    fi
  done
}

function run {
  if [ ! -d python_modules ]; then
    install-dep
  fi
  source python_modules/bin/activate
  python $@
}

if [ $# == 0 ]; then
  show-help
  exit 0
fi

case $1 in
version | v | --version | -v)
  show-version
  ;;
help | h | --help | -h)
  show-help
  ;;
init)
  init
  ;;
install | i | add | a)
  shift
  install-dep $@
  ;;
run | r)
  shift
  run $@
  ;;
*)
  echo >&2 "Unknown argument: $1"
  exit 1
  ;;
esac
