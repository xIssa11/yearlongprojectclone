# Ryan Grant logs
# Week 13 Nov 27 - Dec 3
# Time Spent
## **Meetings on:**
### Tuesday: We discussed how much we needed to get done this week in order to make the milestone deadline on Sunday
### Saturday: reconvene and talk about was accomplished in the week and what we had to do during the weekend
### Sunday: Meet once more to finalize our design document for submission
## **This week I was trying to implement this [tutorial](https://aws.amazon.com/blogs/machine-learning/blur-faces-in-videos-automatically-with-amazon-rekognition-video/)**
### The article mentions lots of topics that I have little to 0 experience working with.
### Aws Rekognition - as this was doing the bulk of the heavy lifting for this section of the project
### [aws rekognition analyze metadata](https://aws.amazon.com/getting-started/hands-on/analyze-extract-metadata-video-rekognition/)
### [aws rekognition detect faces](https://aws.amazon.com/getting-started/hands-on/detect-analyze-compare-faces-rekognition/)
### Both of these pages gave me a better understanding of how aws - rekognition works
### Spent time learning how lambda functions work together (using Step functions)
### Docker/Images/AWS ECR
### I have never really understood docker. And after some more research I still don't really understand. Hopefully I will not need a deep understanding for this project.
## This [guide](https://aws.amazon.com/blogs/machine-learning/blur-faces-in-videos-automatically-with-amazon-rekognition-video/) details setting up the follow aws services
1. AWS S3 Bucket
2. AWS lambda function to start detection in video
3. Request sent to AWS rekognition
### Next 3 steps utilize AWS step functions to automate the process
4. AWS lambda to check status of face detection job
5. AWS lambda- get timestamps and face coordinates then information gets passed to aws-rekognition
6. AWS lambda function to blur faces in video this uses AWS Elastic container registry (ECR)
7. video sent to new S3 bucket

## Issues/time spent debugging
1. After <code>pip install -r requirements.txt</code> I was running into the error

` Getting requirements to build wheel ... error
  error: subprocess-exited-with-error

  × Getting requirements to build wheel did not run successfully.
  │ exit code: 1
  ╰─> [54 lines of output]`
  ### This took over 3 hours to debug as it was not clear that the build aws was using had an interaction between the pip modules PyYAML and cython. This issue was caused because the newest version of cython had some incompatibilites with PyYAML
  ### This was fixed by using PyYAML==5.3.1 in requirements.txt
  ### I only found this solution after digging through diffent solutions for over 2 hours
  
2. Then I got the error NFO: building library "npymath" sources
      error: Microsoft Visual C++ 14.0 or greater is required. Get it with "Microsoft C++ Build Tools": https://visualstudio.microsoft.com/visual-cpp-build-tools/
      [end of output]
### installed build tools ~15-20 minutes after installing the wrong visual studio and restarting 
3. Several hours of trying to fix PATH variables
### Fixed by deleting python, node, npm and modules. Reinstalled, everything seems to be fixed. 
4. On deployment I was getting very strange error codes. 
### Fixed by doing 20-30 minutes of research someone suggested full disk causing errors and this happened to be my issue. 
5. After Deployment all of the Policies, roles, lambda functions and S3 buckets seemed to be in place. However as soon as I tested it with a video nothing worked. I was getting the error role does not have permission to call DetectFaces in Amazon Rekognition.
### Spent ~2 hours researching IAM roles, rekognition permisions, Testing different IAM Role policies. Created a new role called AdminLambda with the following policies AdministratorAccess and AmazonRekognitionFullAccess. Then set each of the 6 lambda functions execution role to be AdminLambda. 
### Even with all access I am still getting the error in StartFaceDetectFunction:
 <code> Lambda role does not have permission to call DetectFaces in Amazon Rekognition. </code>

### This is from 
<code>
 # use Amazon Rekognition to detect faces in video uploaded to Amazon S3
        try:
            job_id = start_face_detection(bucket, key, 1, reko)
</code>

### After a meeting on Saturay Dec 2nd we discussed how AWS amplify was likely causing permissions issues. We talked about 2 solutions
1. Find how to properly use AWS amplify to work with the permissions.
2. Completely scrap amplify (I don't think this is the best solution)
### Most of Sunday spent on the design document for milestone
### Peer eval screenshot
![img](https://i.imgur.com/QvriGmU.png)
## Week 11 & 12 Nov 13-26
## Assigning tasks for milestone 2
### We orignialy assigned myself, Issa and Abijith to work on KVS however none of us made progress. After Mo had figured out a solution, we reassigned tasks to have enough features to the milestone.
## Tasks I was assigned
1. Create lambda functions to detect when a new video is uploaded.
2. Create the bluring feature.
3. Create a lambda function to blur the video when detected from the first function, blur the video and send it to a new S3 bucket where the processed video was stored.
## Tasks completed this week
1. Setting up and offical S3 bucket for video preprocessing
2. Created a new Policy to give permissions for the lambda function to access the required resource.
3. Created a new IAM role. this grants a Lambda function permission to access AWS services and resources. 
4. Attached the 2 previous
5. Created a lambda function for detecting a new file being added to the S3 bucket video-preprocessing. 
6. Added manual testing as well as automated logs sent to cloudwatch services
### Tasks to do before milestone (1 week away)
1. Create a bluring feature
2. Create lambda function to blur and send to new bucket
### Peer eval screenshot
![img](https://i.imgur.com/7l1ou8C.png)
## Week 10 Nov 6-12
### From a week before the reading break I have been dealing with Major Depression disorder, causing massive ammounts of insomnia and complete lack to of will to work on any of my course. After talking with my parents they advised me to seek counsel. And im now taking medication to help alliviate these issue. I have talked about this a bit with my group to help them understand why I haven't been able to get that much done. During this time Mo steped up to sort out the storing video situation. I was at a huge roadblock so I am very grateful to him for this. Now I'm behind in all of my course and trying my hardest to meet the Milestone 2 deadline on Sunday Dec. 3rd.
## Week 9 Work period Oct 30 - Nov 5
## Overview of tasks completed
1. Create slides for Presentation
2. Create script for Presentation
3. Practice script until memorized
4. Coordinate 2 meetings for group practice. One on Wednesday night another on Thursday morning
5. Saturday meeting to go over features for next milestone
6. Assign features for next milestone
## Tasks to complete by milestone:
1. Create signal channel for KVS (WebRTC)
2. Create stream for KVS (WebRTC)
3. Front end get mic & camera
4. JS capture a/v
### Peer eval screenshot
![img](https://i.imgur.com/OFQBitK.png)
## Week 8 Work period Oct 23 - Oct 29
## Overview of tasks completed
1. Complete slides for Mini presentation
2. Create, edit, publish video demonstration for the presentation
### Although a major setback with not being able to use AWS video, considerable effor has been spent on Kinesis Video Stream (KVS) implementation. The use of WebRTC with associcated libraries in React has been reasearched. 
## Currently working on implementing these features:
1. Display video from database

## Tasks to complete by milestone:
1. Upload video to database
2. Display video from database
3. Mini-Presentation
### Peer eval screenshot
![img](https://i.imgur.com/SileOQX.png)
## Week 7 Work period Oct 16 - Oct 22
## Overview of tasks completed
### Our team ran into some major hurdles revolving around the setup of certain amazon services. Because the issues were preventing the continuation of indvidual tasks we decided to meet on Oct 17 in person to progress on our project. Although I was struggling with my personal laptop issues I was there to help if anyone needed my assistance. 
## Tasks to complete by milestone:
1. Upload video to database
2. Display video from database
3. Mini-Presentation
### With 2 weeks remaining until the mini presentation I should have my 2 features completed by next week. Leaving 1 week of work dedicated to the presentation. Including slides/video demonstration with prepared material. 
### Peer eval screenshot
![img](https://i.imgur.com/SileOQX.png)
## Week 6 Oct 9-15
## Overview of tasks completed:
1. Research how videos are stored in amazon database
2. Practice using video in html
3. Review peer work to familiarize myself with their implementation
## Goals for next week
1. Upload video to database
2. Display video from database
## Overview of tasks to be completed by milestone
1. Upload video to database
2. Display video from database
3. Mini-Presentation
### Peer eval screenshot
![week5](https://i.imgur.com/jdrc3Ep.png)
## Week 5 Oct 2-8
## Overview of tasks completed:
1. Plan meeting during class for project plan
2. Research tech stack including AWS, S3, etc
3. Break scope into smaller features
4. Assign features to each person for each milestone
## Overview of tasks to be completed by milestone
1. Website visual mockup
2. Upload video to database
3. Display video from database
### Peer eval screenshot
![tasks from board](https://i.imgur.com/UrmaTcI.png)
## Week 4 Sept 25 - Oct 1
## Overview of tasks:
### After being assigned to the datastructure portion of the word chain assignment I broke up the requirements into the following:
1. Find a word bank that would fit our specifications.
After reviewing many sources (most of which were in a unusable data format) I came upon 12Dicts and the various compliations of dictionaries. I chose the 2of12 wordlist which has all the words that were in at least 2 of the 12 major dictionaries. Resulting in a 41000 word .txt file.
2. Then with the .txt file I had to write code in python to convert to a .csv file. 
3. Take the .csv file and seperate it into seperate .csv files where the lengths of words were the same.
4. Write a simple python function to grab the designated .csv file convert it to a list and pass that to whoever needs it for the algorithm.
5. Finally I needed to document my work and push the python file and .csvs to the repo.

## Tasks completed from the board:
![tasks from board](https://i.imgur.com/9CpaTJy.png)

![tasks from board](https://i.imgur.com/9CpaTJy.png)
