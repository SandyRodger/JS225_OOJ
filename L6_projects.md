## [6 Projects](https://launchschool.com/lessons/303f0e4f/home)

### [Introduction](https://launchschool.com/lessons/303f0e4f/assignments/f5610e4f)

- call-back to RB120

### [Tic-tac-toe](https://launchschool.com/lessons/303f0e4f/assignments/f6bb76f9)

- [RB120 link](https://launchschool.com/lessons/97babc46/assignments/7dcb53f1)

Minimum accaptable:

```javascript
const readlineSync = require('readline-sync');

class Board {
  winningLines = [[1, 2, 3], [4, 5, 6], [7, 8, 9],
                  [1, 4, 7], [2, 5, 8], [3, 6, 9], 
                  [1, 5, 9], [3, 5, 7]];

  constructor() {
    this.squares = {};
    for (let i = 1; i < 10; i++) {
      this.squares[i] = new Square(' ');
    }
  }

  getSquareAt(key) {
    return this.squares[key].marker;
  }

  setSquareAt(key, marker) {
    this.squares[key].marker = marker;
  }

  unmarkedKeys() {
    let allSquares = Object.entries(this.squares)
    let r = allSquares.filter(([_, square]) => square.isUnmarked())
    // console.log(`r.length is ${r.length}`)
    return r.map((elem) => elem[0]);
  }

  isFull() {
    return this.unmarkedKeys().length === 0
  }

  someoneWon() {
    // console.log(`this.detectWinner() is : ${this.detectWinner()}`)
    // console.log(`which, with !! in front is : ${!!this.detectWinner()}`)
    return !!this.detectWinner();
  }

  detectWinner() {
    for (let i = 0; i < this.winningLines.length; i++) {
      let line = this.winningLines[i];
      if (this.squares[line[0]].marker === TTTGame.humanMarker &&
          this.squares[line[1]].marker === TTTGame.humanMarker &&
          this.squares[line[2]].marker === TTTGame.humanMarker) {
            return TTTGame.humanMarker;
        } else if (
          this.squares[line[0]].marker === TTTGame.computerMarker &&
          this.squares[line[1]].marker === TTTGame.computerMarker &&
          this.squares[line[2]].marker === TTTGame.computerMarker) {
            return TTTGame.computerMarker;
        }
    }
  }
}

class Square {
  initialMarker = " ";
  
  constructor(marker) {
    this.marker = marker;
  }

  isUnmarked() {
    return this.marker === this.initialMarker;
  }
}

class Player {
  constructor(marker) {
    this.marker = marker;
  }
}

class TTTGame {
  static humanMarker = 'X';
  static computerMarker = 'O';

  constructor() {
    this.board = new Board;
    this.human = new Player(TTTGame.humanMarker);
    this.computer = new Player(TTTGame.computerMarker);
  }

  displayWelcomeMessage() {
    console.log("Welcome to Tic Tac Toe!\r");
  }

  displayGoodbyeMessage() {
    console.log('Thanks for playing Tic Tac Toe! Goodbye!\r');
  }

  displayBoard() {
    this.refresh();
    console.log( ``);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(1)}  |  ${this.board.getSquareAt(2)}  |  ${this.board.getSquareAt(3)}`);
    console.log( `     |     |`);
    console.log( `-----+-----+-----`);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(4)}  |  ${this.board.getSquareAt(5)}  |  ${this.board.getSquareAt(6)}`);
    console.log( `     |     |`);
    console.log( `-----+-----+-----`);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(7)}  |   ${this.board.getSquareAt(8)} |  ${this.board.getSquareAt(9)}`);
    console.log( `     |     |`);
    console.log( ``);
  }

  humanMoves() {
    console.log(`Choose a square (${this.board.unmarkedKeys().join(', ')}): `);
    let square;
    while (!square) {
      let choice = readlineSync.question('which square do you choose? (1- 9)\n');
      if (!this.board.unmarkedKeys().includes(choice))
        console.log(`invalid choice, try again`);
      else {
        square = choice;
      }
    }
    this.board.setSquareAt(square, this.human.marker)
  }

  computerMoves() {
    let unmarkedKeys = this.board.unmarkedKeys();
    let chosenSquare = unmarkedKeys[Math.floor(Math.random() * unmarkedKeys.length)];
    this.board.setSquareAt(chosenSquare, TTTGame.computerMarker);
  }

  boardFull() {
    return this.board.unmarkedKeys().length === 0;
  }

  displayResult() {
    this.displayBoard();
    let potentialWinner = this.board.detectWinner();
    if ( potentialWinner === 'O') {
      console.log(`Computer wins`)
    } else if (potentialWinner === 'X') {
      console.log(`You win`)
    } else if (this.boardFull()) {
      console.log("It's a draw!")
    }
  }

  playAgain() {
    let answer;
    while (!answer) {
      answer = readlineSync.question("Would you like to play again? (y/n)")
      if (!['y','n'].includes(answer.toLowerCase())) {
        console.log("Sorry, answer must be 'y' or 'n'")
        answer = false;
      }
    }
    return answer.toLowerCase() === 'y'
  }

  refresh() {
    console.clear();
  }

  postPlayProtocol() {
    this.displayResult();
    if (this.playAgain()) {
      this.refresh()
      this.board = new Board;
      this.play();
    } else {
      this.displayGoodbyeMessage();
    }
  }

  play() {
    this.displayWelcomeMessage();
    this.displayBoard();
    while (!this.board.someoneWon() || !this.boardFull()) {
      this.displayBoard();
      this.humanMoves()
      if (this.board.someoneWon() || this.boardFull()) {
        return this.postPlayProtocol();
      } else {
        this.computerMoves()
        if (this.board.someoneWon() || this.boardFull()) {
          return this.postPlayProtocol();
        }
      }
    }
    this.postPlayProtocol()
  }
}

let game = new TTTGame;
game.play();
```

- with computer strategy:

```javascript
/*


If neither player can win with a single play and the center square is empty, play the center square.
If none of the above conditions apply, pick a square at random.

*/

const readlineSync = require('readline-sync');

class Board {
  winningLines = [[1, 2, 3], [4, 5, 6], [7, 8, 9],
                  [1, 4, 7], [2, 5, 8], [3, 6, 9], 
                  [1, 5, 9], [3, 5, 7]];

  constructor() {
    this.squares = {};
    for (let i = 1; i < 10; i++) {
      this.squares[i] = new Square(' ');
    }
  }

  getSquareAt(key) {
    return this.squares[key].marker;
  }

  setSquareAt(key, marker) {
    this.squares[key].marker = marker;
  }

  unmarkedKeys() {
    let allSquares = Object.entries(this.squares);
    let r = allSquares.filter(([_, square]) => square.isUnmarked());
    return r.map((elem) => elem[0]);
  }

  isFull() {
    return this.unmarkedKeys().length === 0;
  }

  someoneWon() {
    return !!this.detectWinner();
  }

  detectWinner() {
    for (let i = 0; i < this.winningLines.length; i++) {
      let line = this.winningLines[i];
      if (this.squares[line[0]].marker === TTTGame.humanMarker &&
          this.squares[line[1]].marker === TTTGame.humanMarker &&
          this.squares[line[2]].marker === TTTGame.humanMarker) {
            return TTTGame.humanMarker;
        } else if (
          this.squares[line[0]].marker === TTTGame.computerMarker &&
          this.squares[line[1]].marker === TTTGame.computerMarker &&
          this.squares[line[2]].marker === TTTGame.computerMarker) {
            return TTTGame.computerMarker;
        }
    }
  }

  victoryIfThisOneSquareFilledBy(player = this.human) {
    for (let i = 0; i < this.winningLines.length; i++) {
      let line = this.winningLines[i];
      let emptySquares = line.filter((num) => this.squares[num].marker === Square.initialMarker);
      let filledSquares = line.filter((num) => this.squares[num].marker === player.marker);
      if (emptySquares.length === 1 && filledSquares.length === 2) { 
        // let playerName = player.marker === 'X' ? 'Human' : 'Computer';
        // console.log(`${playerName} will win if they fill square ${emptySquares[0]}`);
        return emptySquares[0];
      }
    }
  }
}

class Square {
  static initialMarker = " ";
  
  constructor(marker) {
    this.marker = marker;
  }

  isUnmarked() {
    return this.marker === Square.initialMarker;
  }
}

class Player {
  constructor(marker) {
    this.marker = marker;
  }
}

class TTTGame {
  static humanMarker = 'X';
  static computerMarker = 'O';

  constructor() {
    this.board = new Board;
    this.human = new Player(TTTGame.humanMarker);
    this.computer = new Player(TTTGame.computerMarker);
  }

  displayWelcomeMessage() {
    console.log("Welcome to Tic Tac Toe!\r");
  }

  displayGoodbyeMessage() {
    console.log('Thanks for playing Tic Tac Toe! Goodbye!\r');
  }

  displayBoard() {
    // this.refresh();
    console.log( ``);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(1)}  |  ${this.board.getSquareAt(2)}  |  ${this.board.getSquareAt(3)}`);
    console.log( `     |     |`);
    console.log( `-----+-----+-----`);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(4)}  |  ${this.board.getSquareAt(5)}  |  ${this.board.getSquareAt(6)}`);
    console.log( `     |     |`);
    console.log( `-----+-----+-----`);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(7)}  |   ${this.board.getSquareAt(8)} |  ${this.board.getSquareAt(9)}`);
    console.log( `     |     |`);
    console.log( ``);
  }

  humanMoves() {
    console.log(`Choose a square (${this.board.unmarkedKeys().join(', ')}): `);
    let square;
    while (!square) {
      let choice = readlineSync.question('which square do you choose? (1- 9)\n');
      // console.log(`line205: this.board.unmarkedKeys() is ${this.board.unmarkedKeys()}`)
      if (!this.board.unmarkedKeys().includes(choice))
        console.log(`invalid choice, try again`);
      else {
        square = choice;
      }
    }
    this.board.setSquareAt(square, this.human.marker)
  }

  computerMoves(targetSquare) {
    let unmarkedKeys = this.board.unmarkedKeys();
    let randomSquare = unmarkedKeys[Math.floor(Math.random() * unmarkedKeys.length)];
    let chosenSquare = targetSquare ? targetSquare : randomSquare;
    this.board.setSquareAt(chosenSquare, TTTGame.computerMarker);
  }

  boardFull() {
    return this.board.unmarkedKeys().length === 0;
  }

  displayResult() {
    this.displayBoard();
    let potentialWinner = this.board.detectWinner();
    if ( potentialWinner === 'O') {
      console.log(`Computer wins`)
    } else if (potentialWinner === 'X') {
      console.log(`You win`)
    } else if (this.boardFull()) {
      console.log("It's a draw!")
    }
  }

  playAgain() {
    let answer;
    while (!answer) {
      answer = readlineSync.question("Would you like to play again? (y/n)")
      if (!['y','n'].includes(answer.toLowerCase())) {
        console.log("Sorry, answer must be 'y' or 'n'")
        answer = false;
      }
    }
    return answer.toLowerCase() === 'y'
  }

  refresh() {
    console.clear();
  }

  postPlayProtocol() {
    this.displayResult();
    if (this.playAgain()) {
      this.refresh()
      this.board = new Board;
      this.play();
    } else {
      this.displayGoodbyeMessage();
    }
  }

  play() {
    this.displayWelcomeMessage();
    this.displayBoard();
    // console.log(`line208: ${this.board.victoryIfThisOneSquareFilled()}`);
    while (!this.board.someoneWon() || !this.boardFull()) {
      this.displayBoard();
      this.humanMoves()
      this.board.victoryIfThisOneSquareFilledBy(this.human)
      if (this.board.someoneWon() || this.boardFull()) {
        return this.postPlayProtocol();
      } else {
        let nextComputerMove = this.board.victoryIfThisOneSquareFilledBy(this.computer)
        let nextHumanMove = this.board.victoryIfThisOneSquareFilledBy(this.human)
//  If the computer can win with a single play, make that play.
        if (nextComputerMove) {
          this.computerMoves(nextComputerMove);
//  If the computer can't win with a single play, but the human can, then try to block that play.
        } else if (nextHumanMove) {
          this.computerMoves(nextHumanMove);
//  If neither player can win with a single play and the center square is empty, play the center square.
        } else if (this.board.unmarkedKeys().includes(5)) {
          this.computerMoves(5);
//  If none of the above conditions apply, pick a square at random.
        } else {
          this.computerMoves()
        }
        if (this.board.someoneWon() || this.boardFull()) {
          return this.postPlayProtocol();
        }
      }
    }
    this.postPlayProtocol()
  }
}

let game = new TTTGame;
game.play();
```

- Best of 3:

```javascript
/*


If neither player can win with a single play and the center square is empty, play the center square.
If none of the above conditions apply, pick a square at random.

*/

const readlineSync = require('readline-sync');

class Board {
  winningLines = [[1, 2, 3], [4, 5, 6], [7, 8, 9],
                  [1, 4, 7], [2, 5, 8], [3, 6, 9], 
                  [1, 5, 9], [3, 5, 7]];

  constructor() {
    this.squares = {};
    for (let i = 1; i < 10; i++) {
      this.squares[i] = new Square(' ');
    }
  }

  getSquareAt(key) {
    return this.squares[key].marker;
  }

  setSquareAt(key, marker) {
    this.squares[key].marker = marker;
  }

  unmarkedKeys() {
    let allSquares = Object.entries(this.squares);
    let r = allSquares.filter(([_, square]) => square.isUnmarked());
    return r.map((elem) => elem[0]);
  }

  isFull() {
    return this.unmarkedKeys().length === 0;
  }

  someoneWon() {
    return this.detectWinner()
  }

  detectWinner() {
    for (let i = 0; i < this.winningLines.length; i++) {
      let line = this.winningLines[i];
      if (this.squares[line[0]].marker === TTTGame.humanMarker &&
          this.squares[line[1]].marker === TTTGame.humanMarker &&
          this.squares[line[2]].marker === TTTGame.humanMarker) {
            return TTTGame.humanMarker;
        } else if (
          this.squares[line[0]].marker === TTTGame.computerMarker &&
          this.squares[line[1]].marker === TTTGame.computerMarker &&
          this.squares[line[2]].marker === TTTGame.computerMarker) {
            return TTTGame.computerMarker;
        }
    }
  }

  victoryIfThisOneSquareFilledBy(player = this.human) {
    for (let i = 0; i < this.winningLines.length; i++) {
      let line = this.winningLines[i];
      let emptySquares = line.filter((num) => this.squares[num].marker === Square.initialMarker);
      let filledSquares = line.filter((num) => this.squares[num].marker === player.marker);
      if (emptySquares.length === 1 && filledSquares.length === 2) { 
        // let playerName = player.marker === 'X' ? 'Human' : 'Computer';
        // console.log(`${playerName} will win if they fill square ${emptySquares[0]}`);
        return emptySquares[0];
      }
    }
  }
}

class Square {
  static initialMarker = " ";
  
  constructor(marker) {
    this.marker = marker;
  }

  isUnmarked() {
    return this.marker === Square.initialMarker;
  }
}

class Player {
  constructor(marker) {
    this.marker = marker;
    this.winCount = 0;
  }
}

class TTTGame {
  static humanMarker = 'X';
  static computerMarker = 'O';

  constructor() {
    this.board = new Board;
    this.human = new Player(TTTGame.humanMarker);
    this.computer = new Player(TTTGame.computerMarker);
  }

  displayWelcomeMessage() {
    console.log("Welcome to Tic Tac Toe!\r");
  }

  displayGoodbyeMessage() {
    console.log('Thanks for playing Tic Tac Toe! Goodbye!\r');
  }

  displayBoard() {
    // this.refresh();
    console.log( ``);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(1)}  |  ${this.board.getSquareAt(2)}  |  ${this.board.getSquareAt(3)}`);
    console.log( `     |     |`);
    console.log( `-----+-----+-----`);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(4)}  |  ${this.board.getSquareAt(5)}  |  ${this.board.getSquareAt(6)}`);
    console.log( `     |     |`);
    console.log( `-----+-----+-----`);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(7)}  |   ${this.board.getSquareAt(8)} |  ${this.board.getSquareAt(9)}`);
    console.log( `     |     |`);
    console.log( ``);
  }

  humanMoves() {
    console.log(`Choose a square (${this.board.unmarkedKeys().join(', ')}): `);
    let square;
    while (!square) {
      let choice = readlineSync.question('which square do you choose? (1- 9)\n');
      // console.log(`line205: this.board.unmarkedKeys() is ${this.board.unmarkedKeys()}`)
      if (!this.board.unmarkedKeys().includes(choice))
        console.log(`invalid choice, try again`);
      else {
        square = choice;
      }
    }
    this.board.setSquareAt(square, this.human.marker)
  }

  computerMoves(targetSquare) {
    let unmarkedKeys = this.board.unmarkedKeys();
    let randomSquare = unmarkedKeys[Math.floor(Math.random() * unmarkedKeys.length)];
    let chosenSquare = targetSquare ? targetSquare : randomSquare;
    this.board.setSquareAt(chosenSquare, TTTGame.computerMarker);
  }

  boardFull() {
    return this.board.unmarkedKeys().length === 0;
  }

  displayResult() {
    this.displayBoard();
    let potentialWinner = this.board.detectWinner();
    if ( potentialWinner === 'O') {
      console.log(`Computer wins`)
    } else if (potentialWinner === 'X') {
      console.log(`You win`)
    } else if (this.boardFull()) {
      console.log("It's a draw!")
    }
  }

  refresh() {
    console.clear();
  }

  thriceWinner() {
    if (this.human.winCount === 3) {
      return 'human';
    } else if (this.computer.winCount === 3) {
      return 'computer';
    }
  }

  incrementWinCount(marker) {
    if (marker === TTTGame.humanMarker) {
      this.human.winCount += 1;
    } else if (marker === TTTGame.computerMarker) {
      this.computer.winCount += 1
    }
  }

  checkForWinner() {
    if (this.human.winCount === 3) {
      return "human";
    } else if (this.computer.winCount === 3) {
      return "computer";
    }
  }

  displayScore() {
    console.log(`Human: ${this.human.winCount} | Computer: ${this.computer.winCount}`)
  }

  postPlayProtocol(marker) {
    this.incrementWinCount(marker);
    this.displayResult();
    this.displayScore();
    let thriceWinner = this.thriceWinner();
    if (!thriceWinner) {
      // this.refresh()
      this.board = new Board;
      this.play();
    } else {
      console.log(`${thriceWinner} has won thrice! Game over`);
      this.displayGoodbyeMessage();
    }
  }

  play() {
    this.displayWelcomeMessage();
    // this.displayBoard();
    while (!this.board.someoneWon() || !this.boardFull()) {
      this.displayBoard();
      this.humanMoves()
      if (this.board.someoneWon() || this.boardFull()) {
        return this.postPlayProtocol();
      } else {
        let nextComputerMove = this.board.victoryIfThisOneSquareFilledBy(this.computer)
        let nextHumanMove = this.board.victoryIfThisOneSquareFilledBy(this.human)
        if (nextComputerMove) {
          this.computerMoves(nextComputerMove);
        } else if (nextHumanMove) {
          this.computerMoves(nextHumanMove);
        } else if (this.board.unmarkedKeys().includes(5)) {
          this.computerMoves(5);
        } else {
          this.computerMoves()
        }
        if (this.board.someoneWon() || this.boardFull()) {
          return this.postPlayProtocol(this.board.someoneWon());
        }
      }
    }
    this.postPlayProtocol(this.board.someoneWon());
  }
}

let game = new TTTGame;
game.play();
```

### [Twenty-one](https://launchschool.com/lessons/303f0e4f/assignments/235718a8)

- Fiddly. I definitely lost myself in the weeds. Next time I will make a more comprehensive plan about what objects get passed where, what their responsibilities are etc. Have a piece of paper where I can draw objects and their relationships
