---
youtubeId: LWVKgK0nHd8
layout: projectpage
title: "Gameplay Programming"
description: "Various gameplay elements used for an ending level concept"
projectyear: 2019
projectperiod: Year 2
project_url: https://github.com/zd2horton/GPP-Group-Project
date: 2024-08-20
engine: Unity
categories: FinishedProject
skills: "Gameplay Programming, Player Character Creation, Group and Coding Co-Ordination, and More"
bannerimage: "/zd2hortontest.github.io/assets/img/UniProjects.png"
---

<p style="text-align: center;">
<h2><ins>The Module and Tools</ins></h2>
Development of gameplay oriented elements (movement, power-ups, cutscenes, enemies etc.) both new and tackled previously, done in tutorial format before a final group project utilising the best contribution of each area.<br>


<h2><ins>The Project and Contributions</ins></h2> 
My contributions were seen in the final level, notably in two sequences. The first has the player needing to reach an activated door, leading to a battle area before the second sequence where the player finishes the level with a basic Simon Says. Both include small, guiding cutscenes.<br><br><br>

Though simple, the level showcases vital cutscenes well, with a more methodical style that gives more rest or planning periods than previous levels. This is emphasised by simple but careful jumps with the first sequence alongside the puzzle sequence itself and the large combat space.<br><br>


<h2><ins>Notable Areas</ins></h2>
The Simon Says area showcases the double jump power, its usage vital to navigate the panels. This wasn't implemented well at first, spawning issues from registering a colour more than once when stepped on, to failing the player even when correct. The following contributed to such: </p>


```cs
    public void tileHit(Collider other, int index)
    {
        if (transform.GetChild(index).tag == "redTile")
        {
            redTileHit = true;
            redTapped++;
        }
		(if statements continued for blue and green)
    }
	
	
    private void checkIfWrong()
    {
        if (!((blueTileHit == false && greenTileHit == false && redTileHit == false)
            || (blueTileHit == true && greenTileHit == false && redTileHit == false)
            || (blueTileHit == true && greenTileHit == true && redTileHit == false)
            || (blueTileHit == true && greenTileHit == true && redTileHit == true))
            || (redTapped > 1 || blueTapped > 1 || greenTapped > 1))
        {
            blueTileHit = false;
            greenTileHit = false;
            redTileHit = false;

            redTapped = 0;
            blueTapped = 0;
            greenTapped = 0;
            animator.SetTrigger("Wrong");
            StartCoroutine("Respawn");
        }

        else if (blueTileHit == true && greenTileHit == true && redTileHit == true)
        {
            solvedPuzzle = true;
        }
    }

    IEnumerator Respawn()
    {
        yield return new WaitForSeconds(1.1f);
        player.transform.position = new Vector3(14, 0.6f, 83.44f);
        player.GetComponent<PlayerControl>().HEALTH -= 5;

    }
```

<p style="text-align: center;">
This logic verifying correct/incorrect combinations was very convoluted and inefficient, being responsible for aforementioned issues. Recently, it has been fully overhauled.<br><br>

The following is placed on each tile, now sending an activated tile's colour as a string to the new code if the new sequence string doesn't already contain it. This is done so the final string has each colour only once, as the correct sequence itself does.</p>


```cs 
    private void Start()
    {
		simonScript = gameObject.GetComponentInParent<simonSaysScriptNew>();
	}

    void OnTriggerEnter(Collider other)
    {
		string attachThis = gameObject.tag.Replace("Tile", "");
		if (other.gameObject.tag == "Player" && !simonScript.hitSequenceString.Contains(attachThis))
        {
			simonScript.hitSequenceString += attachThis;
			gameObject.GetComponentInParent<simonSaysScriptNew>().numTapped++;
		}
    }
}
```

<p style="text-align: center;">
The following is the new logic, triggering after each colour has been used. As the correct order is a constant, the final string can be directly checked with it. </p>

```cs
 private void Update()
    {
        if (numTapped == 3){checkIfWrong();}
    }

    private void checkIfWrong()
    {
        if (hitSequenceString != "bluegreenred")
        {
            hitSequenceString = "";
            numTapped = 0;
            animator.SetTrigger("Wrong");
            StartCoroutine("Respawn");
        }
        else{solvedPuzzle = true;}
    }
```
<p style="text-align: center;">
Though far more reliable and sound, this logic's issue is with the correct sequence being hardcoded, and relies in all ways on it being one of each colour. Ideally, the puzzle would reset after touching three tiles as before, and allow wholly randomised orders. Due to the tiles' nature and collisions however, this present logic was implemented. <br><br>


<h2><ins>Strengths and Shortcomings</ins></h2>
Generally, the level did well in indicating vital information, also using time limits and testing jumping skills. Though the final effort was the module's main area, the creation of each element beforehand also gave valuable experience, with improvements on follow cameras and moving platforms as well as new areas such as spline camera movement and combat. Many of these elements though basic, are vital gameplay features, building upon foundations even further.<br><br>

There were also many notable issues, notably those in the initial Simon Says implementation and the segment's overall lack of randomisation. However, the overall level should've also had a firmer sense of difficulty and flow and reward in its design. It's very simple and far more so than levels before with its methodical approach, not posing a larger challenge or intensity as expected of a final level.<br><br>

As a result of these factors, there isn't much satisfaction from challenges or rewards provided, nor sense of escalation in progression. With improvements from this, it could be a fully constructed journey, with more satisfaction and immersion throughout.<br><br>


<h2><ins>In Review</ins></h2>
In all, the module was a vital step in handling character controlling and other gameplay elements, with many areas I am personally passionate about. Many areas first seen in the Tank project were notably improved, while the character controller and power-ups logic proved useful for future platformer projects. Some glaring issues were initially present and the level isn't very expressive, but the former was able to be tended to and the latter would be improved in a similar project or even a remaster.</p>