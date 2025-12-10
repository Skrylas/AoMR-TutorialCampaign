# Triggers

## Difficulty:
Difficulty for Campaigns overlaps with standard Skirmish/Scenario gameplay, with some exceptions as seen in the below table.
The Condition Scenario: Difficulty Level features difficulties from the Skirmish Column below:
| Skirmish Difficulties  | Campaign Difficulties |
| ------------- | ------------- |
| -  | Story Mode  |
| Standard  |  Standard  |
| Moderate  |  Moderate  |
| Hard  |  Hard  |
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
| Campaign: Advance to the Next Mission Prompt Skip |  This trigger is used in the campaign for prompting the player to view hidden tutorial missions.  This allows custom text with a Yes or No.  Clicking Yes advances the player to the next mission immediately, Clicking No brings up a standard campaign advancement prompt which skips the next mission, and advances to one beyond.  It should be noted that the 3rd mission should have a pre-requisite of the 1st mission, in the case of the 2nd mission being skipped and the player decides to Quit the campaign, having the pre-requisite setup this way ensures Mission 3 will be visible upon returning to the Campaign.  If the Display Prompt option is set to OFF, then both buttons return players to the standard victory screen (if there is something I am missing here, please let me know). |![image](https://github.com/user-attachments/assets/6873e728-cea0-44d5-bd36-f51c6de0b947)|
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
- **Win_03**
     - Campaign: Advance to the Next Mission / Campaign: Advance to the Next Mission Prompt

## Persistant User Data:
With the launch of Retold, Age of Mythology now supports saving Data between scenarios by default.  This is utilized by the default campaign to update and add visuals to the Greek main menu as you progress through Fall of the Trident.
- These are stored in the `C:\Users\Usename\Games\Age of Mythology Retold\SteamID\user\UserProfile.xml`
- When a Scenario processes saving the UserData, they are saved under a `<scenariodata name="ScenarioName">` tag.
     - You are given 16 Variable Index slots (0-15) per scenario, and each Variable is stored as an integer (whole number).
     - If one has more than 15 Variables per scenario to carry between their campaign scenarios, you could add multiple variables together, for example using one variable in the Tens place, and another in the Hundreds place.
 
- **Triggers**
     - **User: Set Scenario User Data**: Sets an Index Variable to the value you choose.
     - **Quest Variable: Set Scenario User Data**: Sets an Index Variable to the value equal to a Quest Variable.  You can utilize other Quest Variable triggers to modify this value.
     - **Quest Variable: Get Scenario User Data**: Obtains the Variable set in the prior two trigger effects.  The Name field is the Name of the Scenario, this will be the `<scenariodata name="ScenarioName">` tag in the `UserProfile.xml`.

## External UI:
With the launch of Heavenly Spear, a new trigger function was introduced, allowing the loading of UI elements from an .xaml file.  This is utilized in only one place, the title card of the Heavenly Spear campaign during its opening cinematic.  
     - **UI: Load Custom UI Resources**: `/Content/InGame/HUD_CampaignResources_YAS.xaml`.  
     - To unload this resource, the same Trigger Effect is then utilized with no resource path.  

## Misc:
There appears to be a potential bug that Scenarios in a Campaign may start without a UI.  If a mission does not start with a cinematic you should create a Trigger to Enter and Exit Cinematic Mode to prevent this, both effects can be part of the same trigger.

## Alternate Player
<img align="right" src="https://github.com/user-attachments/assets/0bad4cde-cb3e-4137-b602-f63db174c8d1"> Popular with alternate scenario missions where players play the role of a villain or supporting town, if you wish to edit a scenario, or create a scenario in which the player plays as any slot other than Player 1, this can simply be done by changing the Active Player selection within the editor in the upper-right navigation bar of the editor:

This will prompt a warning that the Active Player is not set to Player 1 upon Saving the scenario; Click Yes.
- Don't forget to set the PlayerData to Human for the actively controlled player in the scenario data along with any other adjusted player data required.
- Upon loading the scenario in the campaign the player will control the set player number.
