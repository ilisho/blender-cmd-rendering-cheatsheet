# 📘 Blender CMD Rendering Cheatsheet

> A personal collection of Blender command-line rendering examples, crafted with love and tested in production 💻🎬

---

## 🧭 Table of Contents

- [⚙️ Basic CLI Commands Reference](#️-basic-cli-commands-reference)
- [🔄 Reset to Factory Startup (Clean Instance)](#-reset-to-factory-startup-clean-instance)
- [⚠️ Important Notes](#️-important-notes)
- [💤 Render with time out of 60 second before Sleep](#️-render-with-time-out-of-60-second-before-sleep)
- [🖼️ Render one frame](#️-render-one-frame)
- [📦 Batch Rendering](#-batch-rendering)
- [⚠️ Render particular scene](#️-render-particular-scene)
- [🎯 To render specific frame range with specific sample count (use this exmpl to adapt all other)](#-to-render-specific-frame-range-with-specific-sample-count-use-this-exmpl-to-adapt-all-other)
- [🪟 PowerShell Version](#-powershell-version)
- [🍎 macOS Version](#-macos-version)
- [⏱️ Misc CMD Commands](#️-misc-cmd-commands)
- [🧠 Tips for Using CMD](#-tips-for-using-cmd)
- [🧠 CMD 101 good to know](#-cmd-101-good-to-know)
- [📚 Helpful Links](#-helpful-links)
- [📬 FAQ](#-faq)



---

## ⚙️ Basic CLI Commands Reference

```bash
-a                          # Render full animation
-b                          # Open Blender without UI
-S, --scene <name>          # Set the active scene
&&			    			# Next task after finishing prev
-s 1                        # Start frame
-e 46                       # End frame
-f 34                       # Render a specific frame
-o "file path/####"			# Render to specific folder [#### outputs sequential frame numbers (0001, 0002, ...).  Use Frame_#### or any_custom_name_#### to add a filename prefix.]
--python-expr "..."         # Run Python in Blender (e.g., set samples)
```
### Examples:

Set Cycles samples:
```bash
--python-expr "import bpy; bpy.context.scene.cycles.samples = 1"
```

Set Eevee samples:
```bash
--python-expr "import bpy; bpy.context.scene.eevee.taa_render_samples = 128"
```
---
## 🔄 Reset to Factory Startup (Clean Instance)

```bash
--factory-startup
```

Example 🪟 WIN:
`C:\Users\USERNAME>`
```bash
F:\SteamLibrary\steamapps\common\Blender\blender.exe --factory-startup
```

Example 🍎 macOS:

```bash
/Applications/Blender.app/Contents/MacOS/Blender --factory-startup
```

> Use this to start a clean Blender without affecting your main setup (do not save preferences of it to not affect your main blender version ui).

---

## ⚠️ Important Notes

- ❌ **Do not copy `C:\Users\USERNAME>`** — it's just a prompt, not part of the command.
- Make sure **no spaces** exist in your folder/file/scene names — this can break commands.
- if spaces exist in your folder/file/scene names you can take it in quotes `""` Example: `"F:\my projects folder\dark forest\creature in woods v01.blend"`

✅ Good:
```bash
F:\SteamLibrary\steamapps\common\Blender\blender.exe -b F:\project\scene.blend -S SceneName -a && F:\SteamLibrary\steamapps\common\Blender\blender.exe -b "F:\second project\scene.blend" -S SceneName -a
```

❌ Bad:
```bash
C:\Users\USERNAME>F:\SteamLibrary\steamapps\common\Blender folder\blender.exe -b F:\project 1\scene new.blend -S my Scene Name -a
```
## > ⚠️ Be careful:

**This is my path to blender instal directory** `F:\SteamLibrary\steamapps\common\Blender\blender.exe` you will have another one so if you use vanilla blender you can right click on a blender shortcut and open file location OR if you use Steam version you can open steam library and Search file location. 

**short version of your comand will be**  `yourblenderpath\blender.exe -b yourfilepath\scene.blend -S scenename -a && timeout /t 60 && rundll32.exe powrprof.dll,SetSuspendState 0,1,0`

❗**It is here for example so you can see how exactly path should look like**❗

## > ⚠️ How to Add Blender to PATH (User Variables) on Windows and Launch It Without Typing the Full Path Every Time:

1-Open the Environment Variables window
Press `Win + S` and type: `Edit environment variables for your account`

2-Then in Advanced tab click on `Environment Variables` open it.

3-Find your user Path variable
In the `User variables for [your name]` section, locate `Path` → select it → click Edit…

4-Add Blender’s folder
Click `New` and paste the folder path where Blender is installed, for example: `C:\Program Files\Blender Foundation\Blender 4.2` or  `F:\SteamLibrary\steamapps\common\Blender`
⚠️ Use the folder path, not the full blender.exe path.

5-Save changes
Click OK → OK → OK to close all windows.

6-Restart your terminal
Open a new Command Prompt, PowerShell, or any terminal.

7-Test
Run: `blender --version`

If it prints Blender’s version, it works! Now you can launch Blender from the terminal simply by typing: `blender`

---

## 💤 Render with time out of 60 second before Sleep

`C:\Users\USERNAME>`
```bash
F:\SteamLibrary\steamapps\common\Blender\blender.exe -b F:\my_projects_folder\dark_forest\creature_in_woods_v01.blend -a && timeout /t 60 && rundll32.exe powrprof.dll,SetSuspendState 0,1,0
```


-----------------------------------------------------------------------------------------------------------------------------

## 🖼️ Render one frame

`C:\Users\USERNAME>`
```bash
F:\SteamLibrary\steamapps\common\Blender\blender.exe -b F:\my_projects_folder\dark_forest\creature_in_woods_v01.blend -f 69 && timeout /t 60 && rundll32.exe powrprof.dll,SetSuspendState 0,1,0
```
> This will render a specific frame — for example, frame 69.

---


## 📦 Batch Rendering

`C:\Users\USERNAME>`
```bash
F:\SteamLibrary\steamapps\common\Blender\blender.exe -b F:\my_projects_folder\dark_forest\creature_in_woods_v01.blend -a && F:\SteamLibrary\steamapps\common\Blender\blender.exe -b "F:\my_projects_folder\alien render\acid simulation\acid_v01.blend" -a
```

-----------------------------------------------------------------------------------------------------------------------------
## ⚠️ Render particular scene
## ⏱️ Render with time out of 60 second before sleep

`C:\Users\USERNAME>`
```bash
F:\SteamLibrary\steamapps\common\Blender\blender.exe -b F:\my_projects_folder\dark_forest\creature_in_woods_v01.blend -S scenename -a && timeout /t 60 && rundll32.exe powrprof.dll,SetSuspendState 0,1,0
```

### Example shows the render of multiple scenes and layers👇:
> F:\SteamLibrary\steamapps\common\Blender\blender.exe -b F:\my_projects_folder\dark_forest\creature_in_woods_v01.blend -S character -a && F:\SteamLibrary\steamapps\common\Blender\blender.exe -b F:\my_projects_folder\dark_forest\creature_in_woods_v01.blend -S background -a && F:\SteamLibrary\steamapps\common\Blender\blender.exe -b F:\my_projects_folder\dark_forest\creature_in_woods_v01.blend -S environment_forest_mountain -a && F:\SteamLibrary\steamapps\common\Blender\blender.exe -b F:\simulations_fx\legs_folder\legs_close_up_v01.blend -S scene_legs -a && F:\SteamLibrary\steamapps\common\Blender\blender.exe -b F:\simulations_fx\legs_folder\legs_close_up_v01.blend -S scene_ground -a && timeout /t 60 && rundll32.exe powrprof.dll,SetSuspendState 0,1,0 (And you can continue it for as long as you wish. If you don’t want your PC to go to sleep, just ignore this part: && timeout /t 60 && rundll32.exe powrprof.dll,SetSuspendState 0,1,0) 

### Why it is important 👀:
> This avoids slowdowns caused by switching scenes within a single .blend. Each scene loads once and renders faster.

>❓(You need that if you have file export to multi folders. In large scenes files will be exported in queue - Scene_1/Scene_2/Scene_3 frame by frame so it will cause blender to reload all (txt, info, etc) every time after switching the scene layer (can add extra 2-10 min for a frame) - will do render longer and you don't want that. You need to send every scene in separate batch render so blender will load all info for Scene_1 and render it out fast, then after finish it switch to Scene_2 load all data and so on -> as an example scene that took me 10 min on one after batching the scenes became 40 seconds for a frame with the same settings)

-----------------------------------------------------------------------------------------------------------------------------

## 🎯 To render specific frame range with specific sample count (use this exmpl to adapt all other)

> ❓ This example shows the render of the specific scene 'Scene_character' from frame 1 to 46 using 1 sample — this produces just an ALPHA image, so it is intended to be done fast. After completing this task, the render can continue from frame 47 to 300 using 2000 samples. This command is the most advanced and my personal favorite. It can be adapted to any of the previously mentioned setups simply by removing or adding parameters as needed. I have also adapted this same command for other systems, including Mac and PowerShell. I strongly recommend reading the entire document before using this command.

This command uses batch rendering, a specific scene for each document, a specific frame range for rendering, a specific sample count for each file, and optionally puts the PC to sleep upon completion.  

`C:\Users\USERNAME>`
```bash
F:\SteamLibrary\steamapps\common\Blender\blender.exe -b F:\my_projects_folder\dark_forest\landing_v01.blend -S Scene_character --python-expr "import bpy; bpy.context.scene.cycles.samples = 1" -s 1 -e 46 -a && F:\SteamLibrary\steamapps\common\Blender\blender.exe -b F:\my_projects_folder\dark_forest\landing_v01.blend -S Scene_character --python-expr "import bpy; bpy.context.scene.cycles.samples = 2000" -s 47 -e 300 -a && timeout /t 60 && rundll32.exe powrprof.dll,SetSuspendState 0,1,0
```
Same example but using `blender` command instead of full path.

`C:\Users\USERNAME>`
```bash
blender -b F:\my_projects_folder\dark_forest\landing_v01.blend -S Scene_character --python-expr "import bpy; bpy.context.scene.cycles.samples = 1" -s 1 -e 46 -a && blender -b F:\my_projects_folder\dark_forest\landing_v01.blend -S Scene_character --python-expr "import bpy; bpy.context.scene.cycles.samples = 2000" -s 47 -e 300 -a && timeout /t 60 && rundll32.exe powrprof.dll,SetSuspendState 0,1,0
```
This example show hot to render multiple frame ranges from the same .blend file into separate output directories without duplicating scenes.
The output path must be defined before `-a`, otherwise Blender will ignore it.

`C:\Users\USERNAME>`
```bash
blender -b F:\my_projects_folder\dark_forest\landing_v01.blend -S Scene_character --python-expr "import bpy; bpy.context.scene.cycles.samples = 1" -s 1 -e 46 -o "D:\projects\demo\renders\part_01\####" -a && blender -b F:\my_projects_folder\dark_forest\landing_v01.blend -S Scene_character --python-expr "import bpy; bpy.context.scene.cycles.samples = 1" -s 60 -e 180 -o "D:\projects\demo\renders\part_02\####" -a  && rundll32.exe powrprof.dll,SetSuspendState 0,1,0
```

---
## 🪟 PowerShell Version
>⚠️ Always wrap paths and scene names in quotes `""` for all links/path. Start command with `&`

`PS C:\Users\djmuc>`
```bash
& "F:\SteamLibrary\steamapps\common\Blender\blender.exe" -b "F:\my_projects_folder\dark_forest\landing_v01.blend" -S "Scene_character" --python-expr "import bpy; bpy.context.scene.cycles.samples = 1" -s 1 -e 46 -a && & "F:\SteamLibrary\steamapps\common\Blender\blender.exe" -b "F:\my_projects_folder\dark_forest\landing_v01.blend" -S "Scene_character" --python-expr "import bpy; bpy.context.scene.cycles.samples = 2000" -s 47 -e 300 -a && Start-Sleep -Seconds 60 && rundll32.exe powrprof.dll,SetSuspendState 0,1,0
```

---
## 🍎 macOS Version
>⚠️ Command Prompt (CMD) and Mac/Linux Terminal (bash/zsh):
Very similar in syntax for chaining commands `&&`, quoting strings, and general logic.

Use backslashes `\` in CMD, forward slashes `/` in bash/macOS.

No need for extra quotes unless paths have spaces.

```bash
"/Applications/Blender.app/Contents/MacOS/Blender" -b /Users/username/Desktop/Cthulhu_Cult.blend -S Scene_character --python-expr "import bpy; bpy.context.scene.cycles.samples = 1" -s 1 -e 45 -a && "/Applications/Blender.app/Contents/MacOS/Blender" -b /Users/username/Desktop/Cthulhu_Cult.blend -S Scene_character --python-expr "import bpy; bpy.context.scene.cycles.samples = 200" -s 45 -e 449 -a && osascript -e 'tell app "System Events" to sleep'
```

-----------------------------------------------------------------------------------------------------------------------------


## ⏱️ Misc CMD Commands

### Timeout (wait):
```bash
&& timeout /t 60
```

### Sleep (suspend PC):
```bash
&& rundll32.exe powrprof.dll,SetSuspendState 0,1,0
```

### Shutdown:
```bash
&& shutdown /s /t 0
```

> ⚠️ Can cause Windows errors if used improperly.

---

## 🧠 Tips for Using CMD

- **Copying Text:**  
  - Left click + drag to select  
  - Right click to copy  
  - CTRL + V to paste

- **Fast Navigation:**  
  - CTRL + ← / → to fast move through text  
  - CTRL + DEL / BACKSPACE to fast delete words

- **Interrupt CMD Process:**  
  - Press `CTRL + C` to kill Blender or stop rendering
  - after finish using console press `CTRL + C` to kill console then close it

---

## 🧠 CMD 101 good to know

>**In the Windows Command Prompt (CMD), you can repeat the last command you entered by using the following methods:**

Arrow Key: Simply press the Up Arrow key (↑). This will bring up the last command you executed. You can press it multiple times to cycle through previous commands. If you want to view a list of previously executed commands, you can use the `doskey/history command`, which will display all the commands you've entered in the current session. F7 Key: Pressing the `F7` key will bring up a graphical history of your commands in a window. You can navigate this history using the arrow keys and select a command to execute it again.
Using : In some command line environments (like Bash), you can use `!!` to repeat the last command. However, this does not work in CMD.

Example of repeating a command:
- `‼️If you close the CMD window, it won’t work — it will immediately wipe all history. The good practice is to write your command in a TXT file and copy-paste it later for a specific project.‼️
- `If you’ve previously run a render command in this same CMD instance, you can simply press the Up Arrow (↑) key to retrieve it and run the render again.
- These methods should help you efficiently repeat commands in CMD!` 🛠️

---
## 📚 Helpful Links

- 🔗 Blender CLI documentation:  
  [https://docs.blender.org/manual/en/latest/advanced/command_line/arguments.html](https://docs.blender.org/manual/en/latest/advanced/command_line/arguments.html)

- 📺 My video tutorial on CMD rendering:  
  [YouTube – ilisho](https://www.youtube.com/watch?v=InmY5MwfzNQ)

- 📺 Original Video tutorial on CMD rendering that i was inspired by:  
  [YouTube – Spencer Magnusson](https://www.youtube.com/watch?v=6RjCaf9noXo&list=LL&index=4&t=93s)

## Related Repositories

- [Shortcut Cheat Sheet Repo](https://github.com/ilisho/shortcuts-i-might-forget) — full collection of shortcuts i use and can forget

___

## 📬 FAQ

1. - Can I open the Blender file while it’s rendering from the command line?

- Yes, but don’t save it. If you save, the command-line render will be reset.

I usually open the file after starting the render if I want to check:
	•	whether I’ve set the correct render options,
	•	and if the file paths are correct.

If everything looks good, I just close the file without saving.
If something needs fixing, I stop the render, make the changes, save the file, close it, and start the render again.

⸻

2. - Can I work in another program or run another Blender instance while the render is running?

- Absolutely! You can open as many programs or Blender instances as you want, even run two renders from two command lines at the same time if you like.

`⚠️ Keep in mind: this can affect your PC performance, so use it wisely.
`I often prepare new scenes, do blocking, animation, and other tasks in solid mode (without heavy render previews) while the command-line render runs.

`You can even play games in parallel! (Elden Ring works perfectly, though sometimes there are small stutters during scene or frame switches.)
`If you lower graphics settings to a minimum, games run smoothly and barely affect the render speed.

⸻

3. - Does this actually speed up the workflow?

- Yes, yes, and yes again! The best part — you stay productive, and let’s be honest, it looks super cool. Command-line renders are basically hacker vibes 😎
````
___
👨‍💻 Keep experimenting, keep rendering — and never forget:  
`CTRL + C` is your emergency exit! 😄
