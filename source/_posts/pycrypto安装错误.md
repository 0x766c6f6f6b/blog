Python 3.7 使用 pip install 安装 pycrypto 失败，错误信息是一堆 缺少 {、缺少; 之类的错误。
![](vx_images/418010117238571.png)
本来想直接下载预编译的 pycrypto 来安装的，但是找了一圈，pycrypto2.6.1 + python3.7 的根本没有，最新好像只到 python3.3。

那就只能手动编译安装了。

可以只安装visual studio生成工具
应该只需要勾选 C++ 开发套件，加一个 Win10 的 SDK 就够了。

打开 VS 的安装文件夹，在 VC – Tools – MSVC – version – include 下面找到 stdint.h 文件，例如，**C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Tools\MSVC\14.21.27702\include**。
具体版本号可能存在差异，但是位置是差不多的
将 stdint.h 文件复制到 SDK 的 include – ucrt 文件夹下，例如 C:\Program Files (x86)\Windows Kits\10\Include\10.0.17763.0\ucrt。

在 ucrt\ 文件夹下找到 inttypes.h，大概 13 行，修改 #include <stdint.h> 为 #include "stdint.h"。

重新执行 pip install pycrypto。