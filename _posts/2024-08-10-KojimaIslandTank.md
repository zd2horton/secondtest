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
skills: "Maya Modelling, Character Physics and Controller, Cameras, Cutscenes and Toggling"
bannerimage: "/zd2hortontest.github.io/assets/img/UniProjects.png"
---
<p style="text-align: center;">
<h2><ins>The Module and Tools</ins></h2>
Principles of 3D Environments introduced development and usage of both Maya and Unity skills (though the former was only used for this module), combining together for a finished experience. Before this combination effort, Unity tutorials were given as to familiarise with the engine and some of its basic capabilities.<br>


<h2><ins>The Project</ins></h2>
Through Maya, a tank model was created alongside detailed animations showcasing its various parts, with this being used in Unity as a playable vehicle to traverse a large island. The tank also recieved unique situational weapons for use with various obstacles, such as Galaxy Minstrel bullets for knocking down a box of Maltesers to clear the road of obstructing cubes.<br>

Alongside this, a player avatar from the prior tutorials was used. Its controls were notably abnormal though, resembling tank controls due to its development and the module's beginner nature. However, the experience only required the avatar to travel to the tank, primarily via a travelling platform.<br><br>


<h2><ins>Notable Areas</ins></h2>
There was also experimentation with cameras, notably with tunnel view cameras, a tank wheel camera and a moving cutscene camera. The wheel camera was set as a child of the tank and was toggled as desired, while the other cameras were toggled similarly to the following extract, changing camera activities as needed in the map:</p>

```cs
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
This sufficed for the tunnel cameras, but the cutscene camera's movement was created by moving from designated points in a basic way, as seen in this extract:</p>

```cs
	if (this.transform.position != point1.transform.position)
	{
		transform.position = Vector3.MoveTowards(transform.position, point1.transform.position, (Time.deltaTime * speed * 2.5f));
	}

	if (this.transform.position == point1.transform.position)
	{
		nextPoint = true;
	}
```
<br><br>

<p style="text-align: center;">
<h2><ins>Strengths and Shortcomings</ins></h2>
The project allowed for many different aspects to begin and grow. Though general Unity is the notable highlight, others such as camera work, animations and character controls also had foundations with the project and were able to be developed further in later projects. The experience was also open to a lot of imagination, which helped liven the obstacles and weapons!<br>

However, issues surrounding the tank's controls, notably with aiming, were apparent. This was due to difficulties with modelling in Maya alongside the eventual implementation in Unity which, as it locked aiming to a first-person view, caused skewed controls with the view's camera. As aforementioned, progress in Maya was notably stilted as modelling was an area that felt difficult to understand.<br><br>


<h2><ins>In Review</ins></h2>
Though the project's issues were bothersome, with movement generally stilted and slower than desired, it overall went well considering the lack of experience in both applications beforehand. The Unity work in specific provided valuable foundation to build from in Unity, and as experience would progress, many areas including camera and movement mechanics would be improved with far more optimised scripting.<br>

Movement in particular would be notably smoothed out for the avatar character in the following year's "Gameplay Programming", one of a number of future experiences which would prove very valuable to a remastering of this project. The aiming system would also be a focal point in a remastering, likely having more attributes about it to limit so that the camera would not prove problematic.</p>