<script>
export default {
    components: {},
    props: {
        game: {
            type: Object,
            required: true,
        },
        onRestart: {
            type: Function,
            required: true,
        },
    },
    data() {
        return {}
    },
    computed: {
        show() {
            return this.game.hasWon() || this.game.hasLost()
        },
        contents() {
            if (this.game.hasWon())
                return '2048 完成！'
            else if (this.game.hasLost())
                return '游戏结束'
            else
                return ''
        },
    },

    methods: {
        restart() {
            this.onRestart && this.onRestart()
        },
    },
}
</script>

<template>
    <div v-show="show" class="overlay">
        <p class="message">
            {{ contents }}
        </p>
        <button class="play-again" @click="restart">
            再玩一次
        </button>
    </div>
</template>
