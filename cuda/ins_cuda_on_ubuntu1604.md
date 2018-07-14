# Ubuntu 16.04 安装 CUDA

帮某人配 OpenCL 环境，安装 CUDA，路途坎坷，记点笔记。

外星人配置：GeForce 590，确实有点老了啊。

 下载CUDA：[https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads)  
 Quick Start Guide  [https://docs.nvidia.com/cuda/cuda-quick-start-guide/index.html](https://docs.nvidia.com/cuda/cuda-quick-start-guide/index.html)  
 Installation Guide Linux [https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html)  
主要有 runfile 和 deb 两种方式。虽说官方文档建议能 deb 就 deb，不过 deb 的方式无法选择具体装哪些组件，反正最后我失败了，还是用的 runfile。

还是得按照官方文档一步步来，这里只是记录部分步骤：

1. 清理
````
Use the following command to uninstall a Toolkit runfile installation:
$ sudo /usr/local/cuda-X.Y/bin/uninstall_cuda_X.Y.pl
Use the following command to uninstall a Driver runfile installation:
`$ sudo /usr/bin/nvidia-uninstall
Use the following commands to uninstall a RPM/Deb installation:
$ sudo apt-get --purge remove <package_name>          # Ubuntu
补充：
sudo apt-get --purge remove nvidia-*
````

2. 下载  
先将所下载的 runfile 文件添加可执行权限，然后`./cuda_9.2.148_396.37_linux.run --extract=~/downloads/extract`，可以提取出三个文件：驱动，CUDA，CUDA-samples。当然也可以不提取，直接安装，会让你选择是否安装这几个部分。这里提取只是为了看清楚里面的东西。
```
9.2/
├── cuda_9.2.148_396.37_linux.run
└── extract
    ├── cuda-linux.9.2.148-24330188.run
    ├── cuda-samples.9.2.148-24330188-linux.run
    └── NVIDIA-Linux-x86_64-396.37.run
```
因为显卡版本较老，runfile 里带的驱动竟然太新了不支持，只好去官网 [https://www.geforce.com/drivers](https://www.geforce.com/drivers) 单独下载 `NVIDIA-Linux-x86_64-390.67.run`
但是驱动降级了之后，CUDA竟然又不支持了，没变法，最后用的下载的`CUDA Toolkit 8.0 GA2` 配合这个驱动。

3. 安装依赖  
我也不知道应不应该，参考自 [https://gist.github.com/wangruohui/df039f0dc434d6486f5d4d098aa52d07](https://gist.github.com/wangruohui/df039f0dc434d6486f5d4d098aa52d07)
```
sudo apt-get install build-essential gcc-multilib dkms xorg xorg-dev
```

4. 禁用 Nouveau  
创建文件 `/etc/modprobe.d/blacklist-nouveau.conf`，内容如下：
```
blacklist nouveau
options nouveau modeset=0
```
Regenerate the kernel initramfs:
```
$ sudo update-initramfs -u
```
重启

5. 在 TTY 中安装  
CTRL+ALT+F1 然后登陆  
先禁用 lightdm
```
sudo service lightdm stop
```
安装驱动：
```
sudo ./NVIDIA-Linux-x86_64-390.67.run
install opengl library? No
Update the Xserver config? Yes
```
安装 CUDA，注意不要安装驱动了，刚刚已经安装过了
```
sudo ./cuda-linux64-rel-8.0.61-21551265.run
Accept the EULA
Install the driver? No
Install CUDA? Yes
Install the CUDA samples? Yes
```

6. 后序工作  
可能需要：参考自：[http://www.markbuckler.com/post/install-cuda/](http://www.markbuckler.com/post/install-cuda/)
```
sudo apt-get install nvidia-modprobe
```
更新 PATH：
```
export PATH=/usr/local/cuda-9.2/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-9.2/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
简单检测：
```
cat /proc/driver/nvidia/version
nvidia-smi
nvcc -V
```
深度检测：  
cd 到 `~/NVIDIA_CUDA-9.2_Samples`, 键入`make`. 编译出来的可执行文件在 `~/NVIDIA_CUDA-9.2_Samples/bin`
运行：
```
./bin/x86_64/linux/release/deviceQuery
./bin/x86_64/linux/release/bandwidthTest
```
