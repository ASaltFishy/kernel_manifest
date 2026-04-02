# how to fetch code
``` bash
# 一定要指定 --depth=1 否则安卓和linux的提交历史记录会把流量和存储撑爆！
repo init -u https://github.com/ASaltFishy/kernel_manifest -b oneplus/sm8850 --depth=1 -m oneplus_15.xml
# 相比一加15原来的版本,xml文件已经手动修改过，主要更改：高通codelinra私有代码-->aosp仓库拉取-->用清华aosp镜像可以直接不翻墙拉取代码
repo sync -c --no-tags --no-clone-bundle -j$(nproc)
```

# how to build kernel
``` bash
# ./kernel_platform/oplus/build/oplus_build_kernel.sh canoe perf
cd ./kernel_platform
bash ./setup_env.sh
tools/bazel run --jobs=$(($(nproc) - 2)) //common:kernel_aarch64_dist -- --destdir=./out
```
生成的产物在./out/Image