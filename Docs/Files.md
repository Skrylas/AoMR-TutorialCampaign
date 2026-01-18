# File Structure and Uploading

## Location of your Campaign Files:
1) Locate your AoMR Mods Folder at: `C:\Users\USERNAME\Games\Age of Mythology Retold\STEAMUSERID\mods`
2) Open the local folder.
3) Create a new folder - this will be the name of your campaign.  Once we have created a local copy, it can be uploaded to the in-game mod manager or on the website.

## File Structure:
1) Inside your newly named folder, you should create a folder named "game" - this will hold **ALL** campaign files.
2) The following folder structure depicts possible folders and files you may use, this guide will cover these.
   
```
game
├───campaign
│   └───YOUR_CAMPAIGN_NAME
│       ├───YOUR_CAMPAIGN_NAME.xml
│       └───YOUR_SCENARIOS.mythscn
├───data*
│   ├───strings*
│   │   └───english**
│   │       └───stringmods.txt*
│   └───gameplay*
│       ├───techtree_mods.xml*
│       └───proto_mods.xml*
├───sound*
│   └──YOUR_CAMPAIGN_NAME*
│       └───YOUR_SOUNDS.mp3*
└───ui_myth*
    └───resources*
        └───YOUR_CAMPAIGN_NAME*
            └───CAMPAIGN_IMAGES.png*
```

  `*  optional files - can be included if your campaign makes use of them`  
  `** or another language or multiple`  
  		`Currently there appears to be an issue where multiple languages cannot be properly swapped between in custom campaigns.  If someone discovers that this has been fixed, please let me know.`  

The above file structure largely replicates the base AOMR file structure.

As noted, the only 2 mandatory folders are the actual Campaign folder, which contains your scenarios, and the Strings folder which tells the game what the name of the Campaign and the Scenarios are.

### Campaign Folder:
The Campaign folder will contain two things ([Tutorial Example](https://github.com/Skrylas/AoMR-TutorialCampaign/tree/main/TutorialCampaign/game/campaign/LearnToPlay)):
- `CampaignName.xml`
- `CampaignScenarios.mythscn`

The .xml file included with your campaign is what creates your campaign inside the game.  It is what controls the names, descriptions, level order, and other details.  
- [Campaign.xml Setup Guidance](https://github.com/Skrylas/AoMR-TutorialCampaign/blob/main/Docs/XML%20Guidance.md)  
- [Example .xml file from the Tutorial Campaign with notes](https://github.com/Skrylas/AoMR-TutorialCampaign/blob/main/TutorialCampaign/game/campaign/LearnToPlay/ltpc.xml)  

The .mythscn files are your levels themselves, created within the editor.  
You can also include Subfolders, such as a `game\campaign\YourCampaignName\cinematics` folder.
- This is purely for organizational purposes to help keep track of your missions.  The .xml file can reference any folders or subfolders contained within the main `game\campaign` folder.
    - This can allow you to reference other campaigns, or even include two campaigns inside the same Mod that reference each other.

### Data Folder (optional):
This folder is typically used to include a `Stringmods.txt` file.
- Stringmods.txt includes Text strings that your campaign may make use of.  
    - This can include the name of your campaign and the name of your scenarios, which can be referenced in the above campaign.xml file if StringID versions of DisplayName and RollOver are utilized.
    - Stringmods can also be used to create recurring strings of text for your campaign, such as Civilization names, Character names, Dialogue, etc.  Any piece of text your campaign may contain.  You can also reference the existing base strings included in the game.
- [Strings guide](https://github.com/Skrylas/AoMR-TutorialCampaign/blob/main/Docs/Strings.md) includes some things that can be accomplished with Stringmods.
- This file is required for the Campaign Name and Scenario Names, but using strings for in-game text also allows you to create a single file for all text in your missions to be reviewed and edited in one location.

The Data folder can also include various datamods that are included as part of your campaign these can include `Proto_Mods.xml` and `TechTree_Mods.xml` if you have them within a `gameplay` subfolder, along with any other data modifications you may want to include.

This guide will not cover data modding.

- **Note:** When you upload your Campaign into the Mod Manager, it will be automatically tagged as a Datamod due to the inclusion of a Data folder.  But Stringmods.txt do **NOT** count as a Datamod for purposes of Multiplayer, or Celestial Challenges.  If you upload it on the website, the Datamod checkbox will be automatically checked, but you can manually uncheck this.
- **Datamodding:** While Datamodding will require your campaign to be toggled off to play Ranked or Celestial Challenges, there is little downside to this, and can enhance your Campaign's functionality.  
    - The [Crybar Editor](https://github.com/CryShana/CryBarEditor/tree/main) includes a guide on [modding basics](https://github.com/CryShana/CryBarEditor/blob/main/Documentation/Modding.md).
    - It is highly reccomended to make your DataMods Additive to maintain compatibility with new civs, content and patches the Devs may add, and compatibility with your fellow modders.

### Sound Folder (optional):
Can contain any sounds you want to reference in your campaign.  As long as the file-path matches, these can be played in a Dialogue or Sound trigger.
These **DO NOT** need to be in the new FMOD/Bank format.  Including standard .mp3 or .wav can be played without issue.

To reference sounds used in this folder in a Dialogue or Sound trigger, the path must be everything after the base sound folder.  
- For example, if you included a file named `Example.mp3` directly in the Sound folder with no subfolders at `game\sound\Example.mp3`, it should be referenced in-game as `Example.mp3`.  
    - To prevent conflicts with other campaigns, it is recommended that you include a Subfolder of your Campaign name of `game\sound\YourCampaignName\Example.mp3` to be referenced in game as `YourCampaignName\Example.mp3`
    - Sounds must be inside the Sound folder, for example a default sound is played by referencing `events\win.wav` which is contained inside `game\sound\events\win.wav`

### UI Folder (optional):
Can contain any UI elements you wish to reference in your campaign:
- Talking heads, icons, spotlight images, campaign map backgrounds, pins, loading screens, etc.
- The file-path must just match when they are referenced.
    - Included images can be used in game and in the Campaign.xml.
    - References tend to start at the resources folder.  For example: `<icon=\"(518,147)(resources\in_game\Victory_Defeated\victory_hades_top_ornament.png)\">`

## Uploading Your Campaign:
Once your campaign is complete, it can be uploaded in two ways:
- In-game Mod Manager
- [Age of Empires website](https://www.ageofempires.com/mods/)

Whenever a mod is uploaded on either source, it syncs to the other.  Although there can be text formatting and feature differences, they will share the same files and description.
- A mod uploaded initially on either platform can be edited on the other.
    - For example:  I can upload my Campaign in-game, and then go on the website to upload an update.
    - **Note:** The mod is tied to the account that uploaded it.  If you use two different accounts, such as playing in-game on Steam, and using a Microsoft Account for the website, you may run into issues managing the mods of your other account.  As long as you use the same account for both, you can manage and update your Campaign from both sources, no matter which you used to initially upload it.

### In-Game Mod Manager
Publishing is easily done from the in-game manager.  
- Find your Local Copy inside the Mod Manager
    - As indicated by a Blue Folder Icon (when unpublished)
- Click View
- Click **Publish Your Mod**

### Website Mods
Publishing on the Website requires making a .zip filder of your mod/campaign
- Create a `YourCampaignName.zip` folder that contains a `game` folder with all subfolders.  For example:
    - `game\campaign\YourCampaignName`
    - `game\data\strings`
    - This should **NOT** include a subfolder of your mod name, it should directly be the `game` folder.  The .zip acts as your ModNameFolder.
- Log in to the website with your chosen account (Steam / MS), and click Submit a Mod.
- Make sure to Select Age of Mythology, and fill in the details.
    - Uncheck the Datamod box if its automatically been tagged as one.
    - The Allow Discussions checkbox automatically creates a forum thread for your mod

### Differences between the two
- The website has higher res photos
    - And allows for up to 5 photos while the in-game mod manager only allows 1.
    - **Note:** If you upload 5 images to the website, and then update your mod using the in-game mod manager it seems to revert the mod to the single photo from the in-game manager, which also lowers its resolution.
- The website allows for people to leave comments when they leave a review, in-game they can only leave a star rating.
    - It is also possible to enable Discussions for your mod, which automatically creates a forum thread for your mod on the official AoE forums.
- The website has a Changelog feature, allowing you to leave a record of your changes.
     - The changelog does not show in-game, for this reason I personally tend to leave important changes in the mod description.

## Updating Your Campaign:
Updating is done similar to Uploading.

### In-Game Mod Manager Update
- If you have a Local Copy of your Mod, proceed to Step 2, otherwise:
    - Find your mod in the Mod Browser
    - Click View
    - Click Make Local Copy (if there is an error, default to website updates)
- Find your Local Copy inside the Mod Manager
    - As indicated by a Pink Folder Icon (now that its published)
- Click View
- Click Upload Update
- **Note:** Updating a mod through the in-game mod manager can revert images uploaded on the website to the sole in-game image.

### Website Mod Update
- Sign In and Click My Mods
    - Change AoE2 to AoM
 - Open your mod and click Edit Mod
 - Make changes and upload a new .zip file with your updated files
    - If you have lost your original files, you can always subscribe to your mod to download a copy.
