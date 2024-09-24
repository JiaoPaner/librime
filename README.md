<meta charset="UTF-8">

Build dependencies
---
  - compiler with C++17 support
  - cmake>=3.12
  - libboost>=1.74
  - libglog>=0.7 (optional)
  - libleveldb
  - libmarisa
  - libopencc>=1.0.2
  - libyaml-cpp>=0.5
  - libgtest (optional)

Runtime dependencies
---
  - libboost
  - libglog (optional)
  - libleveldb
  - libmarisa
  - libopencc
  - libyaml-cpp

## Build dependencies
### boost
```bash
wget https://github.com/boostorg/boost/releases/download/boost-1.84.0/boost-1.84.0.tar.xz
tar -xJf boost-1.84.0.tar.xz
cd boost-1.84.0
./bootstrap.sh
./b2 headers
```

### leveldb
```bash
git clone https://github.com/google/leveldb.git
cd leveldb
mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=OFF -DLEVELDB_BUILD_TESTS=OFF -DLEVELDB_BUILD_BENCHMARKS=OFF -DCMAKE_CXX_FLAGS="-fPIC" .. 
make -j6
```

### marisa
```bash
git clone https://github.com/rime/marisa-trie.git
cd marisa-trie
mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_CXX_FLAGS="-fPIC" .. 
make -j6
```

### opencc
```bash
git clone https://github.com/BYVoid/OpenCC.git
cd OpenCC 
mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=OFF .. 
make -j6
```

### yaml-cpp
```bash
git clone https://github.com/jbeder/yaml-cpp.git
cd yaml-cpp
mkdir build && cd build
cmake -DYAML_CPP_BUILD_CONTRIB=OFF -DYAML_CPP_BUILD_TESTS=OFF -DYAML_CPP_BUILD_TOOLS=OFF -DCMAKE_BUILD_TYPE="Release" .. 
make -j6
```
