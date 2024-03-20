# CCTV-Traffic-Cop-using-GAN
[Deep Learning Application] Super Resolution using SRGAN

## Period
23.11.15 ~ 23.12.17

## Background
Recently, traffic crimes are increasing. To chase these crimes, police check the car license plate through CCTV, but there are some disadvantages.

According to an article, 45 percent of CCTV of Korea are aging and the image quality is poor.

In addition, it is difficult to recognize license plates due to various conditions such as snow, rain, and night.

So, to solve these problem, we proceeded the project that improving the image quality of the license plate in CCTV. 

Therefore, our goal is to be more clear, robust in many situations and to increase the resolution in more detail than old ways.

## Data
* https://www.kaggle.com/datasets/andrewmvd/car-plate-detection/data 

* https://data.caltech.edu/records/fmbpr-ezq86


## Role 
| 박재현 | 구민| 전태성 | 박성욱
|:---:|:---:|:---:|:---:|
| SRGAN & Make evaluation metric| OCR | SRCNN | Bicubic |


## File

* Result : result files 
  
* utils : SRGAN model code 
  - Data Augmentation.ipynb : Data Augmentation file (Bright, Snow, Rain)
  - LRR.ipynb : Convert car lincese letters to image


## Method

We use car license image dataset total of 432 images. 

In data preprocessing, it is divided into select data, crop license plate, augmentation data. Among the collected data, we exclude unsuitable data for learning. Through this process, 341 data were selected.

And we crop only the license plate to focus entirely on increasing the resolution of the license plate.

We have added conditions similar to real-world situations to increase the resolution of the image under any environments, in other words, robustly to various situations.

Brightness was adjusted to express day and night and noise were added to the image to express rain and snow. After this preprocessing, we got 3410 images.

In modeling process, in SRGAN papers, they applied two upsampling, but we applied three upsampling to get a higher-resolution image.



## Result

We used 3310 train data and 100 test data. In problems such as resolution, PSNR and SSIM are approximate metrics and cannot be used to evaluate the quality of good images.

So we evaluated the model using a real-world visual method, one of which is an metric called Letters Recognition Rate, called LRR.

This is an metric to check how many license plate recognition has been made for each image through the EasyOCR model, and it is made by ourselves. LRR is dividing into LCR and LSR.

First, LCR is the Letter Correction Rate, which is an metric of how many letters Easyocr correctly matched. 

In addition, we check how similar OCR viewed the letter. So, LSR measures similarity between the original letter and the recognized letter by OCR. 

After expressing the two letters as images and finding their intersection, we find the cross ratio with the original image. 

Lastly, we conducted a human evaluation called Rank. The evaluation presents images from the three methods, ranking them based on highest resolution and easiest-to-read text from first to third.

The subjects were a total of 30 people, including 1 person in their teens, 26 people in their 20s, and 3 people in their 50s.

As a result, our model performed better than baseline in visual metrics.

<src img = 'Result/sr_result.png'>
<src img = 'Result/result_with_baseline3.png'>
  
## Expected Outcomes

The expected effect of this project is first, cost reduction. The SRGAN technology can be much cheaper than the cost of upgrading an existing low-resolution CCTV system. In other words, instead of installing expensive new hardware, we can save money by applying software updates to existing systems. 

Second, this technology can be combined with self-driving. If the improved image with SRGAN technology is used, accidents can be accurately detected and casualties can be minimized.

Finally, it can help a lot in crime prevention, which is the purpose of cctv. The high-resolution images can more clearly identify the driver's face, car model, color, as well as its license plate. This will greatly help in tracking getaway vehicles, identifying drivers, and tracking traffic offenders.

Ultimately, through our traffic cop, it is possible to create a pleasant road environment and a safe society.



## Reference

https://github.com/PacktPublishing/Generative-Adversarial-Networks-Projects/blob/master/Chapter05/run.py#L17

Chao Dong, Chen Change Loy, Member, Kaiming He, and Xiaoou Tang, Fellow, *Image Super-Resolution Using Deep Convolutional Networks (IEEE, 2009)*

Hojatollah Yeganeh, *Cross Dynamic Range And Cross Resolution Objective Image Quality Assessment With Applications (2014)*


