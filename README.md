# apollo-clang-toolchain
Bazel toolchain to compile LGSVL apollo 5.0 with clang.

Requirements:
- GCC 4.9
- clang 6.0 in /apollo/clang

Installation:
- Add this to your WORKSPACE:
```
git_repository(
    name = 'apollo_clang_toolchain',
    remote = 'https://github.com/sera-sch/apollo-clang-toolchain',
    tag = 'latest',
)
```
- Install GCC 4.9 (avaliable on Ubuntu toolchain PPA):
```sh
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get install g++-4.9
```
- Download chromium's clang build
```sh
cd /apollo
mkdir clang
cd clang
wget https://commondatastorage.googleapis.com/chromium-browser-clang/Linux_x64/clang-321529-2.tgz
tar xzvf clang-321529-2.tgz
```
- Build with `--crosstool_top=@apollo_clang_toolchain//clang:toolchain`

References:
- https://github.com/vsco/bazel-toolchains (Apache 2.0)
- https://github.com/baiduxlab/apollo/tree/master/tools/clang-6.0 (Apache 2.0)
