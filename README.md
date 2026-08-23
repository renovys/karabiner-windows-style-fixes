# Windows-style shortcuts: browser and Finder fixes (Karabiner-Elements)

Three small rules that fix conflicts the popular PC-style shortcut sets leave behind on macOS.

If you came from Windows and mapped <kbd>Alt</kbd> to <kbd>⌘</kbd>, you probably lost a few keys
without noticing. These rules give them back.

---

## The problem

| Symptom | Cause |
| --- | --- |
| <kbd>⌘D</kbd> stopped working everywhere — Finder Duplicate, Add bookmark | PC-style sets map `Alt+D` (address bar) **globally**, so every <kbd>⌘D</kbd> becomes <kbd>⌘L</kbd> |
| <kbd>Alt+F4</kbd> does nothing in Finder | It maps to <kbd>⌘Q</kbd>, and Finder has no Quit |

## The rules

| Rule | Effect | Scope |
| --- | --- | --- |
| Address bar | <kbd>⌘D</kbd> → <kbd>⌘L</kbd> | browsers only |
| Bookmark | <kbd>control+D</kbd> → <kbd>⌘D</kbd> | browsers only |
| Finder close | <kbd>⌘F4</kbd> → <kbd>⌘W</kbd> | Finder only |

Scoping the address-bar rule to browsers is the whole point of rule 1: <kbd>⌘D</kbd> keeps working
everywhere else. Rule 2 then restores bookmarking with the Windows key, <kbd>Ctrl+D</kbd>.

## Install

One click (opens Karabiner-Elements):

[Import into Karabiner-Elements](karabiner://karabiner/assets/complex_modifications/import?url=https%3A%2F%2Fraw.githubusercontent.com%2Frenovys%2Fkarabiner-windows-style-fixes%2Fmain%2Fwindows_style_browser_and_finder_fixes.json)

Or manually:

```shell
curl -L -o ~/.config/karabiner/assets/complex_modifications/windows_style_browser_and_finder_fixes.json \
  https://raw.githubusercontent.com/renovys/karabiner-windows-style-fixes/main/windows_style_browser_and_finder_fixes.json
```

Then enable the rules in *Karabiner-Elements → Complex Modifications → Add rule*.

## Enable order does not matter

Rules 1 and 2 both involve <kbd>D</kbd>, but they match different input modifiers:
rule 1 matches `left_command + d`, while rule 2 matches `control + d` (either Control key).

Karabiner-Elements evaluates complex manipulators from top to bottom, and
["the input event is manipulated only the first matched manipulator"][priority]. A
<kbd>Ctrl+D</kbd> press is therefore handled by rule 2 alone; rule 1 never sees it, whatever the
enable order. The current JSON emits `right_command + d`; macOS treats either Command key as
<kbd>⌘</kbd>, and the right-side modifier is not what keeps the two rules apart.

[priority]: https://karabiner-elements.pqrs.org/docs/json/complex-modifications-manipulator-evaluation-priority/

## Browsers covered

Safari, Chrome, Edge, Brave, Firefox (stable / developer / nightly), Whale.

To add your own, find the bundle identifier and append it to the `bundle_identifiers` arrays:

```shell
osascript -e 'id of app "Vivaldi"'
```

## Also in the official gallery

Submitted to the Karabiner-Elements complex modifications gallery as
[pqrs-org/KE-complex_modifications#1989](https://github.com/pqrs-org/KE-complex_modifications/pull/1989).
This repository is the standalone copy, and it has since moved ahead of that submission: the gallery
version matches any modifier (`"optional": ["any"]`), which lets rule 1 also capture <kbd>⌘⇧D</kbd>
("Bookmark all tabs" in Chrome) and <kbd>⌃⌘D</kbd> (Look Up). This copy matches modifiers exactly and
allows only <kbd>fn</kbd> and Caps Lock, so those shortcuts keep working.

## License

Public domain ([Unlicense](LICENSE)), matching the gallery.
