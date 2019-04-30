# Visual Studio Code

## `Ctrl + ,` Settings 
* General
    * Widen working area width by removing the code minimap 
    **IMAGE HERE**

## Basics
*  `Ctrl +` ` [Integrated Terminal](https://code.visualstudio.com/docs/editor/integrated-terminal)
**IMAGE HERE**

*  `Ctrl + B` Toggle Sidebar
**IMAGE HERE**

*  `Ctrl + K Z` Zen Mode
Enter distraction free Zen mode. Press `Esc` twice to exit.
**IMAGE HERE**

*  `Ctrl + Shift + P` Command Palette
    Access all available commands based on your current context.
**IMAGE HERE**

*  `Ctrl + P` Quick Open 
    Quickly open files.
    **IMAGE HERE**

*  `Ctrl + Shift + M` Errors and Warnings status bar
    Quickly jump to errors and warnings in the project.
    **IMAGE HERE**

## Edting Hacks
* Multi cursor selection
    To add cursors at arbitrary positions, select a position with your mouse and use Alt+Click (Option+click on macOS).
    To set cursors above or below the current position use:
    Keyboard Shortcut: `Shift + Alt + Up` or `Shift + Alt + Down`

    **IMAGE HERE**
    
    You can add additional cursors to all occurrences of the current selection with `Ctrl + Shift + L`.

    **IMAGE HERE**

    > Note: You can also change the modifier to `Ctrl/Cmd` for applying multiple cursors with the `editor.multiCursorModifier` setting . See Multi-cursor Modifier for details.

    If you do not want to add all occurrences of the current selection, you can use `Ctrl+D` instead. This only selects the next occurrence after the one you selected so you can add selections one by one.
    **IMAGE HERE**
* Copy line up / down
    Keyboard Shortcut: `Ctrl+Shift+Alt+Up` or `Ctrl+Shift+Alt+Down`
    >The commands **Copy Line Up/Down** are unbound on Linux because the VS Code default keybindings would conflict with Ubuntu keybindings, see Issue #509. You can still set the commands `editor.action.copyLinesUpAction` and `editor.action.copyLinesDownAction` to your own preferred keyboard shortcuts.
* Move line up and down
Keyboard Shortcut: `Alt+Up` or `Alt+Down`

## Keyboard Shortcuts Reference`
They have a printable version of these keyboard shortcuts. Help > Keyboard Shortcut Reference displays a condensed PDF version suitable for printing as an easy reference.

Below are links to the three platform-specific versions:
* **[Windows](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)**
* **[macOS](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)**
* **[Linux](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf)**