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
ESD (Entertainment Software Development) involved developing many C++ projects in the proprietary ASGE engine. The engine was very flexible, allowing for initial C++ development experience to create basic games such as these or more complex ordeals such as online card games (shown in "LLP: Play and Games").<br><br>

<h2><ins>The Projects</ins></h2>
Both Space Invaders and "Siege Attack" (an Angry Birds-esque game) though basic, were good examples of ASGE in this module, providing uses for calculated curves in their physics! Unique to Siege Attack was its method of importing levels, done through loading text files detailing each block's data for the level. </p>

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
This extract is called after the file is loaded, with the first segment collecting the data (sprite location, map co-ordinates) as a group of arrays. After being converted as needed, the proceding segment gives each block's data a sprite renderer, and fully places down the blocks where needed.<br><br>


<h2><ins>Notable Areas</ins></h2>
Both projects utilised different curves, Siege Attack using a more basic parabola while Space Invaders allowed for gravity, quadratic and sine inspired movements as alternate modes.<br><br>

The quadratic movement moved ships in another parabola curve, while the latter gave more "robotic" alternating movement. Siege Attack in the following exerpt lets the cannonball decay in the parabola curve, decelerating each axis' velocity:
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
While the quadratic and sine movements for Space Invaders employ their specific calculations to calculate each ship's new co-ordinates:
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

<h2><ins>Strengths and Shortcomings</ins></h2>
The projects were great at showcasing curves and provided not only insight into those, but were also valuable as a whole with starting in C# and game coding. The module began with basic examples of coding such as a number guessing game which were able to be done with prior experience, but each task leading up to and including these helped in creating a foundation for the rest of the courses.<br>

However, with both projects more visual polish could have been used as they look basic in appearance. Alongside this, Siege Attack's cannonball controls do not give a directional indicator alongside having a lack of weight, both factors not providing much satisfaction to the player. Meanwhile, Space Invaders has issues with its different modes though the ship's owns bullets can sometimes spawn away from it notably if the ship is movine. The gravity and sine movements also falter in some ways, with the former dropping down far too quickly and lopsided and the latter having too small a curve thus making the enemies look as if they are vibrating.<br><br>


<h2><ins>In Review</ins></h2>
Looking back, both projects were handled well and were good showings of what was learned during that period. The module overall was also notable in providing a great foundation for the rest of the modules, even if C# and ASGE were not the focal points of most. The projects would have benefitted from notable polish however, both in visual and gameplay oriented ways. 