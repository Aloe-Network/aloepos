# Aloe Proof of Space

![Alt text](https://www.aloecoin.org/s/aloe_logo.png)

![Build](https://github.com/Aloe-Network/aloepos/workflows/Build/badge.svg)
![PyPI](https://img.shields.io/pypi/v/aloepos?logo=pypi)
![PyPI - Format](https://img.shields.io/pypi/format/aloepos?logo=pypi)
![GitHub](https://img.shields.io/github/license/Aloe-Network/aloepos?logo=Github)

[![Total alerts](https://img.shields.io/lgtm/alerts/g/Aloe-Network/aloepos.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/Aloe-Network/aloepos/alerts/)
[![Language grade: Python](https://img.shields.io/lgtm/grade/python/g/Aloe-Network/aloepos.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/Aloe-Network/aloepos/context:python)
[![Language grade: C/C++](https://img.shields.io/lgtm/grade/cpp/g/Aloe-Network/aloepos.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/Aloe-Network/aloepos/context:cpp)

Aloe's proof of space is written in C++. Includes a plotter, prover, and
verifier. It exclusively runs on 64 bit architectures. Read the
[Proof of Space document](https://www.chia.net/assets/Chia_Proof_of_Space_Construction_v1.1.pdf) to
learn about what proof of space is and how it works.

## C++ Usage Instructions

### Compile

```bash
# Requires cmake 3.14+

mkdir -p build && cd build
cmake ../
cmake --build . -- -j 6
```

### Run tests

```bash
./RunTests
```

### CLI usage

```bash
./ProofOfSpace -k 25 -f "plot.dat" -m "0x1234" create
./ProofOfSpace -k 25 -f "final-plot.dat" -m "0x4567" -t TMPDIR -2 SECOND_TMPDIR create
./ProofOfSpace -f "plot.dat" prove <32 byte hex challenge>
./ProofOfSpace -k 25 verify <hex proof> <32 byte hex challenge>
./ProofOfSpace -f "plot.dat" check <iterations>
```

### Benchmark

```bash
time ./ProofOfSpace -k 25 create
```


### Hellman Attacks usage

There is an experimental implementation which implements some of the Hellman
Attacks that can provide significant space savings for the final file.


```bash
./HellmanAttacks -k 18 -f "plot.dat" -m "0x1234" create
./HellmanAttacks -f "plot.dat" check <iterations>
```

## Python

Finally, python bindings are provided in the python-bindings directory.

### Install

```bash
python3 -m venv .venv
. .venv/bin/activate
pip3 install .
```

### Run python tests

Testings uses pytest. Linting uses flake8 and mypy.

```bash
py.test ./tests -s -v
```

## ci Building
The primary build process for this repository is to use GitHub Actions to
build binary wheels for MacOS, Linux (x64 and aarch64), and Windows and publish
them with a source wheel on PyPi. See `.github/workflows/build.yml`. CMake uses
[FetchContent](https://cmake.org/cmake/help/latest/module/FetchContent.html)
to download [pybind11](https://github.com/pybind/pybind11). Building is then
managed by [cibuildwheel](https://github.com/joerick/cibuildwheel). Further
installation is then available via `pip install aloepos` e.g.

## Contributing and workflow
Contributions are welcome and more details are available in aloe-blockchain's
[CONTRIBUTING.md](https://github.com/Aloe-Network/aloe-blockchain/blob/main/CONTRIBUTING.md).

The main branch is usually the currently released latest version on PyPI.
Note that at times aloepos will be ahead of the release version that
aloe-blockchain requires in it's main/release version in preparation for a
new aloe-blockchain release. Please branch or fork main and then create a
pull request to the main branch. Linear merging is enforced on main and
merging requires a completed review. PRs will kick off a GitHub actions ci build
and analysis of aloepos at
[lgtm.com](https://lgtm.com/projects/g/Aloe-Network/aloepos/?mode=list). Please
make sure your build is passing and that it does not increase alerts at lgtm.
