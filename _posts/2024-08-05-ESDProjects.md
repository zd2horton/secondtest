---
youtubeId: LWVKgK0nHd8
layout: projectpage
title: "ESD - Space Invaders & Siege Attack"
description: "Two curve oriented projects in ASGE"
projectyear: 2018
projectperiod: Year 1
project_url: https://github.com/zd2horton/space-invaders-zd2horton
date: 2024-08-05
engine: ASGE C++ Engine
categories: FinishedProject
skills: "Calculated Curves, Asset Loading, Class Creation"
bannerimage: "/zd2hortontest.github.io/assets/img/UniProjects.png"
---
<p style="text-align: center;">
<h2><ins>The Module and Tools</ins></h2>
A beginner C++ module using the flexible and proprietary ASGE engine. A valuable foundation for creating both basic and complex games, with transferable values across the entire course.

<h2><ins>The Projects</ins></h2>
Simple "Space Invaders" and "Angry Birds" projects with different uses for calculated curves! Siege Attack used a basic parabola while Space Invaders also used gravity, quadratic and sine inspired movements as alternate modes. Though basic, these were good early examples of ASGE's potential.

<h2><ins>Notable Areas</ins></h2>
Siege Attack loaded levels through text files detailing block data. The following runs after loading the text file, first collecting the data (sprite, map co-ordinates) then using it to set up individual block objects.</p>

```cpp
		if (text_file.is_open())
		{
			for (int i = 0; i < NUMBER_OF_PIECES; i++)
			{
				getline(text_file, imported);
				block_direct[i] = imported;
				getline(text_file, imported);
				import_x[i] = imported;
				getline(text_file, imported);
				import_y[i] = imported;
			}
			text_file.close();
		}
		...
		for (int i = 0; i < NUMBER_OF_PIECES; i++)
		{
			if (!building_pieces[i].addSpriteComponent(renderer.get(), block_direct[i]))
			{
				signalExit();
			}

			ASGE::Sprite* building_sprite = building_pieces[i].spriteComponent()->getSprite();
			building_sprite->xPos(block_x[i]);
			building_sprite->yPos(block_y[i]);
			building_pieces[i].setVisibility(true);
		}
		return;
```

<p style="text-align: center;">
<br>
In its usage of calculated curves, its parabola decays the cannonball by decelerating each axis' velocity:
</p>

```cpp
		vector2 current_velocity = cannonballs[index].getVelocity();
		current_velocity.y += 0.1 * dt_sec * gravity;

		if (ball_sprite->xPos() <= 0 || ball_sprite->xPos() >= game_width)
		{
			current_velocity.x *= -0.1;
		}

		if ( ball_sprite->yPos() >= ground)
		{
			current_velocity.y *= -0.65;
			begin_bounce = true;
		}

		else
		{
			begin_bounce = false;
		}

		if (begin_bounce)
		{
			if (decrease_x > 0)
			{
				decrease_x -= 0.0008;
			}
		}

		current_velocity.x *= decrease_x;
		ball_sprite->xPos(ball_sprite->xPos() + current_velocity.x);
		ball_sprite->yPos(ball_sprite->yPos() + current_velocity.y);

		cannonballs[index].setVelocity(current_velocity);
```
		
<p style="text-align: center;">
Space Invader's quadratic option moved ships in another parabola, and sine gave more "robotic" movement. Both are shown below:
</p>

```cpp
			if (menu_choice == 2) //Quadratic
			{

				enemy_x += dt_sec * enemy_speed * enemies_direction * 2;
				enemy_y = ((pow((enemy_x - game_width/2), 2) / -5000)) - intercept; 

				if (!(i == 0) && i % 10 == 0) 
				{
					intercept -= enemy_gap; 
					enemy_y = enemy_sprite[0]->yPos() + (enemy_gap * std::floor(i / 10));
				}
			}

			if (menu_choice == 3) //Sine
			{
				enemy_x += dt_sec * enemy_speed * enemies_direction;
				enemy_y += sin(ticks / 20);
			}

			enemy_sprite[i]->xPos(enemy_x);
			enemy_sprite[i]->yPos(enemy_y);
			if (!enemies[i].spriteComponent()->getBoundingBox().isBetween(enemy_sprite[i]->xPos(), 100, game_width - 200))
			{
				position_counter += 1;
				enemies_direction *= -1;
			}
```
<br>
<p style="text-align: center;">
<h2><ins>Strengths and Shortcomings</ins></h2>
The projects showcased curves well and proved valuable as a whole in starting with C# and game development. The module began with basic coding tasks such as a number guessing game which could be done with prior experience, though each task including these helped lay foundations for the rest of the courses.<br><br><br>

However, both projects have basic appearances which visual polish would've helped. Additionally, Siege Attack would've benefitted from weightier more satisfying physics, and general quality of life such as indicators for cannonball paths. Meanwhile, Space Invaders' additional modes have some issues (gravity ships dropping quickly and lopsided, sine ships waving too rapidly) and the ship's bullets occasionally spawn incorrectly.<br><br>


<h2><ins>In Review</ins></h2>
At the time, the projects were handled well and good showcases of learned skills. The module also laid a great foundation for the rest, regardless of C#/ASGE usage or lack thereof. If revisited, notable attention given to visuals and gameplay fixes would dramatically improved them.</p>