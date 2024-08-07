---
youtubeId: LWVKgK0nHd8
layout: projectpage
title: "ESD - Space Invaders & Siege Attack"
description: "Put on your seatbelt!"
projectyear: 2018
projectperiod: Year 1
project_url: https://github.com/zd2horton/space-invaders-zd2horton
date: 2024-08-05
engine: ASGE C++ Engine
categories: FinishedProject
skills: "Calculated Curves, Asset Loading, Class Creation"
---

<p style="text-align: center;">
ESD, or "Entertainment Software Development", involved the creation of many C++ projects in the proprietary ASGE engine. This involved aspects such as creating the game window itself with dimensions, defining functions in header files to use in the main files, and initialising of individual sprites for use in each game. The engine was very flexible, and allowed the creation of basic games such as these to more complex ordeals such as online card games (shown in Play and Games). Both Space Invaders and "Siege Attack" (an Angry Birds-esque game) utilised calculated curves in their gameplays, each project providing valuable experience in physics creation!


Quite unique to Siege Attack was the method of importing levels, done through loading text files detailing each block required with its texture location and the required co-ordinates. 

```
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

The given extract takes place after the file is loaded, with the first segment collecting the data as a group of arrays. After being converted into the required data types, the subsequent segment gives each block's data a sprite renderer, and fully places down the blocks where needed and as needed.


Both projects used different curves, Siege Attack using a more basic curve that drops off at the end also having some potential for bouncing, while Space Invaders allowed for gravity, quadratic and sine inspired movements for alternate gameplay modes. The former movement had ships moving in a forward bent curve, while the latter gave more "robotic" alternating movement. 

Siege Attack in the following exerpt pressurises vertical velocity with a negative value over time, while the horizontal velocity steadily decelerates:

```
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
		
	
While the quadratic and sine movements for Space Invaders employ specific calculations to calculate each ship's new co-ordinates:

```		
			if (menu_choice == 2)
			{

				enemy_x += dt_sec * enemy_speed * enemies_direction * 2;
				enemy_y = ((pow((enemy_x - game_width/2), 2) / -5000)) - intercept; 

				if (!(i == 0) && i % 10 == 0) 
				{
					intercept -= enemy_gap; 
					enemy_y = enemy_sprite[0]->yPos() + (enemy_gap * std::floor(i / 10));
				}
			}

			if (menu_choice == 3)
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

</p>