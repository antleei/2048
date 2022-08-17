<script>
import { Game } from '~/composables/game'
export default {
    data() {
        return {
            game: new Game(),
        }
    },
    computed: {
        tiles() {
            return this.game.tiles
                .filter(tile => tile.value !== 0)
        },
    },
    mounted() {
        window.addEventListener('keydown', this.handleKeyDown.bind(this))
    },
    beforeUnmount() {
        window.removeEventListener('keydown', this.handleKeyDown.bind(this))
    },
    methods: {
        handleKeyDown(event) {
            if (this.game.hasWon())
                return

            if (event.keyCode >= 37 && event.keyCode <= 40) {
                event.preventDefault()
                const direction = event.keyCode - 37
                this.game.move(direction)
            }
        },
        onRestart() {
            this.game = new Game()
        },
    },
}
</script>

<template>
    <div class="game" tabIndex="1">
        <div v-for="row_item in game.cells" :key="row_item.id">
            <Cell v-for="col_item in row_item" :key="col_item.id" />
        </div>
        <Tile v-for="tile in tiles" :key="tile.id" :tile="tile" />
        <GameEnd :game="game" :on-restart="onRestart" />
        得分{{ game.score }}
    </div>
</template>
