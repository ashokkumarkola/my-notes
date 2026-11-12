# VS Code Cheat Sheet

Shortcuts for Linux/Windows. macOS: `Ctrl` → `Cmd`, `Alt` → `Option`.

## General

| Shortcut | Action |
|---|---|
| `Ctrl+Shift+P` | Command palette |
| `Ctrl+P` | Quick open file |
| `Ctrl+,` | Settings |
| `Ctrl+K Ctrl+S` | Keyboard shortcuts |
| `` Ctrl+` `` | Toggle terminal |
| `Ctrl+B` | Toggle sidebar |
| `Ctrl+Shift+E / F / G / X` | Explorer / Search / Git / Extensions |
| `Ctrl+\` | Split editor |
| `Ctrl+Tab` | Switch open files |

## Editing

| Shortcut | Action |
|---|---|
| `Ctrl+/` | Toggle line comment |
| `Alt+Up / Down` | Move line |
| `Shift+Alt+Up / Down` | Copy line |
| `Ctrl+Shift+K` | Delete line |
| `Ctrl+Enter` | Insert line below |
| `Ctrl+D` | Select next occurrence |
| `Ctrl+Shift+L` | Select all occurrences |
| `Alt+Click` | Add cursor |
| `Ctrl+Alt+Up / Down` | Cursor above / below (Windows) |
| `Shift+Alt+F` | Format document (Windows) |
| `Ctrl+Shift+I` | Format document (Linux) |
| `Ctrl+Space` | Trigger suggestions |
| `Ctrl+.` | Quick fix |

## Navigation

| Shortcut | Action |
|---|---|
| `F12` | Go to definition |
| `Alt+F12` | Peek definition |
| `Shift+F12` | Find references |
| `F2` | Rename symbol |
| `Ctrl+G` | Go to line |
| `Ctrl+Shift+O` | Go to symbol in file |
| `Ctrl+T` | Go to symbol in workspace |
| `Ctrl+Alt+-` | Navigate back (Linux) |
| `Ctrl+Shift+F` | Search in files |
| `Ctrl+H` | Replace |
| `Ctrl+Shift+V` | Markdown preview |

## `code` CLI

```bash
code .                                   # open folder
code file.txt                            # open file
code -r .                                # reuse window
code --diff a.txt b.txt                  # compare
code --list-extensions                   # export list
code --install-extension <publisher.id>
code --uninstall-extension <publisher.id>
```

## Settings files

| Scope | Path (Linux) |
|---|---|
| User | `~/.config/Code/User/settings.json` |
| Keybindings | `~/.config/Code/User/keybindings.json` |
| Workspace | `.vscode/settings.json` |
| Recommended extensions | `.vscode/extensions.json` |
