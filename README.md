# S14

Here is the assignment:

Look at this model: https://github.com/intel-isl/MiDaS  
Look at this model: https://github.com/NVlabs/planercnn  
Now you have your helmet, mask, PPE, and boots dataset as well  

1.Take your dataset and run it through Midas and get depth images.  
2.Take your dataset and run it through the PlanerCNN model and get planer images (you'll not be using the depth images from PlanerCNN, so don't store them).  

Now your dataset contains depth map, surface planes, and bounding boxes for the classes  
3.Upload to your google drive with a shareable link to everyone, and add a GitHub repo that describes the dataset properly.  

Take this as a step by step approach to quickly get started on Google Colab with exploration and inputs received from the EVA5 Telegram Group.

We received the dataset [link].
Here is the sneak peak. [link]

Images contains 3590 files, 45 JPEG, 5 PNG AND 3540 JPGs.

It would be a good idea to convert the 50 non-JPG images to JPG before we start.
I chose to ignore them.

Task 1:
Getting Depth Images:

There is a lot to explore in the Repo but for the sake of the assignment, lets only look at the working steps:

Very neatly written repo and there are multiple variants, Pytorch, Docker etc but I chose to use the plain Python version.
This is a screenshot that matters:

Focussing on using Colab, it is a good idea to mount google drive and keep all data including repos in the drive so it is persistent across sessions or vms.
Used wget to download the weights file.
After exploring a lot, I found that gdown to be very helpful in copying google drive files.
I tried a lot of upload download etc. for exploration but you can use gdown for a quick copy.
Use unzip command on colab itself to unzip the files to a folder, rename it to input and follow the steps.
The depth map would be in the output folder.

Here is the link to the notebook [link] and the link [link] to the drive which containts depth maps.


Task 2:
Getting Planer Images

This was quite a task.  
The first issue was that the repo is almost 2 years old and the dependencies were 
cffi==1.11.5
numpy==1.15.4
opencv-python==3.4.4.19
scikit-image==0.14.1
torch==0.4.1
tqdm==4.28.1

Sorting this out on a local machine was time consuming exercise only to understand that Colab is a better option.
It took a lot of back and forth to get all dependencies to install until Ajith came as a saviour.
Ajith helped with a working notebook to run the code on Colab and xyz helped with a script that you could reuse everytime you spun a runtime on Colab.

The summary is to downgrade torch to 0.4.0 and install cuda 8 and gcc 5 and once done upgrade it to 0.4.1 and compile nms and roialign.
Also, since the GPUs mentioned were dated and Colab provides newer and faster ones, stick to arch=sm_60 worked for most instances.

The output was quite heavy with 9 files thrown for each input image which could easily consume all drive space.
Thanks to Gunda[link], you can use these modified files, file1[link] and file2[link] and get just the required planer image.
The script also helps store the output files with the input names.

Also add the argument "--numTestingImages=4000" while running inference as the maximum number is set at 100

Here is the link to the notebook[link] and the link to the drive which containts planer images.


Task 3:
Google drive with a shareable link to everyone
GitHub repo that describes the dataset properly


