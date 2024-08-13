---
youtubeId: LWVKgK0nHd8
layout: projectpage
title: "3D Environments - Kojima Island Tank"
description: "Small beginnings with Unity and using external models"
projectyear: 2018
projectperiod: Year 1
project_url: https://github.com/zd2horton/Po3D
date: 2024-08-10
engine: Unity
categories: FinishedProject
skills: "Maya Modelling, Character Physics and Controller, Cameras and Toggling"
bannerimage: "/zd2hortontest.github.io/assets/img/UniProjects.png"
---
<p style="text-align: center;">
Principles of 3D Environments included development and usage of both Maya and Unity skills, combining together for a finished product. Through Maya a tank model was created alongside detailed animations showcasing its various parts, with these outputs being used in Unity as a playable vehicle to traverse a large island. <br><br>

The tank also recieved unique situational weapons to use with oncoming obstacles, such as shooting a Galaxy Minstrel to knock down a box of Maltesers and clear an obstacle on the road. The avatar's own controls were abnormal and resembled tank controls due to the assignment being the first of many Unity projects, though the overall sequence only required avatar controls for the player to make their way to the tank primarily via a travelling platform.<br><br>

Difficulties surrounding the tank's controls, notably with its aiming, were also apparent. This was due to difficulties with modelling in Maya as well as the eventual implementation which, only allowed aiming once in first-person, caused skewed controls with said view's camera. Though these elements were bothersome and movement generally was stilted and slower than desired, the project overall was well considering the lack of experience in either application beforehand. <br><br>

There was also some experimentation with cameras, notably with tunnel view cameras, a tank wheel camera and a moving cutscene camera. The wheel camera was set as a child of the tank and would be toggled as desired, while the other cameras would be toggled similarly to the following extract, changing camera activities as needed in the map:

```
    void OnTriggerEnter(Collider other)
    {
        if (other.transform.IsChildOf(tank.transform) || other.gameObject == ethan)
        {
            nonTriggerCamera.enabled = false;
            csCamera.gameObject.SetActive(true);
            csCamera.enabled = true;
        }
    }

    void OnTriggerExit(Collider other)
    {
        if (other.transform.IsChildOf(tank.transform) || other.gameObject == ethan)
        {
            nonTriggerCamera.enabled = true;
            csCamera.enabled = false;
        }
    }
```

<p style="text-align: center;">
This sufficed for the tunnel cameras, but the cutscene camera's movement would be created through moving from point to point in a basic manner, as seen in this extract:

```
	if (this.transform.position != point1.transform.position)
	{
		transform.position = Vector3.MoveTowards(transform.position, point1.transform.position, (Time.deltaTime * speed * 2.5f));
	}

	if (this.transform.position == point1.transform.position)
	{
		nextPoint = true;
	}
```
<p style="text-align: center;">
As experience would progress, many areas including these camera and movement mechanics would be improved in far more optimised scripting. In review, though many areas were sluggish in nature, the project was still very valuable in crafting the foundations of learning in Unity.
Movement in particular would be notably smoothed out for the avatar character in the following year's "Gameplay Programming", one of a number of future experiences which would prove very valuable to a remastering of this project.