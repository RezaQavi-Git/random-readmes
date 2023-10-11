# Vim Cheat Sheet

## Copy & Paste & Delete

#### Copying (Yanking)

To copy text, place the cursor in the desired location and press the y key followed by the movement command. Below are some helpful yanking commands:
```yaml
yy - Yank (copy) the current line, including the newline character.
3yy - Yank (copy) three lines, starting from the line where the cursor is positioned.
y$ - Yank (copy) everything from the cursor to the end of the line.
y^ - Yank (copy) everything from the cursor to the start of the line.
yw - Yank (copy) to the start of the next word.
yiw – Yank (copy) the current word.
y% - Yank (copy) to the matching character. By default supported pairs are (), {}, and []. Useful to copy text between matching brackets.
```

#### Cutting (Deleting)

In normal mode, d is the key for cutting (deleting) text. Move the cursor to the desired position and press the d key, followed by the movement command. Here are some helpful deleting commands:
```yaml
dd - Delete (cut) the current line, including the newline character.
3dd - Delete (cut) three lines, starting from the line where the cursor is positioned,
d$ - Delete (cut) everything from the cursor to the end of the line.
```

#### Pasting (Putting)

To put the yanked or deleted text, move the cursor to the desired location and press `p` to put (paste) the text after the cursor or `P` to put (paste) before the cursor.
