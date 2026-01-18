# Strings

A Strings file is optional for Campaigns, but is required for files utilizing `<DisplayNameStringID>` rather than `<DisplayName>` and `<RolloverStringID>` rather than `<Rollover>` for Campaign Scenario Names and Descriptions in the [Campaign.xml](https://github.com/Skrylas/AoMR-TutorialCampaign/blob/main/Docs/XML%20Guidance.md).

But a Strings file can also be used for any other text in the game.
Utilizing a Strings file allows you to put all text in a single file/location for proof-reading and editing, and strings can be reused across your missions, allowing a single edit to change all instances.

## File Setup
For examples look at:
- [The example included here](https://github.com/Skrylas/AoMR-TutorialCampaign/blob/main/TutorialCampaign/game/data/strings/english/stringmods.txt)
- The default files located at `game\data\strings` (requires a .BAR extractor)

Your file should include these two lines:
```
Language = "English"
IsRtl = "False"
```
And then an Entry for each String.
`ID = "YOUR_STRING_ID"   ;   Str = "Your text here."`
The string ID should be Unique, and the text contained within the two quotes can be anything, and can include icons and color tags as described below.


## Text Strings
Text strings in the `stringmods.txt` file can include colors and images.
- These can be used inside in any place that accepts Strings inclduding: Campaign and mission names, world prompts, dialogue, etc.

### Color
Standard Color Formatting: `<color=r0,g0,b0> </color>`
- The original Color tag from AoM, these represent the percentage of each color from 0.0 - 1.0.

Retold Color Formatting: `<color=r0:g0:b0,r1:g1:b1> </color>`
- r0: Inside red,
g0: Inside green,
b0: Inside blue,
r1: Outside red,
g1: Outside green,
b1: Outside blue
- As with the original AoM color code, values should be from 0.0 - 1.0 to represent the percentage of each color.
    - Going beyond 1.0 is accepted by the game, and causes color distortion.
 
### Images
Images can be included in Strings: `<icon=\"(X,Y)(imagepath\image.png)\">`
- Images cannot have their proportions changed, but can be resized.
    - The proportion of Horizontal and Vertical size should be consistent with the original image, or it will have dead space around it.  See the examples below.
    - The image will be re-sized proportionally in game if either the X or Y are smaller than the original image.
    - If an image is not given a Vertical size, it will be treated as a Square.
- Example of X only, image size is Square and the original Icon is square:
    - `"<icon=\"(32)(resources\front_end\Lobby\icon_inputmode_mouse.png)\"> Hotkey Trainer <icon=\"(32)(resources\front_end\Lobby\icon_inputmode_gamepad_x.png)\">"`
    - ![image](https://github.com/user-attachments/assets/7b2e57c7-74ab-408c-bd1f-d787ec47c9a8)
- Example of X and Y sizes consistent with original image proportion (518,147):
    - `"<icon=\"(518,147)(resources\in_game\Victory_Defeated\victory_hades_top_ornament.png)\">"`
    - ![image](https://github.com/user-attachments/assets/f95bd503-3df4-4a2a-9498-e738b8b4ae72)
- Example of X, with a Y that is too small (518,50):
    - `"<icon=\"(518,50)(resources\in_game\Victory_Defeated\victory_oranos_top_ornament.png)\">"`
    - ![image](https://github.com/user-attachments/assets/62ea149a-bbb3-408b-9678-9979fc4deea0)
    - This shows it is impossible to resize images.  As the Vertical is too small, the entire image becomes resized to its proportion.

  



