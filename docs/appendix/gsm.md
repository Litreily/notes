# GSM

> [GSM 03.38](https://en.wikipedia.org/wiki/GSM_03.38)

## Basic Character Set

|      | 0x00 | 0x10 | 0x20 | 0x30 | 0x40 | 0x50 | 0x60 | 0x70 |
|------|------|------|------|------|------|------|------|------|
| 0x00 | @    | Δ    | SP   | 0    | ¡    | P    | ¿    | p    |
| 0x01 | £    | _    | !    | 1    | A    | Q    | a    | q    |
| 0x02 | $    | Φ    | "    | 2    | B    | R    | b    | r    |
| 0x03 | ¥    | Γ    | #    | 3    | C    | S    | c    | s    |
| 0x04 | è    | Λ    | ¤    | 4    | D    | T    | d    | t    |
| 0x05 | é    | Ω    | %    | 5    | E    | U    | e    | u    |
| 0x06 | ù    | Π    | &    | 6    | F    | V    | f    | v    |
| 0x07 | ì    | Ψ    | '    | 7    | G    | W    | g    | w    |
| 0x08 | ò    | Σ    | (    | 8    | H    | X    | h    | x    |
| 0x09 | Ç    | Θ    | )    | 9    | I    | Y    | i    | y    |
| 0x0A | LF   | Ξ    | *    | :    | J    | Z    | j    | z    |
| 0x0B | Ø    | `ESC`  | +    | ;    | K    | Ä    | k    | ä    |
| 0x0C | ø    | Æ    | ,    | <    | L    | Ö    | l    | ö    |
| 0x0D | CR   | æ    | -    | =    | M    | Ñ    | m    | ñ    |
| 0x0E | Å    | ß    | .    | >    | N    | Ü    | n    | ü    |
| 0x0F | å    | É    | /    | ?    | O    | §    | o    | à    |

> Note that the [second part](#extension) of the table is only accessible if the GSM device supports the 7-bit extension mechanism, using the `ESC` character prefix. Otherwise, the `ESC` code itself is interpreted as a space, and the following character will be treated as if there was no leading `ESC` code.

## Extension

|      | 0x00 | 0x10 | 0x20 | 0x30 | 0x40 | 0x50 | 0x60 | 0x70 |
|------|------|------|------|------|------|------|------|------|
| 0x00 |      |      |      |      | |    |      |      |      |
| 0x01 |      |      |      |      |      |      |      |      |
| 0x02 |      |      |      |      |      |      |      |      |
| 0x03 |      |      |      |      |      |      |      |      |
| 0x04 |      | ^    |      |      |      |      |      |      |
| 0x05 |      |      |      |      |      |      | €    |      |
| 0x06 |      |      |      |      |      |      |      |      |
| 0x07 |      |      |      |      |      |      |      |      |
| 0x08 |      |      | {    |      |      |      |      |      |
| 0x09 |      |      | }    |      |      |      |      |      |
| 0x0A | `FF`   |      |      |      |      |      |      |      |
| 0x0B |      | `SS2`  |      |      |      |      |      |      |
| 0x0C |      |      |      | [    |      |      |      |      |
| 0x0D | `CR2`  |      |      | ~    |      |      |      |      |
| 0x0E |      |      |      | ]    |      |      |      |      |
| 0x0F |      |      | \    |      |      |      |      |      |

- `FF` is a Page Break control. If not recognized, it shall be treated like LF.
- `CR2` is a control character. No language specific character shall be encoded at this position.
- `SS2` is a second Single Shift Escape control reserved for future extensions.
