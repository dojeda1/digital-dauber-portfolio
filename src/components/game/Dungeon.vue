<template>
    <p>
        Minion Kills: {{$parent.dungeonCount}}/{{this.$parent.regions[this.$parent.region].dungeonGoal}}
    </p>
    <template v-if="task == 'dungeon'">
        <p>Where to next?</p>
        <p class="full-buttons">
            <button v-if="$parent.dungeonCount >= this.$parent.regions[this.$parent.region].dungeonGoal"
            class="btn btn-blue" :class="{ 'disabled' : !playerTurn}" @click="handleFightBoss">Fight Boss</button>
            <button v-else
            class="btn btn-blue" :class="{ 'disabled' : !playerTurn}" @click="handleExplore">Venture Deeper</button>
            <button class="btn btn-blue" :class="{ 'disabled' : !playerTurn}" @click="handleUseItem">Use Item</button>
        </p>
        <p class="dual-buttons">
            <button class="btn btn-inv" :class="{ 'disabled' : !playerTurn}" @click="handleExit"><i className="material-icons left">arrow_back</i>Exit</button>
        </p>
    </template>
    <template v-else-if="task == 'use item'">
        <p>{{$parent.infoText}}</p>
        <p class="items full-buttons" @mouseleave="$parent.infoText = 'Select an Item'">
            <button class="btn btn-blue"
            v-for="(item, index) in $parent.player.inventory"
            :key="index"
                :class="{ 'disabled' : !playerTurn}"
                @mouseover="$parent.infoText = item.info"
                @click="handleAttemptItem(item,index)">{{ item.name }}
                <template v-if="item.charge > 0"> ({{item.goal - item.charge}}/{{item.goal}})</template>
                <template v-if="item.qty > 1"> &times; {{item.qty}}</template>
                </button>
        </p>
        <p class="dual-buttons">
            <button class="btn btn-inv" :class="{ 'disabled' : !playerTurn}" @click="handleBack"><i class="material-icons left">arrow_back</i>Back</button>
        </p>
    </template>
</template>

<script>
export default {
    name: 'Dungeon',
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
        handleExplore() {
            this.$parent.player.animation = 'walk';
            this.playerTurn = false;
            const exploreCheck = this.$parent.randNum(1, 10)
            const $this = this;
            setTimeout(function() {
                $this.$parent.player.animation = 'idle';
                $this.playerTurn = true;
                if (exploreCheck <= 2) {
                    $this.$parent.chestEncounter();
                } else if (exploreCheck <= 5 && $this.$parent.player.level > 1) {
                    $this.$parent.viciousEncounter();
                } else if (exploreCheck == 6) {
                    $this.$parent.merchantEncounter();
                } else {
                    $this.$parent.monsterEncounter();
                }
            },600)
        },
        handleBack() {
            this.task = 'dungeon';
        },
        handleExit() {
            this.$parent.message = 'You exited the dungeon...';
            this.$parent.changeScene('Wild');
        },
        handleUseItem() {
            if (this.$parent.player.inventory.length) {
                this.$parent.infoText = 'Select an item'
            } else {
                this.$parent.infoText = 'Inventory empty'
            }
            this.task = 'use item';
        },
        handleAttemptItem(item,index) {
            let $this = this;
            let player = this.$parent.player;
            this.$parent.handleAttemptItem(item,index,
                function() {
                    $this.playerTurn = false;
                    setTimeout(function() {
                        $this.playerTurn = true;
                        player.animation = 'idle'
                    }, 600)
                }
            );
        },
        handleFightBoss() {
            const regionIndex = this.$parent.region;
            console.log('RI:',regionIndex)
            console.log('Bosses:',this.$parent.bosses)
            // let bossArray = this.$parent.bosses[regionIndex];

            if (this.$parent.regions[regionIndex].bossKills < this.$parent.bosses[regionIndex].length) {
                this.bossEncounter();
            } else {
                this.$parent.viciousEncounter();
                // this.darkEncounter();
            }
        },
        bossEncounter(alternateMessage) {

            let rangeNum = 0;
            let playerLevel = this.$parent.player.level;

            const regionIndex = this.$parent.region;
            console.log("RI:" + regionIndex)
            const regionLevel = this.$parent.regions[this.$parent.region].level;
            const regionTarget = this.$parent.regions[this.$parent.region].targetLevel;

            let bossArray = this.$parent.bosses[regionIndex]
            if (playerLevel <= regionLevel) {
                rangeNum = 1;

            } else if (playerLevel > regionLevel && playerLevel < regionTarget) {
                rangeNum = Math.ceil(bossArray.length * (playerLevel / regionTarget));
            } else {
                rangeNum = bossArray.length;
            }
            // let monNum = this.$parent.randNum(0, rangeNum);
            console.log(rangeNum)
            let monNum = this.$parent.regions[regionIndex].bossKills;
            this.$parent.currentEnemy = JSON.parse(JSON.stringify(bossArray[monNum]));
            const enemy = this.$parent.currentEnemy;
            const message = alternateMessage || "You encountered " + enemy.name + ", " + enemy.title + ".";
            this.$parent.message = message;
            console.log("message: " + message);
            enemy.hp = enemy.hpMax;
            enemy.mp = enemy.mpMax;
            enemy.animation = 'idle';
            enemy.isDead = false

            this.$parent.addEnemyAbilities(enemy);
            this.$parent.addEnemyItems(enemy);

            // console.log(this.state.currentEnemy);
            this.$parent.changeScene('Battle')
            this.$parent.enterEvent();

            console.log('Enemy:',this.$parent.currentEnemy);
        }
    },
    
    created: function() {
        this.$parent.location = 'Dungeon';
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

</style>
