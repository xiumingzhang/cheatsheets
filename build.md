# General

## Configure

```bash
./configure --prefix=/my/nfs/build/folder

make -j
make install
```

## CMake

```bash
# Inside build folder
cmake /src/folder -DCMAKE_INSTALL_PREFIX=/my/nfs/build/folder

make -j
make install
```

### Passing in lib file, include dir, lib root/home
```bash
-DTIFF_LIBRARY=/tiff_build/lib/libtiff.so \
-DTIFF_INCLUDE_DIR=/tiff_build/include \
-DOPENEXR_HOME=/openexr_build/ \
-DBOOST_ROOT=/boost_1_64_0/
```

### Lib and include dir to search first
```bash
-DCMAKE_LIBRARY_PATH=$SHAPETIME_DIR/software/Anaconda3-4.3.1-Linux-x86_64/lib \
-DCMAKE_INCLUDE_PATH=$SHAPETIME_DIR/software/Anaconda3-4.3.1-Linux-x86_64/include
```



# Specific

## Blender as Python Module

Built on `tuesday` with
```bash
cmake ../blender \
-DWITH_CODEC_SNDFILE=ON \
-DPYTHON_VERSION=3.6 \
-DPYTHON_ROOT_DIR=$SHAPETIME_DIR/software/Anaconda3-4.3.1-Linux-x86_64 \
-DWITH_OPENCOLORIO=ON \
-DOPENCOLORIO_ROOT_DIR=$MOON_DIR/software/blender_deps/build/ocio \
-DOPENEXR_ROOT_DIR=$MOON_DIR/software/blender_deps/build/openexr \
-DWITH_OPENIMAGEIO=ON \
-DOPENIMAGEIO_ROOT_DIR=$MOON_DIR/software/blender_deps/build/oiio \
-DWITH_CYCLES_OSL=ON \
-DWITH_LLVM=ON \
-DLLVM_VERSION=3.4 \
-DOSL_ROOT_DIR=$MOON_DIR/software/blender_deps/build/osl \
-DWITH_OPENSUBDIV=ON \
-DOPENSUBDIV_ROOT_DIR=$MOON_DIR/software/blender_deps/build/osd \
-DWITH_OPENVDB=ON \
-DWITH_OPENVDB_BLOSC=ON \
-DOPENVDB_ROOT_DIR=$MOON_DIR/software/blender_deps/build/openvdb \
-DWITH_OPENCOLLADA=ON \
-DWITH_JACK=ON \
-DWITH_JACK_DYNLOAD=ON \
-DWITH_ALEMBIC=ON \
-DALEMBIC_ROOT_DIR=$MOON_DIR/software/blender_deps/build/alembic \
-DWITH_CODEC_FFMPEG=ON \
-DFFMPEG_LIBRARIES='avformat;avcodec;avutil;avdevice;swscale;swresample;lzma;rt;theoradec;theoraenc;theora;vorbisfile;vorbisenc;vorbis;ogg;xvidcore;vpx;mp3lame;x264;x264;openjpeg' \
-DWITH_PYTHON_INSTALL=OFF \
-DWITH_PLAYER=OFF \
-DWITH_PYTHON_MODULE=ON \
-DFFMPEG=$MOON_DIR/software/ffmpeg_build \
-DCMAKE_INSTALL_PREFIX=$MOON_DIR/software/blender_build \
-DCMAKE_LIBRARY_PATH=$SHAPETIME_DIR/software/Anaconda3-4.3.1-Linux-x86_64/lib \
-DCMAKE_INCLUDE_PATH=$SHAPETIME_DIR/software/Anaconda3-4.3.1-Linux-x86_64/include
```

### Caveats
FFmpeg has to be compiled with `-fPIC`:
```bash
./configure --enable-shared --prefix=$MOON_DIR/software/ffmpeg_build/
```
