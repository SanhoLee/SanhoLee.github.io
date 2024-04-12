---
layout: post
title:  "Coordinates Drawer by image processing."
date:   2024-01-27 11:50:33 +0900
categories: Project CV
permalink: /:year/:month/:title
img_path: /imgs/pjt/cv/edgeToCoordinates/
---

## Preview 

**Overall appearance and potential usage.**
![overallAppearance](overall_appearance_and_result.png)


**Available  mouseEvent - cutting img**
![mouse_imgCut](mouseEvent_imgCut.gif)
_cutting img by selecting 2 points rectangle-shape of ROI_

**Available  mouseEvent - masking img**
![mouse_imgMask](mouseEvent_imgMask.gif)
_masking specific area by selecting points_


## **Prologue🤔**

While studying OpenCV, I received a request from my company for a data processing program using image data. When I heard the detailed explanation, it seemed like there was nothing I couldn't do. This was because it involved simple image processing logic that could be solved without the involvement of machine learning.

However, there are certain parts that regular users have to use, so I had to design the GUI. Most of the available blogs or tutorials out there focused mainly on handling images in a console format, and there was actually a lack of information on developing applications for general users who have no knowledge of image processing.

After searching for a few examples, it was found that the main languages that can be used with the OpenCV library are indeed C++ and Python, and C# is also supported. Fortunately, C# has the advantage of being a .NET language, allowing the use of Window Forms. It was also discovered that there is a dedicated library called OpenCvSharp. 

 [GitHub - shimat/opencvsharp: OpenCV wrapper for .NET][1]

There is a platform called emguCV that allows development in a slightly wider range of languages. However, I found it a bit difficult to use, so I didn't pursue it. If given the opportunity, it would be interesting to take a closer look at how to develop using C++ (though that may be a future endeavor).

 [emgucv - computer vision technology company focused on providing industry leading software to solve real world problems.][2]

I have concluded that if you need to write a program that is simple yet fast, using C# is sufficient. And, out of the blue, I compared the trends of the two mentioned platforms using Google Trends search.

**Search Period : 2020.1.1~2022.4.30**

![1](1.png)
_Google Trends search results.(OpenCvSharp vs EmguCV)_

Even if we consider the entire world, neither platform had a significantly high search volume. However, when considering only the average values, it seems that choosing OPENCVSHARP was a good decision as it showed a slight increase.

## **Regional comparative analysis results.🌏📊**

![2](2.png)
_Google Trends search results (regional breakdown)_

I have a suspicion that what I searched for might have been reflected in Japanese statistics (in Osaka, Japan). Since I have actually searched quite a lot, I wonder if it's possible. Anyway, in Korea, it is the second highest search volume, followed by the United States.

I was curious why the search volume is smaller than expected, so I checked the trend with the word OpenCV and indeed, OpenCV is the main one.

![3](3.png)
_Google Trends search results(+OpenCV)_

As a pastime, I checked the trends. It seems like I should search and think more about creating programs with OpenCV or how to apply it in actual applications.

## **Development Environment⚙️👨‍💻**

-   OS : Windows 11
-   IDE : Visual Studio 2023
-   Languages : C#

## **Order of image processing and key functions**🛠️**🖼️**

**\[ Order of image processing \]**

1.  Load a image file
2.  Cut target area of the image.
3.  Mask noise area(unnecessary area)
4.  Calculate CannyEdge pixels(Gaussian Blur had done as blur processing)
5.  Save the detected pixel locations data.

**\[ Key functions \]**

1) Mouse event functionality🖱️

-   Edit the image using the user's mouse input.(How to use a callback function is **[here][3]**)
-   Crop Function: Select the top left and bottom right corners to crop the working area (2 Points)
-   Noise Masking Function: Select points in a clockwise or counterclockwise direction to define the masking area of a polygon. (4 points)
-   Common rule: To confirm and process the selected area, click the middle button of the mouse (the color of the selected element will change), and then press the space bar (a message box will pop up to determine if the process should proceed).

2) Calculate CannyEdge functionality🧮

-   The user can configure the parameters required for the calculation of the canny edge.
-   You can update each parameter using a separate Window form.
-   Changeable parameters : 
    1.  Kernel size k for Gaussian Blur (setting the row and column sizes to be the same)
    2.  The low and high threshold values of CannyEdge

![4](4.png)
_Setting CannyEdge Parameters_

## **Structure of a Window form (entry, main)📃**

-   entry form
-   caseA form(main form)
-   Parameter configuration form

![5](5.png)
_Form of entry (entry form)_

![6](6.png)
_Form of caseA (main form)_

#### _**[Details of the code(Github) ⚙️][4]**_

## **Something I want to try next time.🚀**

While studying image processing and computer vision, I understood how it works with console applications, but I had a lot of vague ideas about how to apply it as an application that actual users can use.

Through developing a desktop application to some extent, I was able to understand the underlying principles of the bigger picture. By utilizing this experience to the fullest, I am now considering shifting my development focus towards creating web-based applications. I believe that this direction not only allows for connectivity with a diverse range of users but also significantly enhances practical usability. (Whether it's a web app or a mobile app...)

In summary, one objective is to develop a computer vision application that operates on the web. Secondly, it seems like I aim to utilize algorithms using machine learning, rather than simple image processing, within the scope of computer vision. Among them, It would be good to consider how to integrate well-known algorithms such as YOLO (Object Detection and Classification) and Unet (Semantic Segmentation) into an application. Let's go for it!


[1]: https://github.com/shimat/opencvsharp
[2]: https://github.com/emgucv
[3]: https://fwanggu-lee.tistory.com/48
[4]: https://github.com/SanhoLee/IMGPROCAPP_WINDESKTOP