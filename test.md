# S14


|References:                                                                                                                 |
| ---------------------------------------------------------------------------------------------------------------------------|
 MiDaS: https://github.com/intel-isl/MiDaS                     
 planercnn: https://github.com/NVlabs/planercnn                    
 [Dataset with helmet, mask, vest, and boots](https://canvas.instructure.com/courses/1968323/discussion_topics/10104950)


|Tasks:                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------| 
 **1.Take your dataset and run it through Midas and get depth images.**  
 **2.Take your dataset and run it through the PlanerCNN model and get planer images** 
 **3.Upload to your google drive with a shareable link and add a GitHub repo that describes the dataset properly.** 

#### This guide would provide a step by step approach to quickly complete the above tasks using **Google Colab**
#### The above repos have been explored individually and in the EVA5 Telegram Group and concisely summarized.


##### Here is the sneak peek
![Alt text](https://github.com/nmeva/S14/blob/main/images/Images.png)


##### Images contains 3590 files, 45 JPEG, 5 PNG AND 3540 JPGs.
##### It would be a good idea to convert the 50 non-JPG images to JPG before we start.


## <u>Task 1:</u>
### Getting Depth Images:

#####
##### The repo is very neatly written and can be used in multiple formats, Pytorch, Docker etc. but I chose to use the plain Python version.
##### Refer to the below screenshot from the repo, these are the only steps that need to be done.
<img src="https://github.com/nmeva/S14/blob/main/images/Midas.png"  width="450">

##### Focus on using Colab, it is a good idea to mount google drive and keep all data including repos
##### in the drive so it is persistent across sessions or vms.

##### Use !wget to download the weights file.

##### After exploring a lot, I found that gdown to be very helpful in copying google drive files to the colab vm.
##### I tried a lot of upload download etc. for exploration but you can use gdown for a quick copy.

##### Use unzip command on colab itself to unzip the files to a folder, rename it to input and follow the steps.
##### The depth map would be generated in the output folder.


##### Here is the link to the [Jupyter Notebook](https://github.com/nmeva/S14/blob/main/images/Midas.png)
##### and [this](https://github.com/nmeva/S14/blob/main/images/Midas.png) is the link to the drive which containts depth maps.



## <u>Task 2:</u>
### Getting Planer Images
##### Issues and Solution:
##### 1.The first issue was that the repo is almost 2 years old and the dependencies were cffi==1.11.5,numpy==1.15.4, opencv-python==3.4.4.19,scikit-image==0.14.1,torch==0.4.1,tqdm==4.28.1
##### Sorting this out on a local machine was time consuming exercise only to understand that Colab is a better option.
##### Following are the changes made.The summary is to downgrade torch to 0.4.0 and install cuda 8 and gcc 5 and once done upgrade it to 0.4.1 and compile nms and roialign.
##### Also, since the GPUs mentioned were dated and Colab provides newer and faster ones, stick to arch=sm_60 worked for most instances

##### + It took a lot of back and forth to get all dependencies to install until @voldy12 and @inocajith made it easy.
##### @inocajith helped with a notebook to run the code on Colab and @voldy12 helped with a script that you could reuse everytime you spun a runtime on Colab.
<a href="https://github.com/nmeva/S14/blob/main/images/planercnn_cuda.sh"> <img src="https://github.com/nmeva/S14/blob/main/images/Planer_Colab.png" width="350"></a>                                                                                                                                                           
##### 2. The output was quite heavy with 9 files thrown for each input image which could easily consume all drive space. Also, the number of images getting processed were restricted to 100 and the output images did not have the input image names.
##### Thanks to Ajith who provided the below modified scripts to get just the required planer image and save the output with the input image name.
##### Also add the argument "--numTestingImages=4000" while running inference to overide the number of processed images.
<a href="https://github.com/nmeva/S14/blob/main/images/visualize_utils.py"> <img src="https://github.com/nmeva/S14/blob/main/images/visualize.png" width="250"></a>


<a href="https://github.com/nmeva/S14/blob/main/images/evaluate.py"> <img src="https://github.com/nmeva/S14/blob/main/images/eval.png" width="250"></a>

##### Here is the link to the [Jupyter Notebook](https://github.com/nmeva/S14/blob/main/images/Midas.png)
##### and [this](https://github.com/nmeva/S14/blob/main/images/Midas.png) is the link to the drive which containts planer images.



## <u>Task 3:</u>
### [this](https://github.com/nmeva/S14/blob/main/images/Midas.png)
### [this](https://github.com/nmeva/S14/blob/main/images/Midas.png) 
