<template>
    <div class="flex card">
        <div class="card-image padding1">
            <img :src="img"
                 alt="нет изображения!"
                 width="60px"
                 height="60px">
        </div>
        <div class="flex-column card-description">
            <div class="flex-column">
                <div class="card-date">{{startedAt | date}}</div>
                <div class="flex">
                    <div class="payment-type"
                         v-if="paymentType === 'free'">
                        <svg width="20"
                             height="12"
                             viewBox="0 0 20 12"
                             fill="none"
                             xmlns="http://www.w3.org/2000/svg">
                            <path fill-rule="evenodd"
                                  clip-rule="evenodd"
                                  d="M3.33333 0C1.49238 0 0 1.53502 0 3.42857V8.57143C0 10.465 1.49238 12 3.33333 12H16.6667C18.5076 12 20 10.465 20 8.57143V3.42857C20 1.53502 18.5076 0 16.6667 0H3.33333ZM2.5 8.57143V3.42857H5.47376V4.19101H3.3928V5.72308H5.03071V6.46394H3.3928V8.57143H2.5ZM6.19299 8.57143V3.42857H7.80405C8.85796 3.42857 9.59636 3.88891 9.59636 4.93906V4.96783C9.59636 5.78062 9.11975 6.17622 8.52903 6.34885L9.8783 8.57143H8.91166L7.65637 6.49271H7.08578V8.57143H6.19299ZM7.08578 5.80939H7.80405C8.41491 5.80939 8.71699 5.53606 8.71699 4.98941V4.96064C8.71699 4.36364 8.37464 4.16943 7.80405 4.16943H7.08578V5.80939ZM10.5284 3.42857V8.57143H13.6431V7.81618H11.4212V6.31289H13.1128V5.59361H11.4212V4.18382H13.529V3.42857H10.5284ZM14.3853 8.57143V3.42857H17.3859V4.18382H15.2781V5.59361H16.9697V6.31289H15.2781V7.81618H17.5V8.57143H14.3853Z"
                                  fill="#F2F2F2"/>
                        </svg>
                    </div>
                    <div class="payment-type"
                         v-else>
                        <svg width="20"
                             height="14"
                             viewBox="0 0 20 14"
                             fill="none"
                             xmlns="http://www.w3.org/2000/svg">
                            <path fill-rule="evenodd"
                                  clip-rule="evenodd"
                                  d="M1.875 0.75H18.125C19.1605 0.75 20 1.58947 20 2.625V5.125C18.9645 5.125 18.125 5.96447 18.125 7C18.125 8.03553 18.9645 8.875 20 8.875V11.375C20 12.4105 19.1605 13.25 18.125 13.25H1.875C0.839466 13.25 0 12.4105 0 11.375V8.875C1.03553 8.875 1.875 8.03553 1.875 7C1.875 5.96447 1.03553 5.125 0 5.125V2.625C0 1.58947 0.839466 0.75 1.875 0.75ZM14.375 1.375H15V2.625H14.375V1.375ZM15 3.875H14.375V5.125H15V3.875ZM14.375 6.375H15V7.625H14.375V6.375ZM15 8.875H14.375V10.125H15V8.875ZM14.375 11.375H15V12.625H14.375V11.375Z"
                                  fill="url(#paint0_linear)"/>
                            <defs>
                                <linearGradient id="paint0_linear"
                                                x1="0"
                                                y1="0.75"
                                                x2="11.236"
                                                y2="18.7275"
                                                gradientUnits="userSpaceOnUse">
                                    <stop stop-color="#00AAFF"/>
                                    <stop offset="1"
                                          stop-color="#002AFF"/>
                                </linearGradient>
                            </defs>
                        </svg>
                    </div>
                    <div class="name">
                        {{name}}
                    </div>
                </div>
                <div class="card-game-description flex">{{gameMode}} . {{participateCount}} / {{maxUsers}} . Призовой фонд {{prizeTable}} руб.
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "TournamentCard",
        props: {
            img: String,
            startedAt: Date,
            paymentType: String,
            name: String,
            gameMode: String,
            participateCount: Number,
            maxUsers: Number,
            prizeTable: Number
        },
        filters: {
            date(value) {
                const d = value.toDateString().split(' ').slice(1, 3).reverse().join(' ');
                const t = value.toTimeString().split(':').slice(0, 2).join(':');
                return `${d}, в ${t}`;
            }
        }
    }
</script>

<style scoped>
    .card {
        color: #F2F2F2;
    }

    .flex {
        display: flex;
        align-items: center;
    }

    .flex-column {
        display: flex;
        flex-direction: column;
    }

    .card-description {
        border-bottom: grey solid 1px;
        padding-top: 1%;
        width: 100%;
    }

    .padding1 {
        padding: 1%;
        box-sizing: border-box;
    }

    .card-game-description {
        color: #5C5E66;
    }

    .card-date {
        font-size: .7rem;
    }

    .payment-type{
        padding-right: .5%;
        padding-top: .2%;
        width: auto;
    }

    .name{
        width: 100%;
        padding-left: .2%;
    }

</style>
