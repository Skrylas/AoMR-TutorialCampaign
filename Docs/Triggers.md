# Triggers

## Difficulty:
Difficulty for Campaigns overlaps with standard Skirmish/Scenario gameplay, with the exception of Story Mode and Ludicrous Difficulty.
The Condition Scenario: Difficulty Level features difficulties from the Skirmish Column below:
| Skirmish Difficulties  | Campaign Difficulties |
| ------------- | ------------- |
| -  | Story Mode  |
| Standard  |  Standard  |
| Moderate  |  Moderate  |
| Titan  |  Titan  |
| Extreme  |  -    |
| Legendary  |  -   |
| -  |  Ludicrous  |

Setting Triggers up for Extreme and Legendary will not do anything for your Campaign.  And Story Mode and Ludicrous are not part of the Difficulty Condition options.
- Story Mode is a hidden Tech that is applied to the Player (Player 1), that boosts work rate by 50%, along with giving your Military Units additional armor and damage.
- Ludicrous Difficulty is a hidden Tech that is applied to the AI (Player 2+), that boosts work rate by 20%, along with giving their Military Units additional armor and damage.

As these already have difficulty modifiers, you may not need or want to modify them further.
If you do want additional effects, you can detect these mods with a `Player: Tech Status` condition, looking for:
- StoryModeGeneral, Active on Player 1
     - Story Mode is considered Standard difficulty by the game otherwise
     - Conditions detecting Standard difficulty will also activate unless they have a second Condition for the tech not being active.  If you wish to create specific effects that do not activate in Story Mode.
- LudicrousModeGeneral, Active on an AI Player
     - Ludicrous is considered Titan Difficulty by the game otherwise
     - Conditions detecting Titan difficulty will also activate unless they have a second Condition for the tech not being active.  If you wish to create specific effects that do not activate in Ludicrous.

## Campaign Progression:
Campaign Progression is largely handled by the [Campaign.xml](https://github.com/Skrylas/AoMR-TutorialCampaign/blob/main/TutorialCampaign/game/campaign/LearnToPlay/ltpc.xml) file (see [XML Guidance](https://github.com/Skrylas/AoMR-TutorialCampaign/blob/main/Docs/XML%20Guidance.md)), but within the campaign scenario, there are required triggers to advance a Campaign.
| Effects  | Description | Screenshot |
| ------------- | ------------- | ------------- |
| Campaign: Advance to the Next Mission  | Immediately loads the next mission in order.  Typically used to automatically load a separate cinematic mission upon winning a playable mission.|
| Campaign: Advance to the Next Mission Prompt |  Loads a Prompt for the player to choose to Quit or advance to the next mission.  Used between missions that have no separate cinematic scenario, or at the end of a cinematic scenario to act as the real "ending".|![image](https://github.com/user-attachments/assets/3e206ffc-f4e1-43db-b13c-402fa66c3af0)|
| Campaign: Advance to the Next Mission Prompt Skip |  An odd trigger.  This allows custom text with a Yes or No.  Clicking Yes Returns player to the standard Victory Screen, Clicking No displays a standard Campaign Advancement Prompt from above.  If the Display Prompt option is set to OFF, then both buttons return players to the standard victory screen. |![image](https://github.com/user-attachments/assets/6873e728-cea0-44d5-bd36-f51c6de0b947)|
| Campaign: Lose Mission |  Prompts a defeat |![image](https://github.com/user-attachments/assets/988bbf2a-ef75-4d77-8d59-fe70fb3313f2)|
| Campaign: Start New Campaign |  Allows custom text, and will load the 1st mission of the listed [Campaign.xml file](https://github.com/Skrylas/AoMR-TutorialCampaign/blob/main/Docs/XML%20Guidance.md).  This should just be `YourCampaignFolderName\YourCampaign.xml` that is contained with the `game\campaign` folder. If the Filepath is not valid, nothing will load.   |![image](https://github.com/user-attachments/assets/ff8646f5-9ad0-4cf0-8831-8e5c0fbbae80)|
| Tutorial: Advance to Fall of The Trident Campaign Prompt |  Prompts going to the FOTT Campaign   |![image](https://github.com/user-attachments/assets/af00b0fc-2559-4023-87f7-2b71fd6e1b26)|
| Scenario: Go to Main Menu |  Immediately goes to the Main Menu.  Is used for the Final Mission or Cinematic Scenario of all Campaigns  |

On the Final Mission or Cinematic of your Campaign, you should use `Scenario: Go to Main Menu`, as attempting to Advance to the Next Mission will cause a hard-lock on a Victory Message wth no controls if there is no next mission to Advance to.  `Campaign: Start New Campaign` is also an option on the final Mission to direct players to a different campaign or even to the first mission of the same Campaign.

## Victory and Loss:
The main Campaigns tend to use a fairly standard 5 Victory and Loss triggers, this handles smooth transitions allowing Victory/Loss sounds to play with a Fade into the UI prompt:

- **Lose_01**
     - Cinematic: Fade Screen, Duration `1000`, Delay `3000`, Activate `Lose_02`
     - Sound: Play Sound File, `events\lose.wav`
     - Music: Stop / Sound: Block All Sounds
- **Lose_02**
     - Campaign: Lose Mission
- **Win_01**
     - Display: Victory Message, ID `STR_SHARED_VICTORY`, Sound `events\win.wav`
     - Trigger: Activate `Win_02`
- **Win_02**
     - Timer Milliseconds `2000`
     - Cinematic: Fade Screen, Duration `2200`, Delay `1000`, Activate `Win_03`
     - Music: Stop / Sound: Block All Sounds
- **Win_3**
     - Campaign: Advance to the Next Mission / Campaign: Advance to the Next Mission Prompt
 
## Misc:
It appears that Scenarios when part of a Campaign start in Cinematic Mode.  If the Mission is not intended to start in Cinematic Mode, you should have a Trigger to Enter and Exit Cinematic Mode immediately on start.
