# Godot Deployment Scripts

**What this does?**
One script export (windows + linux + web) and deploy (via butler) to itch.io.

## How to Use

### One Time Setup

- Have the contents of this repository inside a `bat/` folder as a sibling from `project\project.godot`.
- Create the `exports/lin`, `exports/win` and `exports/web` folders as a sibling from `project\project.godot`.

Configure your project exports for windows/linux/web normally.
Make sure to use the default names for all three:

- web: "Web"
- windows: "Windows Desktop"
- linux: "Linux"

Make sure they are set to export to (export once or use the field at the top of the export dialog):

- web: `exports\web` (i.e.: `index.html` inside this folder)
- windows: `exports\win` (i.e.: `your_game.exe` inside this folder)
- linux: `exports\lin` (i.e.: `your_game` inside this folder)

Configuration

Inside `setup.bat` configure your godot binary, butler binary and itch username and project.

Here's an example:


```bat
:: setup.bat
set GODOT_BINARY=Godot_v4.3-stable_win64_console.exe
set BUTLER_BINARY=butler.exe
set ITCH_USERNAME=zafteer
set ITCH_PROJECT=sink
```

Recommended:

- Add a `.gdignore` file to the `exports` folder so the editor ignores it.
- Add `exports/win/*`, `exports/lin/*` and `exports/web/*` to your `.gitignore`

It should look like this:

```
root
  - project
    - project.godot
  - bat
    ... bat files in this repository ...
  - exports
    - .gdignore (empty file)
    - win
      - .gitignore (with *.*)
    - lin
      - .gitignore (with *.*)
    - web
      - .gitignore (with *.*)
```

## Export and Deployment

Must be run from the root folder.

```ps
bat\export-and-itch-all.bat
```

This will export the project for web, windows, and linux and deploy it all to itch using butler.

The command above is made of a few smaller commands that can all be run independently.
There are also individual commands for each part:

- `bat\export-web.bat`: export for web
- `bat\export-win.bat`: export for linux
- `bat\export-lin.bat`: export for windows
- `bat\itch-web.bat`: deploy for web on itch using butler (requires export first)
- `bat\itch-win.bat`: deploy for linux on itch using butler (requires export first)
- `bat\itch-lin.bat`: deploy for windows on itch using butler (requires export first)

## Advanced usage

As you start your project, include the deploy scripts as a submodule:

```bat
git submodule add -f git@github.com:zaftnotameni/godot-itch-deploy-scripts.git bat
```
