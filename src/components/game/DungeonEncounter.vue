<template>
    <p>Dare to enter?</p>
    <p class="dual-buttons">
        <button class="btn btn-inv" :class="{ 'disabled' : !playerTurn}" @click="handleBack"><i class="material-icons left">arrow_back</i>Leave</button>
        <button class="btn btn-blue" :class="{ 'disabled' : !playerTurn}" @click="handleEnter">Enter</button>
    </p>
</template>

<script>
export default {
    name: 'DungeonEncounter',
    data() {
        return {
            task: 'dungeon',
            playerTurn: true
        }
    },
    methods: {
        log(msg) {
            console.log('Log:',msg);
        },
        handleEnter() {
            this.$parent.dungeonCount = 0;
            this.$parent.message = "You step into the dungeon."
            this.$parent.messageBox = [];
            this.$parent.changeScene('Dungeon');
        },
        handleBack() {
            this.$parent.message = "You left the dungeon behind."
            this.$parent.messageBox = [];
            this.$parent.changeScene('Wild');
        }
    },
    created: function() {
        // this.$parent.location = 'Wild';
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

</style>
