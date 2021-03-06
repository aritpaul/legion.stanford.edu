---
layout: page
permalink: /starting/index.html
title: Getting Started 
---

## Dependencies

To get started with Legion, you'll need:

  * Linux, macOS, or another Unix
  * A C++ 98 (or newer) compiler (GCC, Clang, Intel, or PGI) and GNU Make
  * *Optional*: Python 2.7 (used for profiling/debugging tools)
  * *Optional*: CUDA 5.0 or newer (for NVIDIA GPUs)
  * *Optional*: [GASNet](https://gasnet.lbl.gov/) (for networking, see
     [installation instructions](/gasnet/))
  * *Optional*: LLVM 3.5 (for dynamic code generation)
  * *Optional*: HDF5 (for file I/O)

## Installing

Download Legion from [Github](https://github.com/StanfordLegion/legion):

{% highlight bash %}
git clone https://github.com/StanfordLegion/legion.git
{% endhighlight %}

To test, find an example you'd like to try and run `make`. For example:

{% highlight bash %}
export LG_RT_DIR="$PWD/legion/runtime"
cd legion/examples/full_circuit
make
./ckt_sim
{% endhighlight %}

## Contents

The top-level contents of the repository include:

  * `tutorial`: Source code for the [tutorials](/tutorial/).
  * `examples`: Larger examples for advanced programming techniques.
  * `apps`: Several complete Legion applications.
  * `language`: The [Regent programming language](http://regent-lang.org/) compiler and examples.
  * `runtime`: The core runtime components:
      * `legion`: The Legion runtime itself (see `legion.h`).
      * `realm`: The Realm low-level runtime (see `realm.h`).
      * `mappers`: Several mappers, including the default mapper (see `default_mapper.h`).
  * `tools`: Miscellaneous tools:
      * `legion_spy.py`: A [visualization tool](/debugging/#legion-spy) for task dependencies.
      * `legion_prof.py`: A task-level [profiler](/profiling/#legion-prof).

The rest of this page covers how to begin using the
Legion runtime.

## Makefile Variables

The Legion Makefile includes several variables which influence the
build. These may either be set in the environment (e.g. `DEBUG=0
make`) or at the top of each application's Makefile.

  * `DEBUG=<0,1>`: controls optimization level and enables various
    dynamic checks which are too expensive for release builds.
  * `OUTPUT_LEVEL=<level_name>`: controls the compile-time [logging
    level](/debugging/#logging-infrastructure).
  * `USE_CUDA=<0,1>`: enables CUDA support.
  * `USE_GASNET=<0,1>`: enables GASNet support (see [installation instructions](/gasnet/)).
  * `USE_LLVM=<0,1>`: enables LLVM support.
  * `USE_HDF=<0,1>`: enables HDF5 support.

## Build Flags

In addition to Makefile variables, compilation is influenced by a
number of build flags. These flags may be added to the environment
variable `CC_FLAGS` (or again set inside the Makefile).

  * `CC_FLAGS=-DLEGION_SPY`: enables [Legion Spy](/debugging/#legion-spy).
  * `CC_FLAGS=-DPRIVILEGE_CHECKS`: enables [extra privilege checks](/debugging/#privilege-checks).
  * `CC_FLAGS=-DBOUNDS_CHECKS`: enables [dynamic bounds checks](/debugging/#bounds-checks).

## Command-Line Flags

Legion and Realm accept command-line arguments for various runtime
parameters. Below are some of the more commonly used flags:

  * `-level <category>=<int>`:
    sets [logging level](/debugging/#logging-infrastructure) for `category`
  * `-logfile <filename>`:
    directs [logging output](/debugging/#logging-infrastructure) to `filename`
  * `-ll:cpu <int>`: CPU processors to create per process
  * `-ll:gpu <int>`: GPU processors to create per process
  * `-ll:cpu <int>`: utility processors to create per process
  * `-ll:csize <int>`: size of CPU DRAM memory per process (in MB)
  * `-ll:gsize <int>`: size of GASNet global memory available per process (in MB)
  * `-ll:rsize <int>`: size of GASNet registered RDMA memory available per process (in MB)
  * `-ll:fsize <int>`: size of framebuffer memory for each GPU (in MB)
  * `-ll:zsize <int>`: size of zero-copy memory for each GPU (in MB)
  * `-hl:window <int>`: maximum number of tasks that can be created in a parent task window
  * `-hl:sched <int>`: minimum number of tasks to try to schedule for each invocation of the scheduler

The default mapper also has several flags for controlling the default mapping.
See `default_mapper.cc` for more details.

## Tutorials

Now that a working version of Legion has been established we recommend
that users follow the [tutorials](/tutorial/) to begin using Legion.
