# Self-driving-Car-Using-Raspberry-Pi
This project develops a prototype of self driving car which basically demonstrates lane tracking, automated parking,obstacle detection and traffic lights detection.

The project aims to build a monocular vision using Raspberry Pi as a processing chip. A Pi camera along with an ultrasonic sensor is used to provide necessary data from the real world to the module. The proposed module helps the driver in reaching the given destination safely and intelligently thus avoiding the risk of human errors. Many existing algorithms like  Obstacle detection,Traffic signal detection ,Automatic parking  and Lane tracking are combined together to provide the necessary control to the car.Obstacle detection and Automatic parking  is carried out by Ultrasoic sensors . Lane Tracking and Traffic signal detection is done with help of PIcamera along with OpenCV. 

 A miniature car including above features will be developed which will show optimum performance in the simulated environment considering the fact that all assumptions and Dependencies are met.
 
 Hardware Requirements:<br/>
 1 x Raspberry Pi Model 3B <br/>
 1 x Raspberry Pi 5v Camera <br/>
 2 x HCSR04 Ultrasonic Sensor <br/>
 1 x L293D Motor Driver <br/>
 1 x Robot Chassis Cost <br/>
 1 x Power Bank Cost <br/>
 1 x 9v Battery Cost <br/>
 1 x Set of Jumper wires <br/>
 1 x 16 GB Micro SD Card <br/>
 1 x  Bread Board Cost   <br/>
 
 
 Software Requirements:
 Raspian Os <br/>
 Xming Server <br/>
 PuTTY SSH Session <br/>
 Remote Desktop Connection <br/>
 Opencv 3.0 <br/>
 Python 2.7 <br/>
 
 Modules presented in this project:<br/>
 
 I] Obstacle Avoidance:<br/>
 Working Steps:<br/>
 1.Trig pin on ultrasonic sensor is made logic high using external trigger signal.<br/>
 2.A signal is sent from the transmitter module.<br/>
 3.The signals return back after hitting a surface and the receiver detects this signal.<br/>
 4.The Echo pin is high from the time of sending the signal and receiving it.<br/>
 5.This time can be converted to distance using appropriate calculations.The speed of sound is 340 m/s or 29 microseconds per centimeter<br/>
   &nbsp;&nbsp;Distance(cm) = (Time/29)/2<br/>
 6.This information is processed by the Pi. If the distance between the car and the obstacle is less than 30cm, the car stops.<br/>
 7.Wheels on the left move opposite to the wheels on the right. This helps the car to turn.<br/>
 
 ![Obstacle](https://www.papeeria.com/f/raw/obstacle.png?project_id=a926426ea9aa2141d68919410f7488e9&file_id=5b63a4ca263406746ea1a092484acb3b) <br/>
 ![No Obstacle](https://www.papeeria.com/f/raw/No%20obstacle.png?project_id=a926426ea9aa2141d68919410f7488e9&file_id=fab2f34bfde89d2402e1725700c21bea)<br/>
 ![Terminal output](https://www.papeeria.com/f/raw/obst_ter.png?project_id=a926426ea9aa2141d68919410f7488e9&file_id=ef35b00e37691c1a362acf43c003fbb2)<br/>
 
 
 
 
 II] Lane Tracking:<br/>
 Working Steps:<br/>
 1.Extract the color range for the road.<br/>
 2.Convert the image into grayscale image.<br/>
 3.Identify the lane in white/yellow color using Canny edge algorithm.<br/>
 4.Define the region of interest by using image mask.<br/>
 5.Transform the curved lines using Hough transform.<br/>
 6.Find the slope of lanes obtained from Hough transform.<br/>
 7.If (slope>= -80 and slope <= -30):<br/>
      &nbsp;&nbsp;&nbsp;&nbsp;r+=1 (increment right lane counter)<br/>
      &nbsp;&nbsp;&nbsp;&nbsp;l=0 (reset left lane counter)<br/>
   If(slope>= 30 and slope <= 80):<br/>
      &nbsp;&nbsp;&nbsp;&nbsp;l+=1 (increment left lane counter)<br/>
      &nbsp;&nbsp;&nbsp;&nbsp;r=0 (reset right lane counter)<br/>
8.If l > 10:<br/>
   &nbsp;&nbsp;&nbsp;&nbsp; Turn left<br/>
  elif r > 10:<br/>
   &nbsp;&nbsp;&nbsp;&nbsp; Turn right<br/>
  else:<br/>
   &nbsp;&nbsp;&nbsp;&nbsp; Move straight <br/>
9.Repeat from step 1<br/>
![Left Turn Detection](https://www.papeeria.com/f/raw/left.png?project_id=a926426ea9aa2141d68919410f7488e9&file_id=844082b49a568ff6299de8a8c1d4184b)<br/>
![Rigth Turn Detection](https://www.papeeria.com/f/raw/right.png?project_id=a926426ea9aa2141d68919410f7488e9&file_id=0830918814f385ccb750b92aacf3d18d)<br/>
![Go Straight](https://www.papeeria.com/f/raw/straight.png?project_id=a926426ea9aa2141d68919410f7488e9&file_id=7e089dd46b5bcacfe924e91d0ed16e43)<br/>


III] Traffic light detection:<br/>
Working Steps:<br/>
1.Capture Frames from the pi camera.<br/>
2.Define the specific region in each frame which will be considered for computation.<br/>
3.In defined region using color & shape detection identify Red & Green traffic signal.<br/>
4.If Red signal detected stop the car.<br/>
5.If Green signal detected move the car.<br/>
![Red Signal](https://www.papeeria.com/f/raw/red_light.png?project_id=a926426ea9aa2141d68919410f7488e9&file_id=96303e6e913e5dfc79c716817b8371ec)<br/>
![Green Signal](https://www.papeeria.com/f/raw/green_light.png?project_id=a926426ea9aa2141d68919410f7488e9&file_id=09ae07def3a709fdb8655f20f738bf15)<br/>



IV] Automated Parking:<br/>
Working Steps:<br/>
1.Trig pin on ultrasonic sensor is made logic high using external trigger signal.<br/>
2.A signal is sent from the transmitter module.<br/>
3.The signals return back after hitting a surface and the receiver detects this signal.<br/>
4.Echo pin is high from the time of sending the signal and receiving it.<br/>
5.This time can be converted to distance using appropriate calculations.<br/>
      The speed of sound is 340 m/s or 29 microseconds per centimeter<br/>
      &nbsp;&nbsp;Distance(cm) = (Time/29)/2<br/>
6.The car will keep checking for empty slots by detecting empty spaces with distance>30 cm.<br/>
7.Once it detects free space it keeps checking whether distance in >30 cm for about 1 sec while moving forward.<br/>
8.If it gets distance >30cm for 1 sec then it has found space to park and car will stop.<br/>
9.Then it will park in that spot.<br/>

![Searching For Free Spot](https://www.papeeria.com/f/raw/parking1.png?project_id=a926426ea9aa2141d68919410f7488e9&file_id=a4061905d1f9dcaf5f8366a47ec32823)<br/>
![Found Free Space](https://www.papeeria.com/f/raw/park2.png?project_id=a926426ea9aa2141d68919410f7488e9&file_id=0cab6408434e5f332ea6a3ac88cc7a70)<br/>
![Parked](https://www.papeeria.com/f/raw/park3.png?project_id=a926426ea9aa2141d68919410f7488e9&file_id=709baca78feed22c46d9fc7c7e07b707)<br/>



 
 
