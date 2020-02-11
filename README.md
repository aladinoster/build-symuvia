# Build SymuVia

![](https://img.shields.io/badge/platform-osx--64-blue) 

A simple project structure to Build `SymuVia`. 

1. Get the repo 
  `git clone https://github.com/aladinoster/build-symuvia.git && cd build-symuvia`
2. Place the source Code from `SymuCore` and `SymuVia` inside the `SymuCore/src` and `SymuVia/src`  respectively. 
3. Create the directory to build e.g `mkdir build`
4. Go to the coresonding directory `cd build` 
5. Generate config pointing to the place where the file `CMakeLists.txt` is placed `cmake ..`
6. Build your target via `cmake -build .`