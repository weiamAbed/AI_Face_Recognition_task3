# AI_Face_Recognition_task3
This repository is for task (3) of the AI track of my summer training at Smart-Methods


Note:
This is a collaborated work with Weiam Abed
Please check the Attached files, Pictures, Video

-------------------------------------------------------------------------------------------------------------------------------------------

On this task, we worked on real-time face recognition using python, visual studio code, OpenCV, Python Virtual Environment, and more on my OS Windows 10.
1- I Installed Python 3.9.6 through their main website and I checked the box "Add Python 3.9 to path" then started the installation.
2- I downloaded Visual Studio (The community edition and check Python Development package, Node.JS, Desktop web c++)
3- Downloaded Visual Studio Code by following the simple installation steps
4- from Face Recognition official website and copied the following code (source method):
git clone git://github.com/ageitgey/face_recognition
5- After that, I created a directory on my desktop called "facerecog"
6- through the terminal, I entered the directory path and cloned the previous source method code.
7- Unfortunately, I faced the following error " git: the term 'git' is not recognized.." and fixed it by downloading GIT from the official website and to check the error has disappeared type 'git' in a new PowerShell and I noticed the error was successfully solved.
8- In the same directory path I executed the following which took a lot of time to download the packages:
 pip install virtualenv
9- after I entered this code:
virtualenv maryamenv
10- I entered the path of the newly created environment and entered the Scripts path to run the following in order to activate the environment:
.\activate
11- Here I faced the following error "File Cannot Be Loaded Because Running Scripts Is Disabled on This System" and fixed it with the following steps:
First, Right-click on Windows Power Shell Select "Run as administrator"
Get-ExecutionPolicy -List
Set-ExecutionPolicy Unrestricted
Y
Set-ExecutionPolicy Unrestricted -Force
12- inside the python virtual environment I ran:
pip install cmake
pip install numpy==1.21.0
pip install opencv-python
13- Also, which took a lot of time to download all the necessary packages.
python setup.py install
14- I added this code to check the packages are installed "check the picture"
pip freeze

15- To open up the python shell:
python
16- Then entered:
import face_recognition
import cv2
Note: To activate/deactivate the virtual environment follow the steps:
In CMD in the path of your project folder enter this code to Activate:
env\Scripts\activate.bat
To Deactivate type in the same previous path:
deactivate
17- In visual studio code I used the following python code:
import numpy as np
import face_recognition as fr
import cv2 

video_capture = cv2.VideoCapture(0)

conner_image = fr.load_image_file("conner.jpg")
conner_face_encoding = fr.face_encodings(conner_image)[0]

known_face_encondings = [conner_face_encoding]
known_face_names = ["Conner"]

  while True: 
  
    ret, frame = video_capture.read()

    rgb_frame = frame[:, :, ::-1]

    face_locations = fr.face_locations(rgb_frame)
    face_encodings = fr.face_encodings(rgb_frame, face_locations)

    for (top, right, bottom, left), face_encoding in zip(face_locations, face_encodings):

        matches = fr.compare_faces(known_face_encondings, face_encoding)

        name = "Unknown"

        face_distances = fr.face_distance(known_face_encondings, face_encoding)

        best_match_index = np.argmin(face_distances)
        if matches[best_match_index]:
            name = known_face_names[best_match_index]

        cv2.rectangle(frame, (left, top), (right, bottom), (0, 0, 255), 2)

        cv2.rectangle(frame, (left, bottom -35), (right, bottom), (0, 0, 255), cv2.FILLED)
        font = cv2.FONT_HERSHEY_SIMPLEX
        cv2.putText(frame, name, (left + 6, bottom - 6), font, 1.0, (255, 255, 255), 1)

    cv2.imshow('Webcam_facerecognition', frame)

    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

    video_capture.release()
    cv2.destroyAllWindows()
    
    
18- Run Python file in terminal, To exit the camera (stop run) just type "q"
Thank you for reading :)!
