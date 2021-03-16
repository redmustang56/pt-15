<template>
    <div class="g">
        <div class="g__t">
            <h1>Пятнашки</h1>
        </div>
        <div class="g__bl">
            <Cell v-for="(cell, index) in cells"
                  :value="cell"
                  :indexCell="index"
                  :key="index"
                  @move="move" />
        </div>
        <button class="g__start" @click="randomizeCell(cells)">Начать</button>
    </div>
</template>

<script>
    import Cell from "./Cell"

    export default {
        name: "Wrap",
        components: {
            Cell
        },
        data() {
            return {
                cells: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 0],
                checkCells: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 0],
            };
        },
        methods: {
            randomizeCell(cellsCur) {
                for (let i in cellsCur) {
                    const rIndex = Math.floor(Math.random() * cellsCur.length);
                    [cellsCur[i], cellsCur[rIndex]] = [cellsCur[rIndex], cellsCur[i]]
                }

                for(let i = 0; i < cellsCur.length; i++) {
                    this.$set(this.cells, i, cellsCur[i])
                }
            },
            checkWin() {
                setTimeout(() => {
                    if(JSON.stringify(this.checkCells) === JSON.stringify(this.cells)) {
                        alert("Вы выиграли!")
                    }
                }, 200)
            },
            move(index) {
                let currentCell = this.cells[index]

                if (this.cells[index - 1] === 0) {
                    this.cells.splice(index, 1, 0)
                    this.cells.splice(index - 1, 1, currentCell)
                } else if (this.cells[index - 4] === 0) {
                    this.cells.splice(index, 1, 0)
                    this.cells.splice(index - 4, 1, currentCell)
                } else if (this.cells[index + 1] === 0) {
                    this.cells.splice(index, 1, 0)
                    this.cells.splice(index + 1, 1, currentCell)
                } else if (this.cells[index + 4] === 0) {
                    this.cells.splice(index, 1, 0)
                    this.cells.splice(index + 4, 1, currentCell)
                }
                this.checkWin()
            }
        }
    }
</script>

<style lang="scss" scoped>
    .g {
        &__t {
            display: flex;
            justify-content: center;
            margin: 0 auto 20px;
        }
        &__bl {
            display: grid;
            grid-template-columns: 100px 100px 100px 100px;
            grid-gap: 10px;
            justify-content: center;
        }
        &__start {
            display: flex;
            justify-content: center;
            color: #fff;
            background: #1867c0;
            font-size: 20px;
            border-radius: 5px;
            padding: 18px 20px;
            margin: 20px auto;
            outline: none;
            border: 0;
            box-shadow: none;
        }
    }
</style>