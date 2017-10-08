### Configure

```
./configure --prefix=/my/nfs/build/folder
make -j
make install
```


### CMake (passing in library file, include dir, lib root/home, make install prefix)

```
# Inside build build
cmake /source/folder -DTIFF_LIBRARY=/tiff_build/lib/libtiff.so -DTIFF_INCLUDE_DIR=/tiff_build/include -DOPENEXR_HOME=/openexr_build/ -DBOOST_ROOT=/boost_1_64_0/ -DCMAKE_INSTALL_PREFIX=/my/nfs/build/folder
make -j
make install
```