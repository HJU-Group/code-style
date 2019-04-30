# Visual Studio Code

## Settings 
* General
    
    Widen working area width by removing the code minimap 
        
    ![remove minimap](https://github.com/cca-bheath/code-style/blob/add_vscode/img/VSC-code-remove-minimap.png)

## Basics
*  [Integrated Terminal](https://code.visualstudio.com/docs/editor/integrated-terminal) 
    
    Keyboard Shortcut: Ctrl +`

    ![Integrated Terminal](https://github.com/cca-bheath/code-style/blob/add_vscode/img/VSC-integrated_terminal.png)

*  Toggle Sidebar
    
    Keyboard Shortcut: `Ctrl + B` 

    ![Toggle Sidebar](https://github.com/cca-bheath/code-style/blob/add_vscode/img/VSC-toggle_side_bar.gif)

*  Zen Mode

    Enter distraction free Zen mode. Press `Esc` twice to exit.
    
    Keyboard Shortcut: `Ctrl + K Z`

    ![Zen Mode](https://github.com/cca-bheath/code-style/blob/add_vscode/img/VSC-zen_mode.gif)

*  Command Palette
    
    Access all available commands based on your current context.

    Keyboard Shortcut: `Ctrl + Shift + P` 
        
    ![Command Palette](https://github.com/cca-bheath/code-style/blob/add_vscode/img/VSC-OpenCommandPalatte.gif)

*  Quick Open 

    Quickly open files.
    
    Keyboard Shortcut: `Ctrl + P` 
    
    ![Quick Open ](https://github.com/cca-bheath/code-style/blob/add_vscode/img/VSC-QuickOpen.gif)

*  Errors and Warnings status bar

    Quickly jump to errors and warnings in the project.
    
    Keyboard Shortcut: `Ctrl + Shift + M` 
    
    ![Errors and Warnings](https://github.com/cca-bheath/code-style/blob/add_vscode/img/VSC-Errors_Warnings.gif)

## Edting Hacks
* Multi cursor selection
    
    To add cursors at arbitrary positions, select a position with your mouse and use Alt+Click (Option+click on macOS).
    
    To set cursors above or below the current position use:
    
    Keyboard Shortcut: `Shift + Alt + Up` or `Shift + Alt + Down`

    ![multicursor](https://github.com/cca-bheath/code-style/blob/add_vscode/img/VSC-multicursor.gif)
    
    You can add additional cursors to all occurrences of the current selection with `Ctrl + Shift + L`.

    ![multicursor current](https://github.com/cca-bheath/code-style/blob/add_vscode/img/VSC-add_cursor_current_selection.gif)

    > Note: You can also change the modifier to `Ctrl/Cmd` for applying multiple cursors with the `editor.multiCursorModifier` setting . See Multi-cursor Modifier for details.

    If you do not want to add all occurrences of the current selection, you can use `Ctrl + D` instead. This only selects the next occurrence after the one you selected so you can add selections one by one.
    
    ![multicursor individual](https://github.com/cca-bheath/code-style/blob/add_vscode/img/VSC-add_cursor_current_selection_one_by_one.gif)

* Copy line up / down

    Keyboard Shortcut: `Ctrl + Shift + Alt + Up` or `Ctrl + Shift + Alt+ Down`
    
    >The commands **Copy Line Up/Down** are unbound on Linux because the VS Code default keybindings would conflict with Ubuntu keybindings, see Issue #509. You can still set the commands `editor.action.copyLinesUpAction` and `editor.action.copyLinesDownAction` to your own preferred keyboard shortcuts.

* Move line up and down

    Keyboard Shortcut: `Alt + Up` or `Alt + Down`

## Keyboard Shortcuts Reference
They have a printable version of these keyboard shortcuts. Help > Keyboard Shortcut Reference displays a condensed PDF version suitable for printing as an easy reference.

Below are links to the three platform-specific versions:
* **[Windows](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)**
* **[macOS](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)**
* **[Linux](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf)**

## Plugins
* Recommended
    * [Laravel Blade Snippets](https://marketplace.visualstudio.com/items?itemName=onecentlin.laravel-blade)
    * [Laravel Extra Intellisense](https://marketplace.visualstudio.com/items?itemName=amiralizadeh9480.laravel-extra-intellisense)
    * [PHP Intelephense](https://marketplace.visualstudio.com/items?itemName=bmewburn.vscode-intelephense-client)
    * [Prettier - Code Formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
    * [Vetur](https://marketplace.visualstudio.com/items?itemName=octref.vetur)
* Optional
    * [Auto Close Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-close-tag)
    * [Git History](https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory)
    * [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)

## Jack Sparrow's Guide
https://laracasts.com/series/visual-studio-code-for-php-developers
