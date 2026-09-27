# 6502

Fork of Nick Morgan's [easy6502 / 6502js](https://github.com/skilldrick/6502js)
with these additions:

- A `pong.txt` prototype with two paddles and a moving ball.
- Local `pong.txt` loading through a file picker, without a local web server.
- Fresh saved source on every Assemble: Edge reuses the selected file handle;
  Firefox asks for a new file selection each time.
- Reassembly without reloading the page, plus messages for cancelled selections,
  incorrect filenames, and file-access errors.
- Named constants such as `PADDLE_OFFSET = $04`, with hexadecimal, decimal, or
  binary values from 0 to 65535. Definitions can appear before or after use.
- Constants in immediate, memory, indexed, indirect, and branch operands, plus
  `DCB` data and `* = NAME` relocation. Duplicate names and invalid values are
  rejected; zero-page addressing is selected when available.

Open `index.html`, click Assemble, and select `pong.txt`. Save edits before
assembling again. The page still needs internet access to load jQuery.

```asm
PADDLE_OFFSET = $04
PADDLE_HEIGHT = 7

lda #PADDLE_HEIGHT
sta PADDLE_OFFSET
```

Names are case-sensitive and start with a letter or underscore, followed by
letters, digits, or underscores. Constants emit no bytes and share a namespace
with address labels. Expressions and aliases are not supported. Byte operands
must fit in 0 to 255; use `#<NAME` or `#>NAME` for the low or high byte of a word.
