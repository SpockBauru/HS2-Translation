# HS2 Translation

English fan translation project for Honey Select 2. The translations are applied while the game is running and do not require replacing or modifying any game files.

## Prerequisites

- [BepInEx 5.4](https://github.com/BepInEx/BepInEx/releases/tag/v5.4.8)
- [BepisPlugins for HS2](https://github.com/bbepis/BepisPlugins/releases)
- [XUnity.AutoTranslator](https://github.com/bbepis/XUnity.AutoTranslator)
- [HS2_TextResourceRedirector](https://github.com/IllusionMods/TranslationTools#textresourceredirector) (required for most resources)
- [HS2_Subtitles](https://github.com/DeathWeasel1337/KK_Plugins#subtitles) (required to see subtitles)
- [HS2_TranslationHelper.v1.1](https://github.com/GeBo1/GeBoPlugins/releases/tag/r16) (Optional, but recommended. Translates Japanese names into the Western alphabet without trying to translate into English avoiding mistakes like 悟飯=Food instead of 悟飯=Gohan).
- [HS2_TranslationCacheCleaner](https://github.com/GeBo1/GeBoPlugins#translationcachecleaner) (optional, but recommended)

## Installation

1. Ensure you have the prerequisites installed.
2. Go to the "releases" page above and download the latest version. Alternatively, advanced users can get the latest beta translations by clicking on the "Clone or download" button above. If you are a translator, read the sections below to see how to contribute to the translations.
3. Extract the zip and place the BepInEx folder inside your game folder (where the file "HoneySelect2.exe" is).

## Contribution

Any help is appreciated. Regardless of your translation skill and Japanese knowledge you can still help with translations. Even if you have no experience, you can help by proofreading or using machine translation services such as Google Translate or [DeepL](https://www.deepl.com/translator) (we currently recommend to use [DeepL](https://www.deepl.com/translator)). In the case of machine translations, clean up the translation using sanity and a little logic.

Translation done purely by machines must be kept in the designated files (`zz_machineTranslation.txt` files within `RedirectedResources`). These should be considered placeholders until manual translations are available (those should go into `translation.txt`). The goal is to have everything, manually translated.

### Basic operation and structure

Each translation line follows the pattern: 
```
original text=translated text
```
Example: 
```
悟飯=Food
``` 
Lines beginning with `//` are considered comments, i.e., they are not considered in the translation.

The translations are all inside the `Bepinex\Translation\en` folder. They are then split into the following directories:
- `RedirectedResources` - Replaces the texts embedded in the game files. These translations are loaded only when the game needs the corresponding file, so it is preferable to use this directory instead of the `Text` directory because of its accuracy and performance. This directory mimics the structure of the game, placing a folder for each resource file (such as the ".unity3d" files).
- `Text` - Generic translations that are loaded when the game opens. All texts that are not translated in `RedirectedResources` are checked into this directory. If there is no translation, then the original untranslated text is displayed in the game, Google Translator is called, the translated text is written to `_AutoGeneratedTranslations.txt` and only then the translation is displayed in the game. The text in this folder can be handled with regular expressions (Regex), resized, and separated by game scene instead of being separated by files. This directory is often used in user interfaces (UI) because of these features.
- `Text\Localizations` - Strings under this folder were dumped via TextDump. Translations can be added for missing entries, but new entries should not be added or merging future dumps will become difficult. Basically, don't mess with it.
- `Text\zz_MachineTranslations` - Old folder to Machine Translations, useful for testing. Now Machine Translations go to `RedirectedResources`, read the "Resource Translation" section.
- `Texture` - Contains the translated version of game images. The game images are translated using image editing software. If available the source files (`.psd`, `.xcf`, etc.) files can be found in the project's `Image Source Files` folder.

Coordinate with other translators on the [Illusion Soft Discord server](https://discord.gg/illusionsoft) #translation channel. To avoid translation conflicts please ask if anyone is working on a file. If you have any questions about the quality of your translations, ask for advice on the server.

### How to add or improve translations

- If you want to make a simple edit simply open the file in question and click edit. After you are done editing, commit the changes and stall a pull request.
- If you have more translations to submit [fork the repository](https://help.github.com/articles/fork-a-repo/). This will make a copy of the original project in your account. Upload your changes to the fork into your account, and then [send a pull request](https://help.github.com/articles/about-pull-requests/) to the original project. Your pull request will be reviewed and accepted after a quality check. Again, avoid raw machine translations. Proper capitalization, punctuation, and spelling is a must.

## Text Translations

Texts that are not translated in `RedirectedResources` use the `Text` directory. In this directory the first translation found for a given text is used every time that this same text is found. But sometimes the same word can have different meanings depending on where you are in the game, in this case you can use the "scope level" feature to tell which translation should be used in that part of the game.

### Scope Levels

To use scope levels, use the following structure:
```
#set level xxx
text=translation
text2=translation2
#unset level xxx
```
Where "xxx" represents the number of the desired scope level. Below is a table containing the known scope levels and their locations:

#### Known Scope Levels

| Level | Description           |
|------:|-----------------------|
| -1    | (global)              |
| 0     | Dialogs               |
| 1     | Settings Menu         |
| 2     | Main Menu             |
| 3     | Character Maker       |
| 4     | My Room               |
| 6     | ADV dialog scenes     |
| 7     | H scenes              |
| 8     | Lobby                 |
| 9     | Fur's Room            |
| 10    | Card Uploader         |
| 11    | HS/AI Downloader      |
| 13    | Network Splash Screen |
| 14    | Character Search      |
| 15    | Vip Lobby             |

##  Resource Translation

The folder `RedirectedResources` is the main translation directory for the game, so it gets special treatment.

Inside each folder there is a file named `translation.txt`, this is the file where the translations should go. In some folders there is also the file `zz_machineTranslation.txt` which is where machine translations go, that usually have a lower quality.

Every `translation.txt` file has the raw Japanese text that needs translations. Each one starts commented out (`//` at the begining) so it will not be loaded. For your text to display correctly in game, put the translation on the right side of the equal sign and remove the `//` at the start of the line. Do not edit the Japanese text or the translation will not work. Example:

Before:
```
//Tシャツ=
```
After:
```
Tシャツ=T-shirt
```

The file `zz_machineTranslation.txt` can only have the translation lines that are commented out in `translation.txt`. If the file `translation.txt` has been fully translated, the file `zz_machineTranslation.txt` should be deleted. The goal of this translation project is that none of the `zz_machineTranslation.txt`" files remain.

The `assets` folder inside of `Bepinex\Translation\en\RedirectedResources` can be compressed into a .zip archive to be read by the game (simply right-click on the assets folder and then compress to .zip). Uncompressed files under `assets` are also still loaded. The game has to be restarted in order to see updated translations.


The plugin [TextResourceRedirector](https://github.com/IllusionMods/TranslationTools#textresourceredirector) is required for these translations. Always keep it updated.

### Structure of the "RedirectedResources" directory

Table with the localization of the translations for each part of the game:

| Folder                            | Description               |
|-----------------------------------| --------------------------|
| `adv`                             | Main game dialogs         |
| `etcetra/list/config`             | Personalities             |
| `etcetra/list/parametername`      | Traits, H Traits, State   |
| `gamedata/achievement/achivement` | Achievements              |
| `gamedata/achievement/exchange`   | Unlockables/powerups,     |
| `gamedata/bgmname`                | BGM titles                |
| `gamedata/eventcontent`           | Current activity/urge     |
| `map/list/mapinfo`                | Map names                 |
| `list/characustom`                | Maker stuff               |
| `list/h/animationinfo`            | Positions (game versions) |
| `list/h/sound`                    | Sex scenes subtitles      |
| `spr/list/*/planname`             | VIP services names        |
| `studio`                          | Studio stuff              |

#### Personalities

Location of the files for each girl's personality:

| ID | Name   | Eng Name     | Dialog (`adv/scenario/`) | Subtitles (`list/h/sound/voice/*/`)                                             |
|----|--------|--------------|--------------------------|---------------------------------------------------------------------------------|
| 0  | クール  | Composed     | `c00`                      | `hvoicestart_c00_*`, `hvoice_c00_*`, `hvoicestartevXX_c00*`, `hvoiceevXX_c_00*` |
| 1  | 普通   | Normal       | `c01`                      | `hvoicestart_c01_*`, `hvoice_c01_*`, `hvoicestartevXX_c01*`, `hvoiceevXX_c_01*` |
| 2  | 苦労人 | Hardworking   | `c02`                      | `hvoicestart_c02_*`, `hvoice_c02_*`, `hvoicestartevXX_c02*`, `hvoiceevXX_c_02*` |
| 3  | 女友達 | Girlfriend    | `c03`                      | `hvoicestart_c03_*`, `hvoice_c03_*`, `hvoicestartevXX_c03*`, `hvoiceevXX_c_03*` |
| 4  | ギャル  | Fashionable  | `c04`                      | `hvoicestart_c04_*`, `hvoice_c04_*`, `hvoicestartevXX_c04*`, `hvoiceevXX_c_04*` |
| 5  | 気弱   | Timid        | `c05`                      | `hvoicestart_c05_*`, `hvoice_c05_*`, `hvoicestartevXX_c05*`, `hvoiceevXX_c_05*` |
| 6  | 母性的 | Motherly      | `c06`                      | `hvoicestart_c06_*`, `hvoice_c06_*`, `hvoicestartevXX_c06*`, `hvoiceevXX_c_06*` |
| 7  | ドS    | Sadistic    | `c07`                      | `hvoicestart_c07_*`, `hvoice_c07_*`, `hvoicestartevXX_c07*`, `hvoiceevXX_c_07*` |
| 8  | オープン | Open-Minded  | `c08`                      | `hvoicestart_c08_*`, `hvoice_c08_*`, `hvoicestartevXX_c08*`, `hvoiceevXX_c_08*` |
| 9  | 天然   | Airhead      | `c09`                      | `hvoicestart_c09_*`, `hvoice_c09_*`, `hvoicestartevXX_c09*`, `hvoiceevXX_c_09*` |
| 10 | 几帳面  | Careful      | `c10`                      | `hvoicestart_c10_*`, `hvoice_c10_*`, `hvoicestartevXX_c10*`, `hvoiceevXX_c_10*` |
| 11 | 大和撫子 |Ideal Japanese| `c11`                      | `hvoicestart_c11_*`, `hvoice_11_*`, `hvoicestartevXX_11*`, `hvoiceevXX_c_11*` |
| 12 |ボーイッシュ| Tomboy       | `c12`                      | `hvoicestart_c12_*`, `hvoice_c12_*`, `hvoicestartevXX_c12*`, `hvoiceevXX_c_12*` |
| 13 | ヤンデレ | Obsessed     | `c13`                      | `hvoicestart_c13_*`, `hvoice_c13_*`, `hvoicestartevXX_c13*`, `hvoiceevXX_c_13*` |
| -1 | フュル  | Fur          | `c-1`                      |                                                                                 |
| -2 | シトリー | Sitri        | `c-2`                      |                                                                                 |

### Specialized translation lines

There are some specialized resources handled by the resource redirection that require some addititional handling.

#### Format strings

Format strings have replacements in them processed by [`String.Format`](https://docs.microsoft.com/en-us/dotnet/api/system.string.format?view=netframework-4.6#Starting).  The sections that are replaced by the game engine will look like `{0}`, `{1}`, `{2}`, etc.  Usually they are a character name or the name of some item.  The same replacements found in the original string should exist in the translated string.

Example:
```
{0}と仲がいいと思ってるわ=I think I'm good friends with {0}.
```

#### ADV Choices

Because these strings are encoded into a larger entry in the resource files they require special handling by TextResourceRedirector to ensure the text that should no be replaced remains untouched, while allowing the displayed text to be translated. These lines will start with `CHOICE:` followed by the text that needs to be translated.  On the right side of the `=` you need only include the translated text without the `CHOICE:` prefix.

Example:
```
CHOICE:受け取る=Accept
```

#### Optional Prefixes

There are a number of assets that support the use of optional prefixing to get a more exact match. This allows for more specific translations in cases where multiple assets might match the same replacement code.  Matching for these assets will first try the prefixed match, then fall back to the standard un-prefixed match.  Given the following translation file:

```
PREFIX1:こんにちは=Hi!
こんにちは=Hello.
```

Trying to match `こんにちは` for an asset using `PREFIX1` would return `Hi!`, where an asset using `PREFIX2` would fall back to `Hello.`.

| asset location               | prefix        | Notes                                                                               |
|------------------------------|---------------|-------------------------------------------------------------------------------------|
| `etcetra/list/parametername` | `HATTRIBUTE:` |                                                                                     |
| `etcetra/list/parametername` | `MIND:`       |                                                                                     |
| `etcetra/list/parametername` | `STATE:`      |                                                                                     |
| `etcetra/list/parametername` | `TRAIT:`      |                                                                                     |
## Tools

- [Release Tool](https://github.com/SpockBauru/TranslationToolsHS2#releasetoolhs2) - Tool that cleans up the translation files to remove any unnecessary untranslated parts.
- [Yomichan](https://foosoft.net/projects/yomichan/) - This browser plugin allows you to see the definition of Japanese words by putting your mouse over them in the browser and pressing shift.
- Dictionaries:
  - https://jisho.org/
  - http://www.romajidesu.com/
