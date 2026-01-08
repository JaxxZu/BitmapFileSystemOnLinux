# BitmapFileSystemOnLinux
Linux系統上基於Bitmap的檔案管理系统  
這是一個在 Linux 作業系統上實現的簡易檔案系統，核心使用 位元圖（Bitmap） 來管理磁碟區塊的分配。  

## 題目要求
在Linux操作系统上，简单地实现一个基于位示图的文件系统  
1. 为了方便文件系统的编写和测试，最好在VMWare虚拟机上实现。
2. Linux操作系统一般都会自带ramdisk设备(/dev/ram)，它能把一部分内存模拟成一个磁盘。所以，在实验的过程中可以使用ramdisk作为块设备，而不需要专门为该文件系统直接创建一个磁盘分区。
3. 文件系统的实现推荐参考Linux内核源代码中minix文件系统的实现方式。它的实现在(Linux内核源码目录/fs/minix/)目录中。
## 需求分析
Implement a simple file system on Linux, where its core functionality relies on a bitmap to manage disk blocks.  
The basic features to be implemented include adding, deleting, renaming, R/W and copying directories or files.  
Additionally, complete functions for initializing the file system and displaying directory contents.  

## 運行環境
Ubuntu 14.04 LTS  
gcc version 4.8.4  
編譯標準：C99  

## 運行結果
```
sudo su
modprobe brd rd_nr=1 rd_size=640
dd if=/dev/zero of=/dev/ram0 bs=512 count=1280
```
Fig. 2.2.1 Shell commands for creating and initializing a RAM disk
<table >
<tr>
  <td><img width="100%" alt="image" src="https://raw.githubusercontent.com/Jaxx9527/BitmapFileSystemOnLinux/refs/heads/main/img/2.2.2.png" />

</tr>
  <tr>
    <td align="center"> 	 Fig. 2.2.2 Creating and initializing the ramdisk via shell commands
  </td>
  </tr>
</table> 
Since this system does not provide a built-in ramdisk device (/dev/ram), the ramdisk is created and initialized using the commands shown in Fig. 2.2.1. The execution result is shown in Fig. 2.2.2.    

<table >
<tr>
  <td><img width="100%" alt="image" src="https://raw.githubusercontent.com/Jaxx9527/BitmapFileSystemOnLinux/refs/heads/main/img/2.3.png" />

</tr>
  <tr>
    <td align="center"> 	 Fig. 2.3 Formatting implementation   </td>
  </tr>
</table>   
Fig. 2.3 show that the ramdisk originally contained data and after performing the format operation, the contents were cleared.  
<table >
<tr>
  <td><img width="100%" alt="Fig. 2.4.1 " src="https://raw.githubusercontent.com/Jaxx9527/BitmapFileSystemOnLinux/refs/heads/main/img/2.4.1.png" />
</td>
  <td><img width="100%" alt="Fig. 2.4.2 " src="https://raw.githubusercontent.com/Jaxx9527/BitmapFileSystemOnLinux/refs/heads/main/img/2.4.2.png" />
</td>
</tr>
  <tr>
    <td align="center">Fig. 2.4.1 Retrieving directory contents (non-empty)    </td>
    <td align="center"> Fig. 2.4.2 Retrieving directory contents (empty) 	</td>
  </tr>
</table>
Fig. 2.4.1 and Fig. 2.4.2 show the execution results of the function for retrieving directory contents when the ramdisk contains data and when it is empty.



<table >
<tr>
  <td><img width="100%" alt="image" src="https://raw.githubusercontent.com/Jaxx9527/BitmapFileSystemOnLinux/refs/heads/main/img/2.5.png" />

</tr>
  <tr>
    <td align="center"> 	  Fig. 2.5 Implementation of creating files and directories   </td>
  </tr>
</table>

Fig. 2.5 shows the directory contents retrieved after creating a file and a directory on the ramdisk.  
<table >
<tr>
  <td><img width="100%" alt="image" src="https://raw.githubusercontent.com/Jaxx9527/BitmapFileSystemOnLinux/refs/heads/main/img/2.6.1.png" />
</td>
  <td><img width="100%" alt="image" src="https://raw.githubusercontent.com/Jaxx9527/BitmapFileSystemOnLinux/refs/heads/main/img/2.6.2.png" />
</td>
</tr>
  <tr>
    <td align="center">Fig. 2.6.1 Implementation of copying files and directories                      </td>
    <td align="center">  Fig. 2.6.1 Implementation of copying files	</td>
  </tr>
</table>

Fig. 2.6.1 shows that the directory contents retrieved after copying a file and creating a directory.
Fig. 2.6.2 shows that after copying the file, its contents were successfully duplicated.

<table >
<tr>
  <td><img width="100%" alt="image" src="https://raw.githubusercontent.com/Jaxx9527/BitmapFileSystemOnLinux/refs/heads/main/img/2.7.1.png" />
</td>
  <td><img width="100%" alt="image" src="https://raw.githubusercontent.com/Jaxx9527/BitmapFileSystemOnLinux/refs/heads/main/img/2.7.2.png" />
</td>
</tr>
  <tr>
    <td align="center">Fig. 2.7.1  Writing to a file </td>
    <td align="center"> 	  Fig. 2.7.2 Reading from a file   </td>
  </tr>
</table>

                                     
Fig. 2.7.1 and Fig. 2.7.2 show the results of writing to and reading from a file.  

<table >
<tr>
  <td><img width="100%" alt="image" src="https://raw.githubusercontent.com/Jaxx9527/BitmapFileSystemOnLinux/refs/heads/main/img/2.8.1.png" />
</td>
  <td><img width="100%" alt="image" src="https://raw.githubusercontent.com/Jaxx9527/BitmapFileSystemOnLinux/refs/heads/main/img/2.8.2.png" />
</td>
</tr>
  <tr>
    <td align="center">Fig. 2.8.1 File deletion </td>
    <td align="center"> Fig. 2.8.2 Directory deletion	</td>
  </tr>
</table>

    		       	 
Fig. 2.8.1 and Fig. 2.8.2 show that the results of deleting a file or a directory.
