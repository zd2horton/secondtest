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
An introductory foundation for Maya and Unity skills (though the former was only used for this module), familarising basics through tutorials before combining together for a finished experience.<br>


<h2><ins>The Project</ins></h2>
An experience using a tank model (with animations showcasing its parts) created in Maya, to traverse an island with obstructions requiring situational weapons to pass. They were allowed to be imaginative, resulting in such things as Galaxy Minstrel bullets knocking Maltesers down a mountain to clear the way of cubes.<br>

The tutorials' player avatar was also used, though was only required for travelling to the tank. Its controls were abnormal due to the basic coding and resembled tank controls.<br><br>


<h2><ins>Notable Areas</ins></h2>
Cameras were experimented with, notably ones for a tank wheel view, a view from a tunnel and a moving cutscene. The cameras for the latter two were toggled similarly to the following, changing views as needed:</p>

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
Though this was enough for the tunnel cameras, the cutscene camera's movement was done by basic movement from designated points as shown:</p>

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
<br>
<p style="text-align: center;">
<h2><ins>Strengths and Shortcomings</ins></h2>
The module gave a great foundation for many different yet vital areas to grow, with overall Unity as the most notable but others such as camera work, animations and character controls also took root here and grew further in later projects. It also really let imagination flow and helped liven up the obstacles and weapons!<br>

However, there were notable issues with the tank's controls, notably with aiming. These were due to difficulty learning Maya and modelling alongside the implementation in Unity which as a result of the difficulties, locked aiming to a 1st person view, and caused skewed controls with the view camera.<br><br>


<h2><ins>In Review</ins></h2>
Though issues like stilted slow movement weren't ideal, the overall project went well considering lack of any prior experience in Unity or Maya. The Unity side was a valuable foundation and as learning continued, many areas like camera and movement mechanics were optimised in code and refined far more. Character movement was notably refined in the following year's "Gameplay Programming", one of many experiences that may help remaster this project. The aiming system would be a large focal point and should become smoother to use.<br></p>