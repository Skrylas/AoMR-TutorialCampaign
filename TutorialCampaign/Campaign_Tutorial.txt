Welcome to the Tutorial Campaign, Campaign Tutorial.
A remake of the original AoM Tutorial, while also being a tutorial on how to make your own campaign.

Making your own Campaign for Age of Mythology Retold can be easy, but includes several steps:

## Location of your Campaign Files: ##
1) Locate your AoMR Mods Folder at: C:\Users\USERNAME\Games\Age of Mythology Retold\STEAMUSERID\mods
2) Open the local folder.
3) Create a new folder - this will be the name of your campaign.  Once we have created a local copy, it can be uploaded to the in-game mod manager.

## File Structure: ##
1) Inside your newly named folder, you should create a folder named "game" - this will hold ALL campaign files.
2) The following folder structure depicts all possible folders and files you may use, this guide will cover all of them.

game
├───campaign
│   └───YOUR_CAMPAIGN_NAME
│       ├───YOUR_CAMPAIGN_NAME.xml
│       └───YOUR_SCENARIOS.mythscn
├───data
│   └───strings
│       ├───english**
│       │    └───stringmods.txt
│       └───gameplay*
│            ├───techtree_mods.xml*
│            └───proto_mods.xml*
├───sound*
│   └──YOUR_CAMPAIGN_NAME*
│       └───YOUR_SOUNDS.mp3*
└───ui_myth*
    └───resources*
        └───YOUR_CAMPAIGN_NAME*
            └───CAMPAIGN_IMAGES.png*

  *  optional files - can be included if your campaign makes use of them
  ** or another language or multiple
	Currently there appears to be an issue where multiple languages cannot be properly swaped between in custom campaigns.

The above file structure largely replicates the base AOMR file structure.
As noted, the only 2 mandatory folders are the actual Campaign folder, which contains your scenarios, and the Strings folder which tells the game what the name of the Campaign and the Scenarios are.

## Campaign Folder: ##
Inside your campaign folder there will be an .xml file, which determines what files are loaded, in what order, and what is displayed for each.
This folder should also include all scenarios that you wish to be loaded as part of your campaign, both playable and cinematics.

Open the included campaign.xml for notes and references on how to setup your campaign file: 
	\TutorialCampaign\game\campaign\LearnToPlay\ltpc.xml

This can also be used as a template for your own campaign.

## Data Folder: ##
Must always include a Stringmods.txt file - this includes Text strings that tell the game what your campaign is named, and the name of your scenarios.  These will be referenced in the above campaign.xml file.
Stringmods can also be used to create recurring texts to be references in your campaign - you can also reference the existing base strings.

The Data folder can also include various datamods that are included as part of your campaign these can include Proto and TechTree mods if you have them.
This guide won't get into data modding.

When you upload your Campaign into the Mod Manager, it will be tagged as a Datamod due to the usage of Stringmods.txt, but it does not count as a Datamod for purposes of Multiplayer, or Celestial Challenges.
This is only for the in-game mod manager.
If you upload it on the website, make sure not to Tag it as a Datamod, or it will count as one.

## Sound Folder: ##
Can contain any sounds you want to reference in your campaign.  As long as the file-path matches, these can be played in a Dialogue/Sound trigger.
These DO NOT need to be in the new FMOD/Bank format.

To reference sounds used in this folder in Dialogue/Sound triggers, the path must be everything after the base sound folder.
For example, if you included a file named Test.mp3 directly in the Sound folder with no subfolders, it should just be referenced in-game as Test.mp3.  To prevent conflicts, it is recommended that you include a Subfolder of your Campaign name.

## UI Folder: ##
Can contain any UI elements you wish to reference in your campaign:
Talking heads, icons, spotlight images, campaign map backgrounds, pins, loading screens, etc.
Same as Sound, as long as the file-path matches when they are referenced, they can be used in-game and in the campaign.xml.

## Uploading Your Campaign: ##
Once your campaign is complete, it can be uploaded from the in-game mod manager, or on the Age of Empires website.
Note: The mod is tied to the account that uploaded it, if you use different accounts, such as playing in-game on Steam, and using a Microsoft Account for the website.
As long as you use the same account for both, you can manage and update your Campaign from both sources, no matter which you used to initially upload it.

Publishing is easily done from the in-game manager.  You simply click View on your Local Mod in the manager, and then Publish.

From the website manager, the campaign needs to be uploading in a .zip folder as follows:
	CampaignName.zip/game
Do not include a subfolder of your Campaign Name inside the .zip folder, or it will not show up.

When uploading on the website, it should also NOT be tagged as a Datamod, or it will be incompatible with Multiplayer.  


## Updating Your Campaign: ##
Updating is done similarly.  All changes will be made to your local copy, and you will have a button to Update the Online version.
If you no longer have a local copy, you can browse to your Online version, and click the button that says "Make Local Copy".