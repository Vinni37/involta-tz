<template>
    <div class="navbar">
        <div class="top">
            <div class="left-col">
                <h1>Список новостей</h1>
                <div class="reload" v-on:click="reloadRSS">
                    <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M9.29973 0.0524773C10.3583 -0.0731896 11.3802 0.0315329 12.3247 0.316378C15.4638 1.26307 17.7722 4.233 17.8129 7.75586H19.8649C19.9789 7.75586 20.04 7.90247 19.9708 7.99882L16.8684 12.3427C16.8155 12.4139 16.7096 12.4139 16.6607 12.3427L13.5584 8.00301C13.4892 7.90247 13.5502 7.76005 13.6642 7.76005H15.7121C15.6755 5.44359 14.2871 3.46643 12.3247 2.61608C11.5838 2.29354 10.7654 2.13017 9.90636 2.17625C8.72566 2.23908 7.63861 2.69567 6.7592 3.41616C6.29099 3.80154 5.607 3.70939 5.25279 3.21091C4.91487 2.73756 5.00851 2.07572 5.45636 1.71128C6.53934 0.819046 7.85846 0.224222 9.29973 0.0524773ZM13.2408 12.594C12.3655 13.3187 11.2743 13.7753 10.0936 13.834C9.23051 13.88 8.41217 13.7125 7.67525 13.3941C5.71285 12.5438 4.32045 10.5666 4.28788 8.25015H6.33577C6.44977 8.25015 6.51084 8.10354 6.44163 8.0072L3.33925 3.66331C3.28632 3.5921 3.18047 3.5921 3.13161 3.66331L0.0292317 8.00301C-0.0399815 8.10354 0.0210892 8.24596 0.135087 8.24596H2.18705C2.2237 11.7688 4.53216 14.7429 7.67525 15.6854C8.61981 15.9703 9.64172 16.0708 10.7003 15.9493C12.1415 15.7818 13.4607 15.187 14.5436 14.2947C14.9915 13.9261 15.0851 13.2685 14.7472 12.7951C14.393 12.3008 13.709 12.2087 13.2408 12.594Z" fill="#0029FF"/>
                    </svg>
                </div>
            </div>
            <div class="rigth-col">
                <form>
                    <input type="text" v-model="findText">
                    <div v-on:click="cangeFindText">
                        <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <path fill-rule="evenodd" clip-rule="evenodd" d="M8.48485 1.81818C4.80295 1.81818 1.81818 4.80295 1.81818 8.48485C1.81818 12.1667 4.80295 15.1515 8.48485 15.1515C10.2942 15.1515 11.9352 14.4307 13.1363 13.2606C13.1548 13.2382 13.1745 13.2165 13.1955 13.1956C13.2165 13.1746 13.2382 13.1549 13.2606 13.1364C14.4307 11.9352 15.1515 10.2942 15.1515 8.48485C15.1515 4.80295 12.1667 1.81818 8.48485 1.81818ZM15.093 13.8074C16.2669 12.3518 16.9697 10.5004 16.9697 8.48485C16.9697 3.7988 13.1709 0 8.48485 0C3.7988 0 0 3.7988 0 8.48485C0 13.1709 3.7988 16.9697 8.48485 16.9697C10.5004 16.9697 12.3518 16.2669 13.8074 15.0931L18.448 19.7337C18.803 20.0888 19.3786 20.0888 19.7337 19.7337C20.0887 19.3787 20.0887 18.8031 19.7337 18.4481L15.093 13.8074Z" fill="#DCDCDC"/>
                        </svg>
                    </div>
                </form>
            </div>
        </div>
        <hr>
        <div class="bottom">
            <div class="left-col">
                <span v-bind:class="sourseClass('all')"
                    v-on:click="changeSourse('all')"
                >Все</span>
                <span v-bind:class="sourseClass('lenta')"
                    v-on:click="changeSourse('lenta')"
                >Lenta.ru</span>
                <span v-bind:class="sourseClass('mos')"
                    v-on:click="changeSourse('mos')"
                >Mos.ru</span>
            </div>
            <div class="rigth-col">
                <div v-on:click="changeTypeView(true)">
                    <svg width="18" height="18" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <rect v-bind:class="{unSelectSourse: showImages}" width="18" height="8" fill="#C4C4C4"/>
                        <rect v-bind:class="{unSelectSourse: showImages}" y="10" width="18" height="8" fill="#C4C4C4"/>
                    </svg>
                </div>
                <div v-on:click="changeTypeView(false)">
                    <svg width="18" height="18" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <rect v-bind:class="{unSelectSourse: !showImages}" width="8" height="8" fill="#C4C4C4"/>
                        <rect v-bind:class="{unSelectSourse: !showImages}" y="10" width="8" height="8" fill="#C4C4C4"/>
                        <rect v-bind:class="{unSelectSourse: !showImages}" x="10" width="8" height="8" fill="#C4C4C4"/>
                        <rect v-bind:class="{unSelectSourse: !showImages}" x="10" y="10" width="8" height="8" fill="#C4C4C4"/>
                    </svg>
                </div>
            </div>
        </div>       
    </div>
</template>

<script>
export default {
    props: ['typeSourse','showImages'],
    data: function(){
        return{
            findText: ''
        }
    },
    computed: {

    },
    methods:{
        changeTypeView: function(event){
            this.$emit('change-type-view',{
                show_images: event
            });
        },
        sourseClass: function(typeSourse){
            if (typeSourse == this.typeSourse) return 'selectSourse'
            else return 'unSelectSourse'
        },
        changeSourse: function(event){
            this.$emit('change-sourse',{
                typeSourse: event
            });
        },
        cangeFindText: function(){
            this.$emit('change-find-text',{
                 findText: this.findText
            });
        },
        reloadRSS: function(){
            this.$emit('reload-rss');
        }
    }
}
</script>

<style lang="scss" scoped>
    .top,.bottom{
        display: flex;
        justify-content: space-between;
    }
    .left-col, .rigth-col {
        display: flex;
        align-items: center;
    }
    .reload{
        padding: 0.6rem 0.5rem 0.1em 0.5em;
        margin-left: 1rem;
        box-shadow: 0px 2px 5px 0px rgba(34, 60, 80, 0.2);    
        border-radius: 50%;
    }
    .top .rigth-col form{
        display: flex;
        box-shadow: 0px 2px 5px 0px rgba(34, 60, 80, 0.2); 
    }
    .rigth-col form input {
        margin-left: 0.5rem;
        border: none;
        outline: none;
        background: transparent;
    }
    .top .rigth-col form div{
        margin: 0.5rem 1rem 0.5rem 0.5rem;
    }

    .bottom span{
        margin-right: 1rem;
    }
    .selectSourse, .unSelectSourse{
        font-weight: 600;
        cursor: pointer;
    }
    .unSelectSourse {
        color: #0029FF;
        fill: #0029FF;
    }
    .bottom .rigth-col div {
        margin-right: 10px;
    }
    @media (max-width: 700px) {
        h1 {
            font-size: 1.8rem;
        }
        .top{
            display: block;
        }
        .rigth-col form, .rigth-col form input{
            width: 100%;
        }
        .left-col {
            justify-content: space-between;
        }
    }
</style>