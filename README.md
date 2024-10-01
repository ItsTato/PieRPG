# PieRPG
Concept! Extensible, simple-to-use-&amp;-learn and, lightweight game engine for making web RPGs using a Python backend.

> [!NOTE]
> Everything described in this document is just a concept of a possible game engine that I am interested in creating. Due to how busy I am at the moment, this is most likely to be abandoned here for a while or inmediately picked up. No way to tell.

## Plugins
PieRPS's default functionality can be easily expanded using **Plugins**.

A plugin is a folder witth a plugin.yaml and can have any of the following files:
- plugin.js
- plugin.py
- plugin.lua

### Python Files
Python files can extend the engine itself by doing things like adding more API endpoints, further adding logic to existin endpoints and more.

### JavaScript Files
JavaScript files will be injected into the running game instance. This way, you can actively modify what is happening on the client-side easily.

### Lua Files
Lua Files can extend the environment in which the game .lua files are ran. (The same can be accomplished via Python Files, but we recommend keeping things seperate and using a plugin.lua file as well as a `require('plugin_name')` in your game code)

## Game Engine Functionality
The game engine itself will consist of three primary parts:

### Backend
The backend is written 100% in Python. It serves to make your game lua code function, serves the web server and handles your database for you.

### Frontend
The frontend is written in HTML, CSS and, JavaScript. HTML and CSS code will be generated bythe JavaScript part, which is how maps will be rendered.

### Game Worker
Your game is written in Lua at the most basic level. You can use the provided Lua libraries and globals to create a game. Maps will be saved in .yaml files, game saves will be also in .yaml, and will contain a section to keep any **consistent** variables your map may have.

## More Info on the Game Worker
> [!CAUTION]
> I don't really like how it is so far. Will most likely change how this works. My main aim is making the game engine something you can build upon, but a seperate thing that just runs your files. Making a highly hackable game engine is probably what would best serve my purposes.

Your maps, saved in .yaml files are rendered to HTML & CSS, where the player can actually interact with them. Each map will also contain a index.lua file which will handle any map-related events, such as interacting with an NPC. NPC dialogues and interactions can be optionally seperated into NPC.lua files, where you can write out your NPC and then make functional in your index.lua file by doing `Registrar.AddNPC('NPC.lua');`.

After this, there will also be a **Player.lua** file. This file will be how your character moves, etc. By default, you will not need to touch this as it will come with some default move options. Notably, **freemove** will allow players to move freely but **gridmove** will force the player to the typical RPG grid-movement system.

An additional **Player.js** file will exist on the client-side which will only exist to render the player to the end-user. You should not modify this directly unless you have a good reason to, as it could mess up player movement and movement rendering.

A **Pause.js** file will be your pause menu. Any modifications to its UI should be done inside it. This file will be in `UI/Pause`. This folder will further contain a **Status.js**, **Inventory.js**, **Skills.js** and, a **Save.js** to create the subsequents UIs.
