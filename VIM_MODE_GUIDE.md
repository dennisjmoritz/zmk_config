# Vim Normal Mode on RAISE Layer

This guide explains how to use the Vim normal mode implementation on the RAISE layer of your Sofle keyboard.

## Basic Concept

- **Normal Mode**: Hold the RAISE key
- **Insert Mode**: Release the RAISE key

When you hold RAISE, your keyboard becomes a Vim normal mode interface, allowing you to navigate and manipulate text using Vim-like commands that work with standard Linux shortcuts (Ctrl+C, Ctrl+X, Ctrl+V, etc.).

## Navigation Commands

All navigation commands work while holding RAISE:

### Character Navigation
- **h** = Move left (LEFT arrow)
- **j** = Move down (DOWN arrow)
- **k** = Move up (UP arrow)
- **l** = Move right (RIGHT arrow)

*Location: Row 2, right side (home row position)*

### Word Navigation
- **w** = Move forward one word (Ctrl+Right)
- **b** = Move backward one word (Ctrl+Left)

*Location: Row 2 left (w), Row 4 left (b), Row 4 right (w)*

### Line Navigation
- **0** = Move to line start (Home)
- **$** = Move to line end (End)

*Location: Row 3, right side*

### File Navigation
- **gg** = Go to file start (Ctrl+Home)
- **G** = Go to file end (Ctrl+End)

*Location: Row 1, left side*

### Page Navigation
- **Ctrl-u** = Scroll up one page (Page Up)
- **Ctrl-d** = Scroll down one page (Page Down)

*Location: Row 1 right (Ctrl-u), Row 3 right (Ctrl-d)*

## Delete Operations (Cut to Clipboard)

All delete operations cut the selected text to the system clipboard using Ctrl+X:

- **x** = Delete character under cursor (select right, cut)
- **X** = Delete character before cursor (select left, cut)
- **dw** = Delete word forward (select word forward, cut)
- **db** = Delete word backward (select word backward, cut)
- **de** = Delete to end of word (same as dw)
- **dd** = Delete entire line (select line, cut)
- **D** = Delete from cursor to end of line (select to EOL, cut)

*Location: Various positions on rows 1-3 for easy access*

## Change Operations (Cut + Enter Insert Mode)

Change operations cut text and prepare for insertion. After the cut, release RAISE to enter insert mode:

- **cw** = Change word forward
- **ciw** = Change inner word
- **C** = Change from cursor to end of line

*Location: Row 2 left (cw), Row 3 left (ciw), Row 4 left (C)*

## Yank Operations (Copy to Clipboard)

Yank operations copy text to the system clipboard using Ctrl+C:

- **yw** = Yank word forward
- **yy** = Yank entire line

*Location: Row 1, right side*

## Paste Operation

- **p** = Paste from clipboard (Ctrl+V)

*Location: Row 1, right side*

## Insert Mode Entry

These commands position the cursor and prepare for insert mode. Release RAISE after pressing to enter insert mode:

- **i** = Insert at cursor (just release RAISE)
- **I** = Insert at line start (moves to Home, then release RAISE)
- **a** = Insert after cursor (moves right, then release RAISE)
- **A** = Insert at line end (moves to End, then release RAISE)
- **o** = Open new line below (moves to End, presses Enter, then release RAISE)
- **O** = Open new line above (moves to line above end, presses Enter, then release RAISE)

*Location: Various positions on rows 1-3*

## Search Operations

- **/** = Start search (opens Ctrl+F find dialog)
- **n** = Find next occurrence (F3)
- **N** = Find previous occurrence (Shift+F3)

*Location: Row 4, left side*

## Complete RAISE Layer Layout

```
┌─────┬─────┬─────┬─────┬─────┬─────┐                ┌─────┬─────┬─────┬─────┬─────┬─────┐
│ gg  │  G  │  O  │  o  │ dd  │  D  │                │ yy  │ yw  │Ct-u │ ESC │  p  │ DEL │
├─────┼─────┼─────┼─────┼─────┼─────┤                ├─────┼─────┼─────┼─────┼─────┼─────┤
│ TAB │ ESC │  w  │ de  │ dw  │ cw  │                │  I  │  h  │  j  │  k  │  l  │BKSP │
├─────┼─────┼─────┼─────┼─────┼─────┤                ├─────┼─────┼─────┼─────┼─────┼─────┤
│  a  │  A  │  x  │  X  │ db  │ciw  │                │  0  │  $  │Ct-d │Ct-u │ RET │ SPC │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┐  ┌─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│SHIFT│  N  │  /  │  n  │  C  │  b  │MUTE │  │ PP  │  w  │ TAB │ F1  │ F2  │ F3  │SHIFT│
└─────┴─────┴─────┼─────┼─────┼─────┼─────┤  ├─────┼─────┼─────┼─────┼─────┴─────┴─────┘
                   │ GUI │ ALT │CTRL │LOWER│  │SPACE│RAISE│CTRL │ ALT │
                   │     │     │     │     │  │     │(HOLD│     │     │
                   └─────┴─────┴─────┴─────┘  └─────┴─────┴─────┴─────┘
```

## Implementation Details

### How It Works

This implementation uses Linux OS-wide keyboard shortcuts to achieve Vim-like behavior:

- **Text selection**: Uses Shift+Arrow keys and Ctrl+Shift+Arrow keys
- **Cut**: Uses Ctrl+X (cuts to system clipboard)
- **Copy**: Uses Ctrl+C (copies to system clipboard)
- **Paste**: Uses Ctrl+V (pastes from system clipboard)
- **Word boundaries**: Uses Ctrl+Arrow keys for word navigation
- **Search**: Uses Ctrl+F and F3 for find operations

### Design Principles

1. **No operator-pending mode**: All operations are single-key presses (no 'd' then 'w')
2. **No transparent keys**: Every key on the RAISE layer has a defined function
3. **Linux only**: Uses Linux/X11 standard shortcuts
4. **Clipboard integration**: All delete operations cut to clipboard, making "delete" work as "cut"
5. **Natural layer behavior**: Hold RAISE for normal mode, release for insert mode

### Differences from Real Vim

- No visual mode (selection is handled automatically)
- No registers (uses system clipboard only)
- No repeat (.) command
- No macros
- No marks
- Simplified word movement (uses OS word boundaries)
- No text objects beyond word (e.g., no 'di(' for delete inside parentheses)

### Limitations

- Works best in text editors and applications that support standard keyboard shortcuts
- Word boundaries depend on the application (some apps have different word navigation behavior)
- Line selection with 'dd' may behave differently in some applications
- 'O' (open line above) implementation may not work perfectly in all editors

## Tips for Use

1. **Practice the home row navigation**: h, j, k, l are positioned on the right side home row for comfort
2. **Use word navigation**: w and b are very efficient for moving through code
3. **Leverage the clipboard**: All deleted text goes to clipboard, so you can paste it elsewhere
4. **Combine with INSERT layer**: Use normal typing for insert mode, hold RAISE for commands
5. **Remember to release RAISE**: After change operations (cw, C) or insert operations (i, a, o), release RAISE to start typing

## Example Workflows

### Delete a word and replace it
1. Hold RAISE
2. Press 'cw' (change word)
3. Release RAISE
4. Type new word

### Copy a line and paste it elsewhere
1. Hold RAISE
2. Press 'yy' (yank line)
3. Navigate to new location with h/j/k/l
4. Press 'p' (paste)
5. Release RAISE

### Navigate to end of file and add new line
1. Hold RAISE
2. Press 'G' (go to end)
3. Press 'o' (open line below)
4. Release RAISE
5. Type new content

### Search and replace workflow
1. Hold RAISE
2. Press '/' (search)
3. Release RAISE, type search term, press Enter
4. Hold RAISE
5. Use 'n' to find next occurrence
6. Press 'cw' to change the word
7. Release RAISE, type replacement
8. Repeat steps 4-7 as needed

## Troubleshooting

**Q: Navigation isn't working**
A: Make sure you're holding the RAISE key while pressing navigation keys. Also verify your application supports arrow key navigation.

**Q: Delete operations don't cut to clipboard**
A: This feature requires Ctrl+X support in your application. Most Linux text editors and applications support this.

**Q: Word navigation jumps unexpectedly**
A: Different applications define word boundaries differently. Ctrl+Arrow word navigation behavior depends on the application.

**Q: 'dd' doesn't delete the whole line**
A: The 'dd' operation uses Home, Shift+End, Ctrl+X. Some applications may handle this differently. Try pressing 'dd' twice if needed.

**Q: Can't enter insert mode**
A: Remember to release the RAISE key to return to insert mode. If you're using change or insert operations (i, a, o, cw, C), release RAISE after pressing them.

## Comparison with Traditional Vim

| Feature | Traditional Vim | This Implementation |
|---------|----------------|---------------------|
| Normal mode | ESC key | Hold RAISE |
| Insert mode | i, a, o commands | Release RAISE |
| Delete | d{motion} | Single keys: x, dw, dd, etc. |
| Clipboard | Unnamed/named registers | System clipboard |
| Navigation | hjkl, w, b, etc. | Same keys via arrows/Ctrl |
| Search | /, n, N | Same keys via Ctrl+F, F3 |
| Visual mode | v, V, Ctrl+v | Not implemented (automatic selection) |

## Contributing

If you find issues or have suggestions for improvements, please open an issue on the repository. Remember that this implementation is designed for Linux and uses OS-wide keyboard shortcuts, so some behaviors may not be portable to other operating systems.

## Credits

Implementation based on ZMK firmware for Sofle keyboard. Uses standard Linux keyboard shortcuts to emulate Vim behavior.
