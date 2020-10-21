<template>
    <div class="location-card-wrapper">
        <section class="location-card" @click="toggleView" :class="view" >
           <div v-if="loaded" class="location-card-content"> 
               <div class="location-card-content-head">
                    <h2>{{ connectionToShow.name }}</h2>
                    <div class="location-card-content-head-info">
                        <img src="@/assets/icons/info.svg" alt="info-icon"/>
                        <img src="@/assets/icons/warning.svg" alt="warning-icon"/>
                        <button class="head-info-toggle-size">{{ this.view === 'collapsed' ? '&wedge;' : '&vee;' }}</button>
                    </div>
               </div>
               <div class="location-card-content-body">
                    <LiftIconInfo :leftBankInfo="leftBankInfo" :rightBankInfo="rightBankInfo"/>
                    <EscalatorIconInfo :leftBankInfo="leftBankInfo" :rightBankInfo="rightBankInfo"/>
                    <CardInfo  icon="info" title="Liften" content="Wegens voorbereidende onderhoudswerken is de LO buiten dienst. Onze excuses voor het ongemak. fietsers wordt aangeraden gebruik te maken van de Millenium Bridge."/>
                    <CardInfo  icon="warning" title="Algemeen" content="In het kader van de maatregelen tegen het CORONAvirus: HOU AUB VOLDOENDE AFSTAND"/>
                    <div v-if="view !== 'collapsed'" class="accessibility-icons">
                        <h3 class="location-card-content-subtitle">Toegankelijkheid</h3>
                        <div class="accessibility-icons-wrapper">
                            <span v-for="item in connectionToShow.accessibility" :key="item.id">
                                <img v-if="item.possible" :src="getIcon(item)" alt="accessibility-icon"/>
                            </span>
                        </div>
                    </div>
               </div>
            </div>
        </section>
    </div>
</template>

<script>
import axios from 'axios'
import LiftIconInfo from './LiftIconInfo'
import EscalatorIconInfo from './EscalatorIconInfo'
import CardInfo from './CardInfo'

export default {
    components: {
        LiftIconInfo,
        EscalatorIconInfo,
        CardInfo
    },
    props: {
        connection: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            connections: [],
            view: 'collapsed',
            loaded: false
        }
    },
    mounted() {
        axios
            .get('https://awv-fietsverbindingen.development.appwi.se/api/connections')
            .then( res => {
                this.connections = res.data;
                this.loaded = true;
            })
    },
    computed: {
        connectionToShow() {
            const filteredArray = this.connections.filter(c => c.name === this.connection)
            return filteredArray[0]
        },
        leftBankInfo() {
            const filteredBanks = this.connectionToShow.connection_ends.filter(c => c.shore.short_name === 'LO');
            return filteredBanks[0]
        },
        rightBankInfo() {
            const filteredBanks = this.connectionToShow.connection_ends.filter(c => c.shore.short_name === 'RO');
            return filteredBanks[0]
        }
    },
    methods: {
        toggleView() {
            this.view = this.view === 'collapsed' ? 'expanded' : 'collapsed';
        },
        getIcon(item) {
            return require(`../../assets/icons/${item.name}.svg`);
        }
    },
}
</script>

<style lang="scss" scoped>
  @import '@/assets/scss/_vars.scss';

  .location-card-wrapper {
    position: absolute;
    bottom: 0;
    height: auto;
    min-height: 25%;
    width: 100%;
    z-index: 550;

    .location-card {
        display: flex;
        align-items: flex-start;
        position: absolute;
        left: 5%;
        right: 5%;
        height: 474px;
        padding: 0 18px;
        background-color: $bg-color;
        border-top-left-radius: 20px;
        border-top-right-radius: 20px;
        overflow: scroll;

        .location-card-content {
            position: relative;
            width: 100%;
        
            .location-card-content-head {
                display: flex;
                justify-content: space-between;
                align-items: center;

                h2 {
                    color: $sec-color;
                }
                .location-card-content-head-info {
                    display: flex;
                    align-items: center;

                    img {
                        margin-left: 10px;
                    }
                }
                .head-info-toggle-size {
                    display: block;
                    margin-left: 12px;
                    font-size: 20px;
                    color: rgb(68, 68, 68);
                    background-color: transparent;
                }
            }

            .location-card-content-body {
                margin: 12px 0px;

                .accessibility-icons {
                    display: flex;
                    flex-direction: column;
                    margin-top: 20px;

                    h3 {
                        font-size: 14px;
                        font-weight: 400;
                        display: block;
                    }
                    .accessibility-icons-wrapper {
                        margin-top: 8px;
                        span {
                            display: inline-block;
                            margin-right: 14px;
                        }
                    }
                }
            }


            @media screen and (min-width: 768px) {
                display: flex;
                flex-direction: column;
                padding-top: 0;
            }
        }

        @media screen and (min-width: 768px) {
            position: absolute;
            top: 5vh;
            left: 60%;
            right: 40%;
            height: 64px;
            width: 375px;
            border-radius: 20px;
        }
    }

    .location-card.expanded {
        bottom: 0;
        height: 75vh;
        padding-top: 13px;
        transition: all ease 0.4s;

        @media screen and (min-width: 768px) {
            height: 480px;
            padding-top: 13px;
            transition: all ease 0.4s;
        }
    }

    .location-card.collapsed {
        bottom: -320px;
        padding-top: 13px;
        transition: all ease 0.4s;
        overflow: hidden;

        @media screen and (min-width: 768px) {
            height: 64px;
            width: 375px;
            padding-top: 13px;
            transition: all ease 0.4s;

            .location-card-content-body {
                display: none;
            }
        }
    }

    @media screen and (min-width: 768px) {
        position: relative;
        top: 5vh;
        right: -40vw;
        height: 10vh;
        width: 100%;
        z-index: 1100;
    }

  }
</style>
