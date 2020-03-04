# apollo-clang-toolchain
Bazel toolchain to compile LGSVL apollo 5.0 with clang.

## Requirements
- GCC 4.9
- clang 6.0 in /apollo/clang
- AFL (clang-fast) in /apollo/AFL

## Main installation
- Add this to your WORKSPACE:
```
git_repository(
    name = 'apollo_clang_toolchain',
    remote = 'https://github.com/sera-sch/apollo-clang-toolchain',
    tag = '0.2',
)
```
- Install GCC 4.9 (avaliable on Ubuntu toolchain PPA):
```sh
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get install g++-4.9
```
- Download clang build (example for 14.04)
```sh
cd /apollo
mkdir clang
cd clang
wget http://releases.llvm.org/6.0.0/clang+llvm-6.0.0-x86_64-linux-gnu-ubuntu-14.04.tar.xz
tar xvf clang+llvm-6.0.0-x86_64-linux-gnu-ubuntu-14.04.tar.xz
mv clang+llvm-6.0.0-x86_64-linux-gnu-ubuntu-14.04/* .
rmdir clang+llvm-6.0.0-x86_64-linux-gnu-ubuntu-14.04
rm clang+llvm-6.0.0-x86_64-linux-gnu-ubuntu-14.04.tar.xz
```
- Build with `--crosstool_top=@apollo_clang_toolchain//clang:toolchain`

## Installing AFL
```sh
cd /apollo
git clone https://github.com/google/AFL.git
cd AFL/llvm_mode
PATH=/apollo/clang/bin:$PATH LLVM_CONFIG=/apollo/clang/bin/llvm-config make
```
Build with `--crostool_top=@apollo_clang_toolchain//afl:toolchain`

## References
- https://github.com/vsco/bazel-toolchains (Apache 2.0)
- https://github.com/baiduxlab/apollo/tree/master/tools/clang-6.0 (Apache 2.0)
