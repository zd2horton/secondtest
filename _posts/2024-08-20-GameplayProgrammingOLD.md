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
Gameplay Programming involved the development of many gameplay based elements in Unity (movement, power-ups, cutscenes, enemies etc.), with some being new areas while others seen before were able to be improved upon. They were built upon through initial tutorials, before moving onto a group project that borrowed from the group's best implementations of each area.<br>


<h2><ins>The Project and Contributions</ins></h2> 
Overall contributions to the project were seen in the final level notable for two special sequences. The first requires the player to reach an opened door in time, leading to a battle area with slimes before the second sequence where the player steps on coloured tiles in the correct order to reach the finish. Both also include small cutscenes to guide the player.<br>

Though simple, the level showcases cutscene work well and conveys vital information, this being my notable contribution chosen for the project. The overall playstyle is more methodical alongside giving more room to breathe and plan than the previous levels, emphasised by not only the simple careful jumps of the door sequence, but also the puzzle section itself and the large combat space.<br><br>


<h2><ins>Notable Areas</ins></h2>
The final sequence (or "Simon Says") highlights the double jump power, with it being vital to reach the distant panels. This wasn't implemented in a well manner initially, causing issues ranging from inputting a colour twice or even thrice when stepped on once, to failing the player even with the correct order. The following extracts contributed to such: </p>


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
As shown, the logic deciding correct/incorrect combinations was extremely convoluted, also being inefficient in checking combinations and letting colours be inputted more than once. This logic was responsible for all notable issues, and was fully overhauled upon recent revisiting.<br>

The following extract is placed on the tiles, directing to the old logic before but now using the stepped on tile's colour as a string in its logic. This string is sent to the new code if the new sequence string doesn't already contain it. This is done so the final string only contains one of each colour as the correct sequence itself does.</p>


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
The following is the new logic, triggering after each colour has been stepped on. As the correct sequence is always the same, the player's input is able to be checked directly then refreshed if incorrect. </p>

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
This logic is far more reliable, removing the prior issues. However, its issue is with the nature of the colour string, as the logic relies on one of each colour to progress and thus is stuck on one hardcoded correct combination. Ideally the puzzle would reset after the player touches three tiles just as before, this also allowing for more randomised colour sequences. Due to the tiles' nature and collisions however, this present logic was implemented. <br><br>


<h2><ins>Strengths and Shortcomings</ins></h2>
As aforementioned, the level is able to showcase its cutscenes and objectives well, also featuring elements like time limits and testing the player's jumping skills. Additionally, though the group effort was focal to the module, the creation of each gameplay element in the time before gave valuable experience, including not only improvements on follow cameras and moving platforms but also newer areas such as spline camera movement and combat. Many of these elements though basic, are vital gameplay features, having made the module itself important for future projects in all shapes.<br>

There were also many notable issues, however. Alongside the initial Simon Says issues that were of no fault to the player and the segment's overall lack of randomisation, the overall level would have benefitted from higher difficulty and a firmer sense of flow and reward in its level design. Despite its methodical approach, it's very simple and far simpler than previous levels, not increasing in difficulty or intensity from them in spite of expectations.<br>

Due to its simplicity, there isn't much satisfaction gained from challenges or rewards provided, nor sense of an escalation in progression. As the final level proceeding the others it'd use these alterations to be a fully constructed journey, letting the overall experience provide more satisfaction and immersion throughout.<br><br>


<h2><ins>In Review</ins></h2>
Overall, this module was a vital step in progressing in character controlling and other gameplay programming elements, encapsulating many areas I am personally passionate about. Immense improvements were also made in areas first seen in the first year Tank Island project, while the character controller itself and the logic for power-ups would prove useful in tending to future platformer projects specifically. Though some glaring issues were initially present and the level doesn't experiment with much, the former was able to be tended to and the latter would also be improved given a similar project or even a remastering of this level.</p>