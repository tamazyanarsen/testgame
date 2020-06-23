<template>
    <div class="main-content"
         @scroll="onScrollHandle">
        <div v-for="item in items"
             :key="item.code + Math.random() * 10000">
            <TournamentCard :game-mode="item.tournamentType.gameMode"
                            :img="item.cardImage+ '?width=300&height=300'"
                            :max-users="item.maxUsers"
                            :name="item.name"
                            :participate-count="item.participateCount"
                            :payment-type="item.paymentType"
                            :prize-table="item.prizeTable"
                            :started-at="item.startedAt"
            />
        </div>
    </div>
</template>

<script>
    import * as ax from 'axios';
    import TournamentCard from "@/components/TournamentCard";
    import * as ld from 'lodash';

    export default {
        name: 'HelloWorld',
        components: { TournamentCard },
        props: {
            msg: String
        },
        data() {
            return {
                tournamentData: null,
                items: [],
                currentStep: 0
            }
        },
        created() {
            this.getData();
            this.onScrollHandle = this.onScrollHandle.bind(this);
        },
        methods: {
            getData(size = 15) {
                ax.get(`https://app.msrvbattle.ru/tournaments/games/v2/?start=${this.currentStep}&gameCode=f533d4be-5b8e-11e9-8647-d663bd873d93&max=${size}&includePaid=true`)
                    .then(e => {
                        this.currentStep = e.data.length;
                        this.tournamentData = e.data
                            .filter(e => e.tournamentData.cardImage)
                            .map(e => Object.assign(e.tournamentData, {
                                code: e.tournamentCode,
                                prizeTable: e.tournamentData.prizeTable && e.tournamentData.prizeTable.length
                                    ? e.tournamentData.prizeTable.reduce((a, b) => a + b)
                                    : 0,
                                startedAt: new Date(e.tournamentData.startedAt)
                            }));
                        this.items.push(...this.tournamentData);
                        console.log(this.items);
                    })
                    .catch(console.warn)
                    .finally(() => console.log('запрос выполнен'));
            },
            onScrollHandle: ld.debounce(function (event) {
                const vm = this;
                const target = event.target;
                if (target.clientHeight + target.scrollTop >= 0.7 * target.scrollHeight) {
                    vm.getData();
                }
            }, 200)
        }
    }
</script>

<style scoped>
    .main-content {
        overflow: auto;
        max-height: 100vh;
    }
</style>
