---
youtubeId: LWVKgK0nHd8
layout: projectpage
title: "Gameplay Programming"
description: "An ending level concept showing various gameplay elements learned"
projectyear: 2019
projectperiod: Year 2
project_url: https://github.com/zd2horton/GPP-Group-Project
date: 2025-03-01
engine: Unity
categories: FinishedProject
skills: "Gameplay Programming, Player Character Creation, Group and Coding Co-Ordination, and More"
bannerimage: "/zd2hortontest.github.io/assets/img/UniProjects.png"
---

<p style="text-align: center;">
<h2><ins>The Module and Project</ins></h2>
    <ul>
    <li>Development of gameplay oriented elements both newly and familiarly tackled, via tutorials.</li>
    <li>These included movement, power-ups, cutscenes, enemies and more.</li>
    <li>A final group project utilised the best contribution of each area.</li>
    </ul><br>


<h2><ins>My Contributions</ins></h2> 
These were seen in the final level, notably in two sequences. The first has the player activate a timed door to reach, leading to a battle area before the second sequence, a basic Simon Says, ends the level. Both include small, guiding cutscenes.<br><br><br>

The level showcases vital cutscenes well, though has a simpler playstyle than previous levels, also allowing rest periods. Simple careful jumps at the beginning showcase this, alongside the large combat space and the final sequence.<br><br>


<h2><ins>Notable Areas</ins></h2>
The Simon Says area highlights the double jump power, it being vital for navigation. The initial implementation caused issues however, such as counting a colour many times when stepped on, or failing the player even when correct. The following contributed to such: </p>


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
This logic used to verify combinations was very convoluted and inefficient, thus causing issues. It has been fully overhauled as of recent.<br><br>

Each tile now has the following, sending its colour when activated to a new sequence string if it doesn't already contain it. This is done so the final string has each colour only once, as the correct sequence itself does.</p>


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
The following new logic triggers once each colour is sent. The correct order does not vary, so it can compared reliably. </p>

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
Though far more reliable and sound, this logic was implemented due to the tiles' limiting nature and collisions, thus the sequence is more set in stone and hardcoded. Ideally, the puzzle would orient more around randomised orders. <br><br>


<h2><ins>Strengths and Shortcomings</ins></h2>
Generally, the level did well in indicating vital information, also using time limits and testing jumping skills. Though the final effort was the module's main area, the creation of each element beforehand also gave valuable experience, with improvements on follow cameras and moving platforms as well as new areas such as spline camera movement and combat. Many of these elements though basic, are vital gameplay features, building upon foundations even further.<br><br>

There were also many notable issues, notably those in the initial Simon Says implementation and the segment's overall lack of randomisation. However, the overall level should've also had a firmer sense of difficulty and flow and reward in its design. It's very simple and far more so than levels before with its methodical approach, not posing a larger challenge or intensity as expected of a final level.<br><br>

As a result of these factors, there isn't much satisfaction from challenges or rewards provided, nor sense of escalation in progression. With improvements from this, it could be a fully constructed journey, with more satisfaction and immersion throughout.<br><br>


<h2><ins>In Review</ins></h2>
In all, the module was a vital step in handling character controlling and other gameplay elements, with many areas I am personally passionate about. Many areas first seen in the Tank project were notably improved, while the character controller and power-ups logic proved useful for future platformer projects. Some glaring issues were initially present and the level isn't very expressive, but the former was able to be tended to and the latter would be improved in a similar project or even a remaster.</p>