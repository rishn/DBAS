# Driver Behaviour Analysis System (DBAS) V.2

An application which is aimed to *monitor and analyse driver behaviour* on various use cases, created during internship at RoshAI Kochi.

Works with:	
		
  	 - Linux Ubuntu 20.04 LTS
	 - OpenCV 4.5.0+
	 - ROS-Noetic
	 - Dlib
	 - YOLOv5 DNN Framework
  	 - mpg321 (MP3 Player)

Current version consists of *ROS nodes* which capture feed from a *Leopard Imaging Camera with V4L2 driver and GMSL2 protocol* that help detect the following driver behaviour use cases:
1. **Drowsiness** - The system detects whether the driver is in a drowsy state or not based on five conditions:
	 - *Closed eye duration:* If the eyes are closed for a certain amount of time continuously checked via the eye aspect ratios (EAR) from the shape detected using Dlib library
	 - *Head tilt angle:* If the head is observed to tilt more than 10 degrees on either side for a certain    amount of time continuously - checked from the angle of the line joining the eye centers
	 - *Eye blink rate:* If the person is blinking less than 10 times per minute - checked from the EAR
	 - *Yawn rate:* If the person is yawning more than once per minute - checked from the size of the mouth opening
	 - A face is not detected in the camera feed

	Based on which of the five conditions are satisfied, the program concludes that the person is in any one of three states (alert - normal, semi-alert - warning, not alert - critical) and issues an appropriate alert.

2. **Device Usage** - The system detects whether the driver is using electronic devices (particularly cell phones) for a long period of time, in which case it concludes that the person is in a semi-alert - warning or not-alert - critical state based on the duration of the object captured in camera and issues an appropriate alert.
	- *DNN Framework* - YOLOv5
	- *Devices detected* - TV Monitor (62), Laptop (63), Remote (65), Cell Phone (67), Book (73)
3. **Eating/Drinking** - The system detects whether the driver is consuming food/drinks for a long period of time, in which case it concludes that the person is in a semi-alert - warning or not-alert - critical state based on the duration of the object captured in camera and issues an appropriate alert.
	- *DNN Framework* - YOLOv5
	- *Items detected* - Bottle (39), Wine glass  (40), Cup (41), Fork (42), Knife (43), Spoon (44), Bowl (45), Banana (46), Apple (47), Sandwich (48), Orange (49), Broccoli (50), Carrot (51), Hot dog (52), Pizza (53), Donut (54), Cake (55)
4. **Smoking** - The system detects whether the driver is smoking for a long period of time, in which case it concludes that the person is in a semi-alert - warning or not-alert - critical state based on the duration of the object captured in camera and issues an appropriate alert.
	- *ML Object Detection Framework* - Pre-trained YOLOv5 DNN model (exported in ONNX format)
5. **Seat belt** - The system detects whether the driver is wearing a seat belt or not. When the driver is not wearing a seat belt it concludes that the person is in a semi-alert - warning or not-alert - critical state based on the duration captured in camera and issues an appropriate alert.
	- *ML Object Detection Framework* - Custom-trained YOLOv5 DNN model (exported in ONNX format)
6. **Impairment by Alcohol/Drugs/Prescription** - Using the general YOLOv5 DNN framework discussed below under *3. Eating/Drinking* that checks for food and beverage items used by the driver, the system can detect consumption of alcoholic drinks while driving.
Using the pre-trained YOLOv5 DNN model discussed below under *4. Smoking*, the system can detect consumption of drugs via cigarettes.
7. **Fatigue/Ignorance** - Symptoms of fatigue are checked with the Drowsiness Detection module (discussed under *1. Drowsiness*), and appropriately alerted to the user.
The Drowsiness detection module also detects when the driver is not focused on the road or is not visible in the camera, thereby detecting signs of ignorant behaviour.

In the image window, the program displays the state of eyes, blink rate, yawn rate, head - yaw, pitch and roll angles, usage of device, consumption of food/drink, smoking and state of alertness (normal/warning/critical).

Text-to-Speech conversion for creating warning or critical alerts can be incorporated with the integration of saved audio files and Asynchronous ROS Callback methods.

![Car_4](https://github.com/rishn/DBAS/blob/main/assets/Car_4.png)
![Car_1](https://github.com/rishn/DBAS/blob/main/assets/Car_1.png)
![Car_3](https://github.com/rishn/DBAS/blob/main/assets/Car_3.png)
![Car_2](https://github.com/rishn/DBAS/blob/main/assets/Car_2.png)

## Demos

https://github.com/rishn/DBAS/assets/91053141/d273e78a-bd3a-4c6d-ac9b-5319bd201197

https://github.com/rishn/DBAS/assets/91053141/9492f15e-a066-4f53-a357-e4aff60c9ad6

https://github.com/rishn/DBAS/assets/91053141/f01228ef-0d8d-4e3e-8339-f2e3885402b8

https://github.com/rishn/DBAS/assets/91053141/5f75ba31-aaf7-495e-bce8-3405649a9446

https://github.com/rishn/DBAS/assets/91053141/28bfe589-1e93-4384-a727-a940d68e3ef2

https://github.com/rishn/DBAS/assets/91053141/211b4714-5f37-4598-9a6e-b11dde958552

https://github.com/rishn/DBAS/assets/91053141/5caa7eff-ab42-4375-9694-61bc1bb4f46d

https://github.com/rishn/DBAS/assets/91053141/638dc73c-d837-4a72-b7ea-0b3066ffacf4

https://github.com/rishn/DBAS/assets/91053141/33dff907-02b7-44e5-9eb1-29bab46c9eca

  
*Source files are not shared via the repository. However, additional files used along with the project directory structure are displayed.*
