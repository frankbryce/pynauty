[![Build and test](https://github.com/pdobsan/pynauty/actions/workflows/build-and-test.yml/badge.svg)](https://github.com/pdobsan/pynauty/actions/workflows/build-and-test.yml)

# Pynauty 

Pynauty can be used to compare graphs for isomorphism and to determine
their automorphism group in a Python programming environment.  Pynauty
is a Python/C extension module using library components from the
[Nauty](https://pallini.di.uniroma1.it/) package by Brendan McKay.


## Usage

Here is an example of `pynauty`'s usage in an interactive session.

```python
>>> from pynauty import *
>>> g = Graph(5)
>>> g.connect_vertex(0, [1, 2, 3])
>>> g.connect_vertex(2, [1, 3, 4])
>>> g.connect_vertex(4, [3])
>>> print(g)
Graph(number_of_vertices=5, directed=False,
 adjacency_dict = {
  0: [1, 2, 3],
  2: [1, 3, 4],
  4: [3],
 },
 vertex_coloring = [
 ],
)
>>> autgrp(g)
([[3, 4, 2, 0, 1]], 2.0, 0, [0, 1, 2, 0, 1], 3)
>>> 
>>> g.connect_vertex(1, [3])
>>> autgrp(g)
([[0, 1, 3, 2, 4], [1, 0, 2, 3, 4]], 4.0, 0, [0, 0, 2, 2, 4], 3)
>>>
>>> g.set_vertex_coloring([set([3])])
>>> print(g)
Graph(number_of_vertices=5, directed=False,
 adjacency_dict = {
  0: [1, 2, 3],
  1: [3],
  2: [1, 3, 4],
  4: [3],
 },
 vertex_coloring = [
  set([3]),
  set([0, 1, 2, 4]),
 ],
)
>>> autgrp(g)
([[1, 0, 2, 3, 4]], 2.0, 0, [0, 0, 2, 3, 4], 4)
>>>
```

## Installation

### Installing from [PyPi](https://pypi.org/project/pynauty/)

You can install `pynauty` using `pip`, just type

```bash
pip install --upgrade pynauty
```

Many binary wheels are provided for recent Linux and macOS systems.

OS/Platform | py3.7 | py3.8 | py3.9 
------------|:-----:|:-----:|:-----:
Ubuntu-20.04/Debian <br/> and derivatives <br/> x86_64 | X | X | X
Archlinux/Manjaro <br/> x86_64 |  |  | X
macOS 10 <br/> x86_64 | X | X | X
macOS 11 <br/> x86_64 |  |  | X

When your system is not compatible with any of the provided binary
wheels `pip` attempts to build the wheel of the extension module on your
local machine. It assumes that the required tools are installed.

## Documentation

The `pynauty` package comes with an HTML documentation, API and User's Guide.
You can read it with your favorite browser:

```bash
<your-browser>  <path-to-installed-package>/pynauty/docs/html/index.html
```

### Building manually from sources

#### Requirements

Apart from Python the requirements are the same as for building Nauty.

- Python 3.7 - 3.9
- An ANSI C compiler 
- GNU autoconf
- GNU make

#### Download sources

You can download the source distribution form
[PyPi](https://pypi.org/project/pynauty/) by issuing:

```bash
pip download --no-binary pynauty pynauty
```

Please note, the source distribution also contains Nauty27r1's source.

#### Build, test, install

To build and test the package first without installing it anywhere just type:

```bash
make tests
```

Here is how to create a virtualenv and install `pynauty` into it.

```bash
% make virtenv-create
python3 -m venv .venv-pynauty
Created virtualenv: .venv-pynauty
To activate it type: source ./.venv-pynauty/bin/activate
% source .venv-pynauty/bin/activate
(.venv-pynauty) % make install
...
```

You can install `pynauty` into an already existing virtualenv just skip
the creation step above and activate your own virtualenv.

```bash
% source /.../my-virtenv/bin/activate
(my-virtenv) % make install
...
```

If `make install` is invoked outside of a virtualenv that will install
`pynauty` in `~/.local` (home install).

The Makefile is self-documenting in the sense that invoking `make`
without arguments will list all available targets with short
explanations.

## Contributing

Questions, bug reports, pull requests are welcome. Please, open an issue
first to discuss what you would like to change.

Pull requests must be made on a dedicated `topic-branch` of your choice
and not against `upstream/main`.  Before submitting a pull request, make
sure that your fork is up to date with upstream. Also update tests,
documentation, examples as appropriate with the changes in your PR. 

## License

Pynauty is distributed under the terms of GPL v3 WITHOUT ANY WARRANTY.
For the exact details on licensing see the file `COPYING`.

Please note, Nauty is covered by its own licensing terms. For the exact
details see the file `src/nauty27r1/COPYRIGHT`.
