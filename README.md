N-Dimensional Fast Marching Method V1.0

[Biicode](https://www.biicode.com/) blocks status:

[![Build Status](https://webapi.biicode.com/v1/badges/jvgomez/jvgomez/console/master)](https://www.biicode.com/jvgomez/console)
[![Build Status](https://webapi.biicode.com/v1/badges/jvgomez/jvgomez/ndgridmap/master)](https://www.biicode.com/jvgomez/ndgridmap)
[![Build Status](https://webapi.biicode.com/v1/badges/jvgomez/jvgomez/fmm/master)](https://www.biicode.com/jvgomez/fmm)
[![Build Status](https://webapi.biicode.com/v1/badges/endher/endher/fm2/master)](https://www.biicode.com/endher/fm2)
[![Build Status](https://webapi.biicode.com/v1/badges/jvgomez/jvgomez/fmexamples/master)](https://www.biicode.com/jvgomez/fmexamples)
[![Build Status](https://webapi.biicode.com/v1/badges/jvgomez/jvgomez/fm2examples/master)](https://www.biicode.com/jvgomez/fm2examples)

**Authors:**
 - Javier V. Gomez javvgomez _at_ gmail.com www.javiervgomez.com
 - Jose Pardeiro jose.pardeiro _at_ gmail.com
 - Pablo Gely

## ALGORITHMS
**Fast Marching Methods:**
- [FMM](http://javiervgomez.com/fastmarching/classFMM.html): Fast Marching Method with Binary Queue and Fibonacci Queue.
- [SFMM](http://javiervgomez.com/fastmarching/classFMM.html): Simplified Fast Marhching Method ([FMM](http://javiervgomez.com/fastmarching/classFMM.html) with a simple priority queue).
- [FMM*](http://javiervgomez.com/fastmarching/classFMMStar.html): FMM and SFMM with CostToGo heuristics.

**O(n) Fast Marching Methods:**
- [GMM]((http://javiervgomez.com/fastmarching/classGMM.html): Group Marching Method.
- [UFMM](http://javiervgomez.com/fastmarching/classUFMM.html): Untidy Fast Marching Method.
- [FIM](http://javiervgomez.com/fastmarching/classFIM.html): Fast Iterative Method.

**Fast Sweeping Methods:**
- [FSM](http://javiervgomez.com/fastmarching/classFSM.html): Fast Sweeping Method.
- [LSM](http://javiervgomez.com/fastmarching/classLSM.html): Lock Sweeping Method.

**Other methods:**
- Soon.

**Fast Marching Square motion planning algorithms:**
- [FM2](http://javiervgomez.com/fastmarching/classFM2.html): Fast Marching Square Method.
- [FM2*](http://javiervgomez.com/fastmarching/classFM2Star.html): Fast Marching Square Star FM2 with CostToGo heuristics.

**ROS**

ROS nodes using this code (tested in the TurtleBot) are provided in a separate repo:
https://github.com/jpardeiro/fastmarching_node

**BIICODE**
A version of this code is available at the [biicode](https://www.biicode.com) C/C++ dependency manager. Concretely
the corresponding blocks are:

https://www.biicode.com/jvgomez
jvgomez/console
jvgomez/ndgridmap
jvgomez/fmm
jvgomez/fm2examples

https://www.biicode.com/endher
endher/fm2


## DISCLAIMER and IMPORTANT NOTES

- The code is not deeply tested. I've just tested it works for the cases I need. If you find any problem, have any question (or whatever), please write to: javvgomez _at_ gmail.com

- The compilation time is highly increased due to CImg library. Please, omit it when possible.

- License GNU/GPL V3: http://www.gnu.org/copyleft/gpl.html

- This is a source code intended for my research. Although I want it to be useful for other people it is not intended to act as a library (there are many many points to improve). However, if you show interest or have feature request do not hesitate to contact me and I will try my best to improve the code for whoever needs it. I am also open to contributions and to create a formal library if necessary.


## Documentation

- [API Reference](http://javiervgomez.com/fastmarching/)
- This README is important as well.


To build latest the documentation:

    $ cd doc
    $ doxygen

Go into the HTML folder and open index.html


## Dependencies:

This code uses C\++11 so a compiler g++ 4.8 or equivalent is required. With GCC 4.7 some runtime problems can occur.

### Linking CImg dependencies.
If you want to compile code that uses the CImg library, you will need to add the following line to the CMakeLists.txt

    target_link_libraries (fmm X11 pthread)

The code provides a copy of the CImg library. This will take care of loading and savig images. Depending on the extension used, you will need to install another libraries as said in the main page of CImg: http://cimg.sourceforge.net/

The example code uses png, therefore examples of libraries to be installed are libpng, Magick++, ImageMagick, etc.

### Boost dependencies
When using Ubuntu, you should install Boost libraries (tested with 1.55+):

    sudo apt-get install libboost-all-dev

## Building the code
To build the code:

    $ cd build
    $ cmake .. -DCMAKE_BUILD_TYPE=Release (Release, RelWithDebInf or Debug, Release by default)
    $ make
    $ ./fmm -map1 ../data/testimg.png -map2 ../data/map.png -vel ../data/velocities.png

This main shows most of the utilities implemented so far.

## Folder structure

Although there are a lot of folders, they are quite simple. It is organized this way because I'm focusing on an upload to Biicode (www.biicode.com)

+ build: where the code should be compiled.
+ console: the console class.
+ data: additional files and maps to test.
  + alpha: contains code the be refactorized and included in the library in the future.
+ doc: doxygen documentation.
+ examples: easy examples to understand how to use the code.
+ fm2: Fast Marching Square (FM2) algorithms.
+ fmm: Fast Marching Algorithms.
  + fmdata: classes related to the data types of the Fast Marching Method and other algorithms.
+ gradientdescent: under development.
+ io: input/output helper classes.
+ ndgridmap: main container.
+ scripts: matlab scripts to parse outputs and automatic benchmarking bash script.
+ thirdparty: others' software included.

## KNOWN ISSUES

- Gradient Descent for FM2* could fail if very narrow passages are in the way of the path.

## TODO

At the top of each file there are specific TODO comments. Here are some others:

- Upload as a unique biicode block.
- Review and update nDGridMap.pdf
- Convert all scripts to python (or similar) so that they keep completely open source.
- Improve the way FM2 and its versions deal with the grid when running multiple times on the same grid. Concretely, avoid recomputation of velocities map.
- Reimplement FM2Dir from scratch. Currently in data/alpha folder.
- Restructure the folder and the CMake files in order to properly have examples and that stuff.
- Substitute arg parsing with boost_options.
- Remove relative file dependencies (#include "../../fmm", filename = "../../data", CMakeLists.txt deps, etc).
- Implement a grid copy constructor and assignment operator, etc.
- Most of the unsigned int should be replaced by size_t to be type-correct.
- Use smart pointers (specially for grid).
- Create a testing framework.
- BenchmarkCFG::configure, parse ctorParams_ with a variadic templated function, something like:` parseParams<int, bool>(param1, param2)`, `parseParams<string,double,bool>(p1,p2,p3)`.
- For most methods, neighbors for same cell are computed many times. Store them like FMT to save some computation time.
- GridPlotter code can be refactorized so that the same code is not repeated many times.
- Review template template parameters, perhaps it can be simplified (specially for benchmark): `template <grid_t>` to `template <nDGridMap <cell_t, ndims>>` so we can use cell_t without doing `template <grid_t, cell_t>` (redundant).
