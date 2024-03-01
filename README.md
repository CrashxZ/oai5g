# OAI 5G
##OAI 5G - ARM64 Setup instructions
---
###Sources - Configure sources
 ```
   sudo dpkg --add-architecture arm64
   echo -e \
        "deb [arch=arm64] http://mirrors.mit.edu/ubuntu-ports jammy main restricted\n"\
        "deb [arch=arm64] http://mirrors.mit.edu/ubuntu-ports jammy-updates main restricted\n"\
        "deb [arch=arm64] http://mirrors.mit.edu/ubuntu-ports jammy universe\n"\
        "deb [arch=arm64] http://mirrors.mit.edu/ubuntu-ports jammy-updates universe\n"\
        "deb [arch=arm64] http://mirrors.mit.edu/ubuntu-ports jammy multiverse\n"\
        "deb [arch=arm64] http://mirrors.mit.edu/ubuntu-ports jammy-updates multiverse\n"\
        "deb [arch=arm64] http://mirrors.mit.edu/ubuntu-ports jammy-backports main restricted universe multiverse"\
    | sudo tee /etc/apt/sources.list.d/arm-cross-compile-sources.list

  sudo cp /etc/apt/sources.list "/etc/apt/sources.list.`date`.backup"
  sudo sed -i -E "s/(deb)\ (http:.+)/\1\ [arch=amd64]\ \2/" /etc/apt/sources.list
```

``` 

sudo apt install -y gcc-aarch64-linux-gnu \
                    g++-aarch64-linux-gnu


sudo apt-get install -y \
    libatlas-base-dev:arm64 \
    libblas-dev:arm64 \
    liblapack-dev:arm64 \
    liblapacke-dev:arm64 \
    libreadline-dev:arm64 \
    libgnutls28-dev:arm64 \
    libconfig-dev:arm64 \
    libsctp-dev:arm64 \
    libssl-dev:arm64 \
    libtool:arm64 \
    zlib1g-dev:arm64

```
### Install required packeges
```
cd cmake_targets
./build_oai -I
```
### Install USRP
```
sudo apt install libuhd4.1.0
```
### Build LDPC generators
```
cd
cd 
rm -r ran_build
mkdir ran_build
mkdir ran_build/build
mkdir ran_build/build-cross

cd ran_build/build
cmake ../../..
make -j`nproc` ldpc_generators generate_T
```

### RAN Build
```
cd ../build-cross
cmake ../../.. -DCMAKE_TOOLCHAIN_FILE=../../../cmake_targets/cross-arm.cmake -DNATIVE_DIR=../build

make -j`nproc` dlsim ulsim ldpctest polartest smallblocktest nr_pbchsim nr_dlschsim nr_ulschsim nr_dlsim nr_ulsim nr_pucchsim nr_prachsim
make -j`nproc` lte-softmodem nr-softmodem nr-cuup oairu lte-uesoftmodem nr-uesoftmodem
make -j`nproc` params_libconfig coding rfsimulator
```

