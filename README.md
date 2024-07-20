
# Tic-Tac-Toe Game

![Tic-Tac-Toe](![image](https://github.com/user-attachments/assets/4c037b11-719d-402e-8a05-1183de3ce80e)
)

## Introduction

Welcome to the Tic-Tac-Toe game project! This is a simple, fun, and interactive game built using HTML, CSS, and JavaScript. It allows two players to play the classic game of Tic-Tac-Toe in their web browsers. The game detects the winner and announces the result, making it a great example of basic game development using web technologies.

## Features

- **Two Player Mode**: Play against a friend.
- **Winner Detection**: Automatically detects and announces the winner.
- **Reset Functionality**: Easily reset the game to play again.
- **Responsive Design**: Optimized for various screen sizes.

## Screenshots

![Game Screenshot](![image](https://github.com/user-attachments/assets/9f99dfa8-3a2a-4bb6-8303-eab236a5b5f1)
)
![Winner Announcement](![image](https://github.com/user-attachments/assets/f138d8cc-4f5c-4824-ab58-caf8f8ee5fa7)
)

## Technologies Used

- **HTML**: For structuring the content.
- **CSS**: For styling the game.
- **JavaScript**: For game logic and interactivity.

## Installation

To run this project locally, follow these steps:

1. **Clone the repository**:
    ```bash
    git clone https://github.com/your-username/tic-tac-toe.git
    ```
2. **Navigate to the project directory**:
    ```bash
    cd tic-tac-toe
    ```
3. **Open `index.html` in your favorite browser**.

## Usage

- Click on any box to make a move.
- The first player starts with "O".
- The game alternates turns between "O" and "X".
- The winner is announced once three boxes in a row, column, or diagonal are filled with the same mark.
- Use the **Reset Game** button to reset the game at any time.
- Use the **New Game** button to start a new game after a winner is declared.

## Code Overview

### HTML

The HTML file structures the game layout, including the game board and control buttons.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic-Tac-Toe</title>
    <link rel="stylesheet" href="style.css"/>
</head>
<body>
    <div class="msg-container hide">
        <p id="msg">Winner</p>
        <button id="new-btn">New Game</button>
    </div>
    <main>
        <h1>Tic-Tac-Toe</h1>
        <div class="container">
            <div class="game">
                <button class="box"></button>
                <button class="box"></button>
                <button class="box"></button>
                <button class="box"></button>
                <button class="box"></button>
                <button class="box"></button>
                <button class="box"></button>
                <button class="box"></button>
                <button class="box"></button>
            </div>
        </div>
        <button id="reset-btn">Reset Game</button>
    </main>
    <script src="app.js"></script>
</body>
</html>
```

### CSS

The CSS file styles the game, making it visually appealing.

```css
* {
    margin: 0;
    padding: 0;
}

body {
    background-color: #548687;
    text-align: center;
}

.container {
    height: 70vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

.game {
    height: 60vmin;
    width: 60vmin;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 1.5vmin;
}

.box {
    height: 18vmin;
    width: 18vmin;
    border-radius: 1rem;
    border: none;
    box-shadow: 0 0 1rem rgba(0,0,0,0.3);
    font-size: 8vmin;
    color: black;
    background-color: #fff;
}

#reset-btn, #new-btn {
    padding: 1rem;
    font-size: 1.25rem;
    background-color: #191913;
    color: #fff;
    border-radius: 1rem;
    border: none;
}

#msg {
    color: #fffc;
    font-size: 8vmin;
}

.msg-container {
    height: 20vmin;
}

.hide {
    display: none;
}
```

### JavaScript

The JavaScript file handles the game logic, including player turns and winner detection.

```javascript
let boxes = document.querySelectorAll(".box");
let resetbtn = document.querySelector("#reset-btn");
let newGamebtn = document.querySelector("#new-btn");
let msgContainer = document.querySelector(".msg-container");
let msg = document.querySelector("#msg");

let turnO = true;
let gameActive = true;

const winPatterns = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
];

const resetGame = () => {
    turnO = true;
    gameActive = true;
    enableBoxes();
    msgContainer.classList.add("hide");
};

boxes.forEach((box, index) => {
    box.addEventListener("click", () => {
        if (!gameActive) return;
        if (box.innerText === "") {
            box.innerText = turnO ? "O" : "X";
            turnO = !turnO;
            box.disabled = true;
            checkWinner();
        }
    });
});

const disableBoxes = () => {
    boxes.forEach(box => box.disabled = true);
};

const enableBoxes = () => {
    boxes.forEach(box => {
        box.disabled = false;
        box.innerText = "";
    });
};

const showWinner = (winner) => {
    msg.innerHTML = `Congratulations, Winner is ${winner}`;
    msgContainer.classList.remove("hide");
    disableBoxes();
    gameActive = false;
};

const checkWinner = () => {
    for (let pattern of winPatterns) {
        let pos1Val = boxes[pattern[0]].innerText;
        let pos2Val = boxes[pattern[1]].innerText;
        let pos3Val = boxes[pattern[2]].innerText;

        if (pos1Val && pos1Val === pos2Val && pos2Val === pos3Val) {
            showWinner(pos1Val);
            return;
        }
    }

    if (Array.from(boxes).every(box => box.innerText !== "")) {
        msg.innerHTML = "It's a Tie!";
        msgContainer.classList.remove("hide");
        gameActive = false;
    }
};

newGamebtn.addEventListener("click", resetGame);
resetbtn.addEventListener("click", resetGame);
```

## Contribution

Feel free to fork this project, submit issues and pull requests. Contributions are always welcome!

