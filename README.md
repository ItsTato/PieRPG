# PieRPG
Concept! Extensible, simple-to-use-&amp;-learn and, lightweight game engine for making web RPGs using a Python backend.

# Revision the 2nd and a half (and another half)
> [!NOTE]
> Everything described in this document is just a concept of a possible game engine that I am interested in creating. Due to how busy I am at the moment, this is most likely to be abandoned here for a while or inmediately picked up. No way to tell.

## Plugins
PieRPG's default functionality can be easily expanded using **Plugins**.

A plugin is a folder witth a plugin.yaml and can have any of the following files:
- plugin.pre.js
- plugin.aft.js
- plugin.py
- plugin.lua
or even all of them.

A plugin.yaml file looks as follows:
```yaml
Name: Tato's wonderful plugin
Short Identifier: twp
Description: Adds 7 tremendously awesome skills & skill animations you can use.
Version:
  Major: 1
  Minor: 0
  Revision: 0
Links:
  Discord: discord.gg/awesomedevs
  Github: ItsTato/awesomeplugin
Credits:
  License: MIT
  Authors:
    - ItsTato
  Contributors:
    - ItsTato
  Play Testers:
    - ItsTato
```

### Python Files
Python files can extend the engine itself by doing things like adding more API endpoints, further adding logic to existing endpoints and more.

### JavaScript Files
JavaScript files will be injected into the running game instance. This way, you can actively modify what is happening on the client-side easily.

### Lua Files
Lua Files can extend the environment in which the game .lua files are ran. (The same can be accomplished via Python Files, but we recommend keeping things seperate and using a plugin.lua file as well as a `myPlugin = Plugins.short_identifier` in your game code. It is important to note that Python plugins can only be accessed via `myPlugin = Plugins.NonLuaPlugins.PythonExtendedEnvironment[Name]`)

## Game Engine Functionality
The game engine itself will consist of three primary parts:

### Backend
The backend is written 100% in Python. It serves to make your game lua code function, serves the web server, handles your database for you and runs all of your Lua code.

### Frontend
The frontend is written in HTML, CSS and, JavaScript. HTML and CSS code will be generated by the JavaScript part, which is how maps will be rendered. All actual code you write will be ran entirely on the backend and the effects will just be rendered by the Frontend. Since the connection between Frontend &amp; Backend is that of localhost, all information will be fetched via an API and via a Websocket. The websocket will continously check for updates or changes in information, which the Backend will accumulate as a Change Log, which is how it will know what information to tell the Frontend.

### Game Worker
Your game is written in Lua at the most basic leve but is ran in an environment managed by Python. You can use the provided Lua libraries and globals to create a game. Maps will be saved in .yaml files, game saves will be also in .yaml, and will contain a section to keep any **consistent** variables your map may have.

## More Info on the Game Worker
> [!CAUTION]
> I don't really like how it is so far. Will most likely change how this works. My main aim is making the game engine something you can build upon, but a seperate thing that just runs your files. Making a highly hackable game engine is probably what would best serve my purposes.

Your maps, saved in .yaml files are rendered to HTML & CSS, where the player can actually interact with them. Each map will also contain a index.lua file which will handle any map-related events, such as interacting with an NPC. NPC dialogues and interactions can be optionally seperated into NPC.lua files, where you can write out your NPC and then make functional in your index.lua file by doing `Registrar.AddNPC('NPC.lua');`.

```lua title="Index.lua"
-- Index.lua
-- This is where all of your code will go.


```

After this, there will also be a **Player.lua** file. This file will be how your character moves, etc. By default, you will not need to touch this as it will come with some default move options. Notably, **freemove** will allow players to move freely but **gridmove** will force the player to the typical RPG grid-movement system.

An additional **Player.js** file will exist on the client-side which will only exist to render the player to the end-user. You should not modify this directly unless you have a good reason to, as it could mess up player movement and movement rendering.

A **Pause.js** file will be your pause menu. Any modifications to its UI should be done inside it. This file will be in `UI/Pause`. This folder will further contain a **Status.js**, **Inventory.js**, **Skills.js** and, a **Save.js** to create the subsequents UIs.
