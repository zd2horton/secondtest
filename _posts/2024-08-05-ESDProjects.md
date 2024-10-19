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
ESD (Entertainment Software Development) involved developing many C++ projects in the proprietary ASGE engine. The engine was very flexible, giving initial C++ development experience where basic or even more complex games could be developed, ranging from the games discussed here to an online card game (shown in "LLP: Play and Games").<br>


<h2><ins>The Projects</ins></h2>
Both Space Invaders and "Siege Attack" (an Angry Birds-esque game) though basic, were good examples of ASGE in this module, providing different uses for calculated curves in their physics! Siege Attack had a unique method of importing levels, done through loading text files detailing each block's data for the level. </p>

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
This extract runs after loading the file, with the first segment collecting the data (sprite location, map co-ordinates) as a group of arrays. After conversion, the next segment gives each block's data a sprite renderer, and fully places down the blocks where needed.<br><br>


<h2><ins>Notable Areas</ins></h2>
Both projects used different curves, Siege Attack using a more basic parabola while Space Invaders used gravity, quadratic and sine inspired movements as alternate modes.<br><br>

The quadratic movement moved ships in another parabola curve, while sine movement gave more "robotic" alternating movement. Siege Attack in the following exerpt decays the cannonball in the parabola curve, decelerating each axis' velocity:
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
While the quadratic and sine movements for Space Invaders utilise their specific calculations for each ship's new co-ordinates:
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
<br><br>
<h2><ins>Strengths and Shortcomings</ins></h2>
The projects were great at showcasing curves and were also valuable as a whole in starting with C# and game coding. The module began with basic examples of coding such as a number guessing game which were able to be done with prior experience, but each task leading up to and including these helped in creating new foundations for the rest of the courses.<br>

However, with both projects, more visual polish would have helped upgrade their basic appearances. Alongside this, Siege Attack's cannonballs don't give a directional indicator when pulled back and also lack a weighty feeling, both of these not giving much satisfying feedback. Meanwhile, Space Invaders has issues with its different modes, and the ship's owns bullets can sometimes spawn notably far from it especially if the ship is moving. The gravity and sine modes in specific have notable issues, with the former dropping down far too quickly in a lopsided fashion and the latter having too small a curve, giving the enemies a rapid vibrating appearance.<br><br>


<h2><ins>In Review</ins></h2>
Looking back, both projects were handled well for the time and were good showings of what was learned during that period. The module overall was also notable in providing a great foundation for the rest of the modules, even if C# and ASGE were not the focal points of most. The projects would have benefitted from notable polish however, both in visual and gameplay oriented ways as discussed.