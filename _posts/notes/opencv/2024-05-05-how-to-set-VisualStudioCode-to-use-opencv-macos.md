---
layout: post
title: "How to configure C++ environment of opencv in Visual Studio Code - macOS"
date: 2024-05-05 12:00:10 +0900
categories: [notes, opencv]
tags: [howToX, opencv, vsc, c++]
img_path: /imgs/opencv/202405/
permalink: /:categories/1

---

## List to do
1. [Install Visual Studio Code](#1-install-visual-studio-code)
2. Configure C++ compile environment **🔗**  **tasks.json**
3. Configure C++ debug environment **🔗**  **launch.json**
4. Install opencv package
5. Configre opencv environment  **🔗**  **c_cpp_properties.json**
	1. Set pkg-config
	2. Set pkg-config PATH
	3. **Compiling source codes by refering opencv pakage**

>As a result of experiencing set up the environment, Xcode is easier than VSC...
{: .prompt-tip }

[How to configure the environment of opencv in Xcode][ref-article1]

However, since VSC (Visual Studio Code) has advantages of ease of use and lightness, I've worked hard to organize the setting method. Also, using VSC seems to increase productivity by simply pasting a pre-set file into a project, without configuring cumbersome settings for each project.

---

## **1. Install Visual Studio Code**

Select one of the following to install visual studio code.

①　Installation using [`brew`][link-brew](Open a terminal, enter following command)

```bash
brew install --cask visual-studio-code
```

②　Download [VSC][link-VSCdownload] installation file and install it.

## **2. Configure C++ compile environment 🔗 tasks.json**
## **3. Configure C++ debug environment 🔗  launch.json**

You can find the contents of #2 and #3 in the article below.

>will be migrated on this blog soon.
{: .prompt-tip }
[How to set the environment of C++ compiling and debugging in Visual Studio Code - macOS][ref-article2]

<br>

## **4. Install opencv package**
Installing and setting at once through the brew.

```bash
brew install opencv
```

installed on following directory if you enter the command above.

`/usr/local/Cellar/opencv/`

<br>

## **5. Configre opencv environment 🔗 c_cpp_properties.json**

### **5.0 Pre-works**

- **`c_cpp_properties.json` file :**
	- supports additional features of C/C++ Intelligence extensions
	- lets you specify a standard version of the C++
	- add a relative path to refering particular header files for opencv packages
	- how to create the file : select "C/C++: Edit Configurations (UI)" from the pull-down menu with the following shortcuts

```
(command key) + (Shift key) + P 
```

![vsc-c/c++-configure-menu][ref-img1]
_c/c++ configure menu on Visual studio code_

<br>

If you select `C/C++: Edit Configurations (UI)`, the following window will appear, where you can assign `includePath`, `compiler Path`, `C++ standard version` and etc. By adding the path of installed package on `includePath`, You can refering it in your project, such like "~/opencv4".

![vsc-contents-of-json-file][ref-img2]
_Specifying c/c++ environment, json-way_

<br>

- **📓 c_cpp_properties.json (working fine with this combination..LOL😎)**  

```json
{
    "configurations": [
        {
            "name": "Mac",
            "includePath": [
                "${workspaceFolder}/**",
                "/usr/local/Cellar/opencv/4.5.1_2/include/opencv4"
            ],
            "defines": [],
            "macFrameworkPath": [],
            "compilerPath": "/usr/bin/g++",
            "cStandard": "c11",
            "cppStandard": "c++11",
            "intelliSenseMode": "macos-clang-x64"
        }
    ],
    "version": 4
}
```
<br>
### **5.1 Set pkg-config ⚙️**

This is a little cumbersome work, once you want to use opencv feature with C++, especially when you need to refering specific library of opencv, I recommend this way to configure it to use. 

Alright, in order to refering them, I used `pkg-config`.
It helps compiling process by refering considered libraries.

- **how to install `pkg-config` through brew**

```bash
brew install pkg-config
```

- **completed the installation**

Then, you can use `pkg-config`, and please make sure if it is well installed in the path below.
(the path could be differed depend on its version and intended user operation.)

```bash
/usr/local/Cellar/pkg-config/0.29.2_3/bin/pkg-config
```

- **opencv4.pc file, for refering several librareis**

If you install opencv with the brew command, a folder related to pkgconfig will be installed along with the opencv installation path, which will have a pc extension file in the form of opencv4.pc. (In my case, The installation version was 4.5.1, so the pc file name contains the number four.)

```bash
/usr/local/Cellar/opencv/4.5.1_2/lib/pkgconfig/opencv4.pc
```
![opencv4.pc file][ref-img3]
_inside of opencv4.pc file_

Now `pkg-config` can refer to `IncludePath` of opencv and (multiple) dynamic libraries as an argument by this pc file, but still `pkg-config` cannot be called globally, so let's set PATH globally.

<br>
### **5.2 Set pkg-config PATH ⚙️**

The idea is setting the path of the environment variable.(just like we usually do) The variable name for `pkg-config` is `PKG_CONFIG_PATH`, and make sure assigning it to the path where the opencv4.pc file located. I typed a line into the `.zshrc` file in the root directory (because the writer is using `Oh-my-zsh`.) for permanent assignment.

```bash
export PKG_CONFIG_PATH=/usr/local/Cellar/opencv/4.5.1_2/lib/pkgconfig
```
**Let's echo if it is well assigned.**
```bash
echo $PKG_CONFIG_PATH
```

<br>
### **5.3 Compiling source codes by refering opencv pakage ⚙️**

Once the setup is complete up, you should check if referring libraries work properly. Please enter the command below at the terminal. String of `opencv4` in below command should be same with the pc extension file name.

```bash
pkg-config opencv4 --libs --cflags opencv4
```

**Result of entering `pkg-config` command**

![list of referring libraries by pkg-config][ref-img4]
_list of referring libraries by pkg-config_

## **Testing**

Then, I created a cpp file and tested if compiling with the opencv packages works fine.
Please prepare any image file in the project folder for the test.
In my case, I made a folder and put an image like this, `data_src/elon.png`.

![testing compile process][ref-img5]{: w="300" h="300" }
_ready to compile process_
![elon][ref-img6]{: w="300" h="300" }
_sample image : elon.png_

### **main.cpp for testing. (RGB to Gray Scale image)**

```c++
#include <iostream>
#include <stdlib.h>
#include <stdio.h>
#include <opencv2/imgcodecs.hpp>
#include <opencv2/imgproc.hpp>
#include <opencv2/highgui.hpp>

using namespace std;
using namespace cv;

Mat src, dst, src_gray;

int main()
{
    int rtn = 0;

    src = imread("data_src/elon.png");
    cout << "test" << endl;

    cvtColor(src, src_gray, COLOR_RGB2GRAY);
    imshow("imgGRAY", src_gray);

    rtn = waitKey(0);
    if (rtn == 27)
    {
        return 0;
    }

    return 0;
}
```

And, for compiling, type the following in the terminal

```bash
g++ -std=c++11 `pkg-config opencv4 --libs --cflags opencv4` main.cpp -o output
```

![Compiled with std version of c++11][ref-img7]
_Compiled with std version of c++11_

I named the executable file as `output`. If you run the file, you can see that the image has been changed to gray one.
(Enter esc to exit the window)

![the result of executing output file.][ref-img8]
_the result of executing output file_

I have confirmed that OpenCV package works properly up to this point.
However, if you have to write down a lot of options every time when you build your application, just like `pkg-config`, `cflags`, and blahblahblah.. there is no reason you have to use VSC.

Luckily, we have a `tasks.json` file to reduce our effort to run and compile the application. You can write it down by dividing the parameters by space. Then, you can modify or delete some of the details, and you don't have to remember commands or type them on the keyboard every time. Just press `command + shift + B`(mac).

### **The tasks.json file that modified for my usage...**

```json
{
	"version": "2.0.0",
	"tasks": [
		{
			"type": "cppbuild",
			"label": "C/C++: g++ 활성 파일 빌드",
			"command": "/usr/bin/g++",
			"args": [
				// 기존의 기본 매개변수 구성.
				//"-g",
				// "${file}",
				// "-o",
				// "${fileDirname}/${fileBasenameNoExtension}",
				//

				"-std=c++11",
				"`pkg-config",
				"opencv4",
				"--libs",
				"--cflags",
				"opencv4`",
				"${file}",
				"-o",
				"${fileDirname}/${fileBasenameNoExtension}"
			],
			"options": {
				"cwd": "${workspaceFolder}"
			},
			"problemMatcher": [
				"$gcc"
			],
			"group": "build",
			"detail": "compiler: /usr/bin/g++"
		}
	]
}
```

### **final, Completed the build 🚀**
![final, Completed the build][ref-img9]

If you're macOS user, you can set up the opencv environement in a relatively easy way in Xcode. 
However, if you prefer to use VSC, you should try this. 
The overall processes of this article is based on [here][link-reference1] as a reference.

<!-- link and imgs -->
[ref-article1]: https://fwanggu-lee.tistory.com/10
[ref-article2]: https://fwanggu-lee.tistory.com/16

[ref-img1]: 1.png
[ref-img2]: 2.png
[ref-img3]: 3.png
[ref-img4]: 4.png
[ref-img5]: 5.png
[ref-img6]: 6.png
[ref-img7]: 7.png
[ref-img8]: 8.png
[ref-img9]: 9.png

[link-brew]: https://brew.sh/
[link-VSCdownload]: https://code.visualstudio.com/download
[link-reference1]: https://programmer.ink/think/mac-environment-install-vscode-debugging-c-program.html