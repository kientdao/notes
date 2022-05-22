---
title: Writing Chess Engines
date: 21-05-2003
private: false
---

## useful stuff
[UCI (universal chess interface)](https://en.wikipedia.org/wiki/Universal_Chess_Interface) - standard form the allows chess engines to communicate with UI
[Forsyth–Edwards Notation](https://en.wikipedia.org/wiki/Forsyth–Edwards_Notation)-  A string that describes the **current** board position
- FEN for initial board state: "rnbqkbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w KQkq - 0 1"
- FEN for board state after e4: "rnbqkbnr/pppppppp/8/8/4P3/8/PPPP1PPP/RNBQKBNR b KQkq e3 0 1"
- integers = empty squares, space-seperated strings at the end don't really matter


## representing the board
### common methods
- [bitboards](https://en.wikipedia.org/wiki/Bitboard) with a more indepth shit [here](https://www.chessprogramming.org/Bitboards)- 1D array with bounds-padding
- 2d matrix array of bytes/chars for pieces

## FEN to board in GO
```go
func FEN(fen string) (b Board) {
  // End string doesn't matter for now
  parts := strings.Split(fen, " ")
  rows := strings.Split(parts[0], "/")

  for i, row := range rows {
    shift:=0
    for j, piece := range row {
      if !unicode.IsDigit(piece) {
        b[i][j+shift] = Piece(piece)
      } else {
        r := int(piece-'0')
        for n:=0;n<r;n++ {
          b[i][j+shift+n] = Piece('·')
        }
        shift+=r-1
      }
    }
  }
  return b
}
```
