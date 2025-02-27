hi.. uh, please use this version of node: https://nodejs.org/download/release/v17.9.1/ if you are going to install all the dependencies from this repository. this is because the latest one just does not work and I wish it was stated in the original GD Browser, but this is cologne we are talking about. 


# GDBrowser

  

Uh... so I've never actually used GitHub before this. But I'll try to explain everything going on here.

  

Sorry for my messy code. It's why I was skeptical about making this open source, but you know what, the code runs fine in the end.

  
  ## How do I run this?
Well, there are 2 ways


From Github:
1) Install [node.js v17](https://nodejs.org/download/release/v17.9.1)
2) Clone/download this repository  
3) Open cmd/powershell/terminal in the main folder (with index.js)
4) Type `npm i` to flood your hard drive with code that's 99% useless
5) (Optional) Type `npm audit fix` and do some random things
6) Type `node index` to run the web server
7) GDBrowser is now running locally at http://localhost:2000

or

1) Get the latest version of node
2) Download this [archive](https://drive.google.com/file/d/12bOrvBdFr9mv1J8LMVqwQ-VCLGdREv0L/view?usp=sharing)
3) Run `node index` in the root directory of the folder and boom it should work.


If you want to disable rate limits, ip forwarding, etc you can do so by modifying `settings.js`. Doing this is probably a good idea if you feel like obliterating Rob's servers for some reason. (please don't)


## Using this for a GDPS?

~~I mean, sure. Why not.~~
Hold up, wait a minute... private servers are an official feature now!


If you would like to add your GDPS to GDBrowser, [fill out this quick form](https://forms.gle/kncuRqyKykQX42QD7) and I'll be happy to add it (provided the server is relatively large and active)
  
  
If you 100% insist on adding a private server to your own magical little fork, you can do so by adding it to **servers.json**. Simply add a new object to the array with the following information:

| identifier       | description                  |
|:----------------:|:-----------------------------:|
| `name`           | The display name of the server |
| `link`           | The server's website URL (unrelated to the actual endpoint) |
| `author`         | The creator(s) of the server |
| `authorLink`     |  The URL to open when clicking on the creator's name |
| `id`             | An ID for the server, also used as the subdomain (e.g. `something` would become `something.gdbrowser.com`) |
| `endpoint`       | The actual endpoint to ~~spam~~ send requests to (e.g. `http://boomlings.com/database/` - make sure it ends with a slash!) |


There's also a few optional values for fine-tuning. I'll add more over time

| identifier       | description                   | type |
|:----------------:|:-----------------------------:|:----:|
| `timestampSuffix` | A string to append at the end of timestamps. Vanilla GD uses " ago" | string |
| `demonList` | The URL of the server's Demon List API, if it has one (e.g. `http://pointercrate.com/` - make sure it ends with a slash!) | string |
| `disabled` | An array of menu buttons to "disable" (mappacks, gauntlets, daily, weekly, etc). They appear greyed out but are still clickable. | array |
| `pinned` | "Pins" the server to the top of the GDPS list. It appears above all unpinned servers and is not placed in alphabetical order. | bool |
| `onePointNine` | Makes a bunch of fancy changes to better fit 1.9 servers. (removes orbs/diamonds, hides some pointless buttons, etc) | bool |
| `weeklyLeaderboard` | Enables the lost but not forgotten Weekly Leaderboard, for servers that still milk it | bool |
| `substitutions` | A list of parameter substitutions, because some servers rename/obfuscate them. (e.g. `{ "levelID": "oiuyhxp4w9I" }`) | object |
| `overrides` | A list of endpoint substitutions, because some servers use renamed or older versions. (e.g. `{ "getGJLevels21": "dorabaeChooseLevel42" }`) | object |

  

# Folders

  

GDBrowser has a lot of folders. [citation needed]

I pride myself in keeping my files neat, without doing the whole `src/main/data/stuff/code/homework/newfolder/util/actualcode` garbage 

  

Most folders contain exactly what you'd expect, but here's some in-depth info in case you're in the dark.

  

## API

This is where all the backend stuff happens! Yipee!

  

They're all fairly similar. Fetch something, parse the response, and serve it in a crisp and non-intimidating JSON. This is probably what you came for.


  

## Assets

Assets! Assets everywhere!

  

All the GD stuff was ripped straight from the GD spritesheets via [Absolute's texture splitter hack](https://youtu.be/pYQgIyNhow8). If you want a nice categorized version, [I've done all the dirty work for you.](https://www.mediafire.com/file/4d99bw1zhwcl507/textures.zip/file)

  

I'd explain what's in all the subfolders but it's pretty obvious. I tried my best to organize everything nicely.

  

## Classes

What's a class you ask? Good question.

  

I guess the best way to put it is uh... super fancy functions???

  

Level.js parses the server's disgusting response and sends back a nice object with all the level info

  

XOR.js encrypts/decrypts stuff like GD passwords

  

## HTML

The HTML files! Nothing too fancy, since it can all be seen directly from gdbrowser. Note that profile.html and level.html (and some parts of home.html) have [[VARIABLES]] (name, id, etc) replaced by the server when they're sent.


## Misc

Inevitable misc folder

  

**Level Analysis Stuff (in a separate folder)**

  
| name | description |
|:----:|:-----------:|
| `blocks.json` | The object IDs in the different 'families' of blocks |
| `colorProperties.json` | Color channel cheatsheet |
| `initialProperties.json` | Level settings cheatsheet |
| `objectProperties.json` | Object property cheatsheet. Low budget version of [AlFas' one](https://github.com/AlFasGD/GDAPI/blob/master/GDAPI/GDAPI/Enumerations/GeometryDash/ObjectProperty.cs) |
| `objects.json` | IDs for portals, orbs, triggers, and misc stuff |

  

**Everything Else**

  
| name | description |
|:----:|:-----------:|
| `achievements.json` | List of all GD/meltdown/subzero/etc achievements. `parseAchievementPlist.js` automatically creates this file |
| `achievementTypes.json` | An object containing different categories of achievements (stars, shards, vault, etc) and how to identify them |
| `credits.json` | Credits! (shown on the homepage) | 
| `dragscroll.js` | Used on several pages for drag scrolling |
| `global.js` | Excecuted on most pages. Used for the 'page isn't wide enough' message, back button, icons, and a few other things |
| `music.json` | An array of the official GD tracks (name, artist) |
| `sampleIcons.json` | A pool of icons, one of which will randomly appear when visiting the icon kit. Syntax is [Name, ID, Col1, Col2, Glow] |
| `secretStuff.json` | GJP goes here, needed for level leaderboards. Not included in the repo for obvious reasons |

---

  

happy gdbrowsing and god bless.
