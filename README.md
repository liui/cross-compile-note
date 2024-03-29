# cross-compile-script

### 记录几个交叉编译时，常用库的编译指令

cmake toolchain file:

```cmake
SET(buildroot /home/i/armhf)

option(BOOST_NO_AUTO_PTR "boost no auto ptr" ON)

# this is required
SET(CMAKE_SYSTEM_NAME Linux)

# specify the cross compiler
SET(CMAKE_C_COMPILER   arm-linux-gnueabihf-gcc)
SET(CMAKE_CXX_COMPILER arm-linux-gnueabihf-g++)

# where is the target environment 
SET(CMAKE_FIND_ROOT_PATH 
    ${buildroot}/zlib
    ${buildroot}/openssl
    ${buildroot}/boost
    ${buildroot}/curl
    ${buildroot}/cpprest
    /usr/arm-linux-gnueabihf
    )

# search for programs in the build host directories (not necessary)
SET(CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER)
# for libraries and headers in the target directories
SET(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)
SET(CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY)
#SET(CMAKE_FIND_ROOT_PATH_MODE_PACKAGE ONLY)

# configure LIBRARY ROOT
SET(BOOST_ROOT ${buildroot}/boost)
SET(OPENSSL_ROOT_DIR ${buildroot}/openssl)
SET(ZLIB_ROOT ${buildroot}/zlib)
SET(CURL_ROOT ${buildroot}/curl)

if (EXISTS "${buildroot}/cpprest/include/cpprest")
    include_directories(${buildroot}/cpprest/include)
endif()

```
