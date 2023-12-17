<script setup lang="ts">

import { ref } from 'vue';

let cells = ref([
    '', '', '',
    '', '', '',
    '', '', ''
]);

let currentMove = 'X';
let gameOver = false;

const isWinner = () => {
    const winlines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
    ];

    for (const line of winlines) {
        if (
            cells.value[line[0]] === currentMove &&
            cells.value[line[1]] === currentMove &&
            cells.value[line[2]] === currentMove
        )
            return true;
    }

    return false;
};

const move = (i: number) => {
    if (gameOver)
        return;

    if (cells.value[i] != '')
        return;
    cells.value[i] = currentMove;

    if (isWinner()) {
        gameOver = true;
        return;
    }

    currentMove = currentMove == 'X' ? 'O' : 'X';
};

const restart = () => {
    for (let i = 0; i < cells.value.length; i++)
        cells.value[i] = '';

    gameOver = false;
    currentMove = 'X';
}

</script>

<template>
    <div class="board">
        <table>
            <tr>
                <td @click="move(0)">{{ cells[0] }}</td>
                <td @click="move(1)">{{ cells[1] }}</td>
                <td @click="move(2)">{{ cells[2] }}</td>
            </tr>
            <tr>
                <td @click="move(3)">{{ cells[3] }}</td>
                <td @click="move(4)">{{ cells[4] }}</td>
                <td @click="move(5)">{{ cells[5] }}</td>
            </tr>
            <tr>
                <td @click="move(6)">{{ cells[6] }}</td>
                <td @click="move(7)">{{ cells[7] }}</td>
                <td @click="move(8)">{{ cells[8] }}</td>
            </tr>
        </table>
    </div>
    <h3 v-if="!gameOver">{{ currentMove }} your turn!</h3>
    <div id="restart" v-if="gameOver">
        <h3>{{ currentMove }} won!</h3>
        <button @click="restart" class="button-4" role="button">Restart</button>

    </div>
</template>

<style scoped>
h1 {
    font-weight: 500;
    font-size: 2.6rem;
    position: relative;
    top: -10px;
}

h3 {
    font-size: 1.2rem;
    font-weight: 500;
    position: relative;
    text-align: center;
    color: aliceblue;
}

table {
    background-color: black;
}

td {
    border: 1px solid black;
    height: 150px;
    width: 150px;
    background-color: #15BB80;
    font-size: 64px;
    color: aliceblue;
    text-align: center;
    transition: 0.1s;
}

td:hover {
    cursor: pointer;
    background-color: #25CB90;
}

#restart {
    width: 100%;
    align-items: center;
    align-self: center;
    display: flex;
    flex-direction: column;
}

.button-4 {
  appearance: none;
  background-color: #FAFBFC;
  border: 1px solid rgba(27, 31, 35, 0.15);
  border-radius: 6px;
  box-shadow: rgba(27, 31, 35, 0.04) 0 1px 0, rgba(255, 255, 255, 0.25) 0 1px 0 inset;
  box-sizing: border-box;
  color: #24292E;
  cursor: pointer;
  display: inline-block;
  font-family: -apple-system, system-ui, "Segoe UI", Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji";
  font-size: 14px;
  font-weight: 500;
  line-height: 20px;
  list-style: none;
  padding: 6px 16px;
  position: relative;
  transition: background-color 0.2s cubic-bezier(0.3, 0, 0.5, 1);
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  vertical-align: middle;
  white-space: nowrap;
  word-wrap: break-word;
}

.button-4:hover {
  background-color: #F3F4F6;
  text-decoration: none;
  transition-duration: 0.1s;
}

.button-4:active {
  background-color: #EDEFF2;
  box-shadow: rgba(225, 228, 232, 0.2) 0 1px 0 inset;
  transition: none 0s;
}

.button-4:focus {
  outline: 1px transparent;
}

.button-4:before {
  display: none;
}

.button-4:-webkit-details-marker {
  display: none;
}

.container {
    height: 200px;
    position: relative;
    border: 3px solid green;
}

.center {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 200px;
    border: 3px solid green;
}
</style>
