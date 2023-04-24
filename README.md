# AOS Special Project - Flamegraph files

Download and open in browser to visualize it.

## Install

Note: Below installation is made in addition to the instllation specified in project report.

1. `sudo apt-get install -y libc6-prof`

## How to run the code with perf?

### For vanilla python 3.11

1. `env LD_LIBRARY_PATH=<path to libc6-prof> perf record -F 100 -g --vmlinux=<path to vmlinux file> -o <output perf file> -- python test.py`
2. `perf script --max-stack 100000 -i <output perf file> | ../scripts/stackcollapse-perf.pl > out.stacks-folded && ../scripts/flamegraph.pl out.stacks-folded > <file name>.svg`

### For patched python 3.11

1. `env LD_LIBRARY_PATH=<path to libc6-prof> perf record -F 100 -g --vmlinux=<path to vmlinux file> -o <output perf file> -- python -X perf test.py`
2. `perf script --max-stack 100000 -i <output perf file> | ../scripts/stackcollapse-perf.pl > out.stacks-folded && ../scripts/flamegraph.pl out.stacks-folded > <file name>.svg`
