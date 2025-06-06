# Campaign.xml

## The Main .xml File
`game\campaign\YourCampaignName\YourCampaignName.xml`

The Campaign.xml file is required to tell the game what your Campaign is named, what the scenarios in the campaign are, and the order they show up in.  Missions are played in the order that they are set in the Campaign.xml file.   
Including multiple .xml files in the same Campaign folder does not appear to work at this time, and are read by the game in alphabetical order.

For examples look at:
- [The example included here](https://github.com/Skrylas/AoMR-TutorialCampaign/blob/main/TutorialCampaign/game/campaign/LearnToPlay/ltpc.xml)
- The default files `steamapps\common\Age of Mythology Retold\game\campaign\fott\fott.xml`

## .xml Tags
Your .xml file should include the folowing:
`<?xml version = "1.0" encoding = "UTF-8"?>`
And the entire file should be wrapped in a `<Campaign> </Campaign>` tag.


Your Campaign info itself is handled by the base information at the top:

| Campaign Header Tag | Effect |
|----|----|
|`<DisplayNameStringID>`|References a StringID in your StringMods or the default StringTable for the name of your campaign.|
|~~`<RolloverStringID>`~~|References a StringID in your StringMods or the default StringTable for the description of the campaign.  Custom Campaigns do not appear to have a visibile description.  This is also evidenced by the Mythical Battle using a filler StringText for its description.|
|~~`<MotifImage>`~~|The image that appears in a campaign's box.  Custom campaigns and Mythical Battles do not appear to ever show this.  The Mythical Battle .xml uses the FOTT Motif as filler.|
|`<MapImage>`|The map that your campaign is based on, where pins will be placed.  Default maps are stored in `game\art\ui\campaign_map`.  Excluding this tag will load a generic background, but not allow Pins to show, there needs to be a map for them to be placed on.|
|~~`<CompendiumImage>`~~|Only for default campaigns, unless you were going to edit the Compendium files.|
|~~`<CompendiumTopic>`~~|Only for default campaigns, unless you were going to edit the Compendium files.|
|~~`<HideFromMainPage>`~~|Value of 1 to hide.  Does not appear to be needed.  The Mythical Battle uses this tag, Custom Campaigns do not need it.|

Each individual Playable Scenario or Cinematic Scenario in your Campaign will also need a Campaign Node.
Each Scenario should start and end with a `<CampaignNode> </CampaignNode>` and can include the following tags:

| Campaign Node Tag | Effect |
|----|----|
|`<Filename>`|The filepath for the scenario.  This should be the `CampaignFolder\ScenarioName`.  This can also reference different campaigns and campaign folders.|
|`<DisplayNameStringID>`|References a StringID in your StringMods or the default StringTable for the name of the scenario.|
|`<RolloverStringID>`|References a StringID in your StringMods or the default StringTable for the description of the scenario.  Appears at the bottom of the campaign window.|
|`<BackgroundImage>`|The image that appears in the faded background and the visible foreground when loading a mission|
|~~`<LoadImage>`~~|Does not appear to do anything.  The Default Campaigns always have this set to match the filepath of `<BackgroundImage>`, as that controls both the background and foreground image while loading, it is not apparent what this tag controls.|
|`<MapImageOverride>`|Loads a different map than the default when this mission is selected. Default maps are stored in `game\art\ui\campaign_map`|
|`<PinImage>`|The map character/pin that displays on the map when the mission is selected. Default pins are stored in`game\art\ui\campaign_map\pins`.  See [this guide by Modding AoM](https://www.youtube.com/watch?v=Fu3XmTmEubc) for creating custom Pins.|
|`<PinXPosition>`|The X coordinate of where the Pin is placed on the map.  Appears to be percentage based, and should be between 0.0 and 1.0|
|`<PinYPosition>`|The Y coordinate of where the Pin is placed on the map. Appears to be percentage based, and should be between 0.0 and 1.0|
|`<PinZoom>`|Controls how zoomed out the map is for numbers between 0.0 and 1.0.  Numbers above 1.0 default to 1.0 zoom.  The lower the number the more zoomed out the map is.|
|`<PrereqScenarioFile>`|Should match the `<Filename>` of the Scenario that takes place before this.  This tag hides the Scenario until the PrereqScenario is beaten.  If this tag is NOT included, then it will always be visible and selectable.  This does not determine the order missions are played in, just when they become visible, missions are played in the order listed.|
|`<HasPrompt/>`|Creates a Yes/No Prompt when selecting the mission to load the Scenario listed before this one in the .xml file.  In the Default Campaign this is used to load the `tutorial\ccnor` Norse Tutorial, which is listed as a hidden scenario in the tgg.xml and mythb.xml.  Requires a `<PromptStringID>` tag to have a description.  If the mission has been completed, Prompts will not appear in the future.|
|`<PromptStringID>`|Gives the above tag a description. ![image](https://github.com/user-attachments/assets/20d3aa1e-0fca-4dae-8cab-93b7fddd5c13)|
|`<Visible>`|When set to 0 hides the campaign from the mission list. Not needed if the mission is meant to be visible.  Typically used for Cinematic Scenarios or Prompted tutorials.|
|`<Cinematic>`|When set to 1 marks the mission as a cinematic.  It is not used on non-cinematic missions.  It is not apparent what this does.|
|`<PlayCinematic/>`| Introduced in POTG and only used in the POTG.xml on all missions that precede a Cinematic Mission.  Appears to replace the prior `Cinematic` tag, as POTG cinematics are not tagged as cinematics, instead tagging the prior mission with this.|


