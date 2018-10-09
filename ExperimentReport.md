## SecondDemo实验报告

姓名：王刚

学号：16020031075

#### 实验过程：

1. 在源程序目录下新建data文件夹，用于存放数据图片和结果图片。把gdal文件夹和gdal_i.lib拷贝到项目目录下，把gdal18.dll拷贝到Release文件夹下。然后在代码块中添加如下代码：

2. ```c++
   #include "./gdal/gdal_priv.h"
   #pragma comment(lib, "gdal_i.lib")
   ```

   输入输出图像路径：

   ![1539060832748](https://github.com/Histra/SecondDemo/blob/master/1539060832748.png)

3. 创建Output1.tif和Output2.tif，然后声明一个临时变量Temp并为之分配内存，用该变量实现复制Input.jpg到Output1.tif和Output2.tif。这一过程和FirstDemo实验大同小异。最后一定要使用CPLFree()函数清除Temp临时变量！

   核心代码展示：

   ![1539060984647](https://github.com/Histra/SecondDemo/blob/master/1539060984647.pngg)

4. 任务一：把图像指定区域的红色通道置为255
   任务描述：把输入图像中起始点（100，100），宽度为200像素，高度为150像素的区域红色通道置为255。

5. 任务一实现思路：

    利用GDAL中的GetRasterBand()函数得到图像的通道：

    GetRasterBand(1)得到的是红色通道；

    GetRasterBand(2)得到的是绿色通道；

    GetRasterBand(3)得到的是蓝色通道。

    那么获取红色通道就可以使用GetRasterBand(1)，然后使用Raster()函数读取Input.jpg中的起点（100，100），宽度为200像素，高度为150像素的区域，并将其赋值给临时变量buffTmp；遍历buffTmp，将其每一处都赋值成(GByte)255，即把红色通道中的每一个值都变成最大值（通常，三基色的每个数值也是在0到255之间，0表示相应的基色在该像素中没有，而255则代表相应的基色在该像素中取得最大值）。在这个过程中要注意对图像横纵坐标的理解和转化；最后，再次使用Raster()函数将buffTmp写入到输出图像poDstDs1的红色通道中。
      核心代码展示：

   ![1539061718278](https://github.com/Histra/SecondDemo/blob/master/1539061718278.png)

6. 任务一结果展示：

   打开data文件夹：
      ![1539062733325](https://github.com/Histra/SecondDemo/blob/master/1539062726091.png)

   打开OutPut1.tif文件(截图，非截图在data文件夹下)：

   ![Output1](https://github.com/Histra/SecondDemo/blob/master/data/Output1.tif)

7. 任务2：把图像指定区域置为白色和黑色
   任务描述：把输入图像中起始点（300，300），宽度为100像素，高度为50像素的区域置为白色，同时，把输入图像中起始点为（500，500），宽度为50像素，高度为100像素的区域置为黑色。

8. 任务二思路：
   对于将特定区域置为白色的任务：我们知道，红黄蓝三色混合以后就是白色，即只需要将红黄蓝三个颜色通道中的值均置为255，便可把该区域置为白色。那么，先重置初始位置坐标和区域宽度高度，然后遍历三个颜色通道，对于每一个颜色通道执行和任务一类似的操作，即对于每一个颜色通道，先将图片特定部分读入buffTmp中，然后把buffTmp中的值置为最大值255，然后再写入poDstDs2中。这样就实现了把图像指定区域置为白色的任务了。

   核心代码展示：![1539071300807](https://github.com/Histra/SecondDemo/blob/master/1539071300807.png)

   对于将特定区域置为黑色的任务：此任务和置白的任务大同小异，我们知道，只需要将红黄蓝三个颜色通道中的值均置为0，便可把该区域置为黑色。那么，再次重置起始位置坐标和指定区域的宽度和高度，然后遍历三个颜色通道，对于每一个颜色通道，先将图片特定部分读入buffTmp中，然后把buffTmp中的值置为最小值0，然后再写入poDstDs2中。这样就实现了把图像指定区域置为黑色的任务了。

   注意：一定要清除内存！

   核心代码展示：![1539092560706](https://github.com/Histra/SecondDemo/blob/master/1539092560706.png)

9. 任务二结果展示：
   打开Output2.tif文件(截图，非截图在data文件夹下)：![1539092728024](https://github.com/Histra/SecondDemo/blob/master/1539092728024.png)

10. 
11. 
12. 

