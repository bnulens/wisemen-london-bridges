<template>
    <div class="location-card-wrapper">
        <section class="location-card" @click="toggleView" :class="view" >
           <div v-if="loaded" class="location-card-content"> 
               <div class="location-card-content-head">
                   <h2>{{ connectionToShow.name }}</h2>
                   <div class="location-card-content-head-info">
                        <img src="@/assets/icons/warning.svg"/>
                        <img src="@/assets/icons/info.svg"/>
                        <button>X</button>
                   </div>
               </div>
               <div class="accessibility-icons">
                   <h3>Toegankelijkheid</h3>
                   <div class="accessibility-icons-wrapper">
                       <span v-for="item in connectionToShow.accessibility" :key="item.id">
                           <img :src="getIcon(item)" alt="accessibility-icon"/>
                        </span>
                   </div>
                </div>
                <!-- <span>{{ connectionToShow.connection_ends[0]["services"][0]["state"].name }}</span> -->
            </div>
        </section>
    </div>
</template>

<script>
import axios from 'axios'
export default {
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
            console.log(filteredArray[0])
            return filteredArray[0]
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
    position: relative;
    height: 100vh;
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
            padding-top: 10px;
            width: 100%;
        
            .location-card-content-head {
                display: flex;
                justify-content: space-between;
                align-items: center;
                width: 100%;

                h2 {
                    color: $sec-color;
                }
                span {
                    display: inline-block;
                }

                @media screen and (min-width: 768px) {
                    height: 20vh;
                }
            }

            .accessibility-icons {
                display: flex;
                flex-direction: column;
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

            @media screen and (min-width: 768px) {
                position: absolute;
                display: flex;
                flex-direction: column;
                padding-top: 0;
                overflow: hidden;
            }
        }

        @media screen and (min-width: 768px) {
            position: absolute;
            align-items: center;
            top: 5%;
            left: 65%;
            height: 10%;
            width: auto;
            border-radius: 20px;
        }
    }

    .location-card.expanded {
        bottom: 0;
    }
    .location-card.collapsed {
        bottom: -320px;
    }

  }
</style>
