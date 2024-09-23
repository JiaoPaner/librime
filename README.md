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

## Build
### boost
```bash
wget https://github.com/boostorg/boost/releases/download/boost-1.84.0/boost-1.84.0.tar.xz
tar -xJf boost-1.84.0.tar.xz
cd boost-1.84.0
./bootstrap.sh
./b2 headers
```
