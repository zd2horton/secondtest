---
youtubeId: LWVKgK0nHd8
layout: projectpage
title: "Gameplay Programming"
description: "Creating various gameplay elements for a final group project"
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
This project initially involved the creation and building upon of various gameplay elements (such as movement, power-ups, cutscenes, enemies etc.) before combining the best of these efforts in a group created experience. Despite this group effort being the focal point, each element created before such allowed for valuable experience, with improvements on follow cameras and moving platforms but also newer areas such as spline camera movement and combat.<br><br>

My contributions to the overall project were seen in the final level in the game which highlighted two special sequences. The first requires the player to reach an opened door in time, leading to a battle area of slimes before the second sequence requires the player to step on coloured tiles in a particular order to reach the finish. The two sequences also include small cutscenes as to guide the player.<br><br>

Though simple, the level is able to showcase cutscene work well and convey vital information, with the overall playstyle being more methodical than the previous intense levels. This is emphasised by not only the simple but careful jumps of the door sequence, but also by the puzzle section itself and the larger space for the slime arena, the latter of which giving more freedom for the player to plan their strikes as they wish rather than being forced to rush in.<br><br>

The final sequence (or "Simon Says") was created to highlight the double jump power, with it being vital to reach distant panels. The sequence was not initially implemented in a well manner however, and thus caused issues of no fault to the player ranging from inputting a colour twice or even thrice when stepped on once, to failing the player even when the pattern was correct. The following code snippets contributed to such: </p>


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
As shown, the logic used to determine correct or incorrect combinations was extremely convoluted, not only being inefficient in checking combinations but also allowing for colours to be inputted more than once. This logic was responsible for all issues, and upon revisiting the project has been overhauled fully as to erase these issues alongside their awkward logic.<br><br>

The code as of recent has now been overhauled, and has erased these issues. The following exerpt is placed on the tiles, having directed to the old logic before but now resting on the colour of the stepped on tile as a string. This string is sent to the new code if a hit sequence string doesn't already contain the colour.</p>


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
The following exerpt is the new logic for the puzzle, which triggers once one of each colour has been stepped on. As the colour sequence is the same every time it is able to be checked directly and then refreshed if incorrect. </p>

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
This logic is notably more reliable and removes the issues from before. However, its issue is with how the colour string is sent, as the logic relies on new colours being pushed to progress. Ideally the puzzle should reset after the player touches three tiles regardless, this logic also allowing for more randomised colour sequences. Though, due to the tiles' nature and collisions, this present logic was implemented. <br><br><br><br>

In all, this module was a vital step in progressing in character controlling and other gameplay programming elements, encapsulating many areas I am personally passionate about. Immense improvements were also made in areas first seen in the first year Tank Island project, while the character controller itself and the logic for power-ups would prove useful in tending to future platformer projects specifically.<br><br>

In terms of improvements, many could still be made. Alongside the aforementioned improvements to the Simon Says area, the overall level itself would benefit from a sense of higher difficulty, alongside a more firm feeling of flow and reward in its level design. The current implementation though unique in its more methodical approach, does not increase in difficulty from the previous level and would be expected to be more intense, if not more difficult. <br><br>

Alongside this, there is not much satisfaction that arises from either challenges or rewards provided to the player, nor is there much sense of an escalation in progression. As the final level it would benefit greatly from these alterations in order to be a fully constructed journey, so that the player is able to derive satisfaction and immersion all throughout the experience.<br><br>
</p>



<p style="text-align: center;">
As experience would progress, many areas including these camera and movement mechanics would be improved with far more optimised scripting. In review, though many areas were sluggish in nature, the project was still very valuable in crafting the foundations of learning in Unity. <br><br>
Movement in particular would be notably smoothed out for the avatar character in the following year's "Gameplay Programming", one of a number of future experiences which would prove very valuable to a remastering of this project.</p>