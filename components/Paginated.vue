<template>
    <section>
        <ul>
            <li 
                v-for="page in pages_array"
                v-bind:key="page.id">
                    <span v-if="page=='..'">{{page}}</span>
                    <span v-else-if="page==pageNumber" class="curentPage">{{page}}</span>    
                    <span v-else
                        v-on:click="changePage(page)"
                    >{{page}}</span>                    
            </li>
        </ul>
    </section>
</template>

<script>
export default {
    props: ['countPage','pageNumber'],
    computed: {
        pages_array: function(){
            if (this.countPage != 0) {
                let pag = []                
                if (this.pageNumber<=5 && this.countPage <= 6) {
                    for (let index = 1; index <= this.countPage; index++) {
                        pag.push(index);
                    }
                } else if (this.pageNumber<=5) {
                    for (let index = 1; index < 7; index++) {
                        pag.push(index);
                    }
                    pag.push('..');
                    pag.push(this.countPage);
                } 
                else if (this.pageNumber>5 && this.pageNumber < (this.countPage-4)) {
                    pag.push(1);
                    pag.push('..');
                    for (let index = (this.pageNumber -2 ); index < (this.pageNumber + 3); index++) {
                        pag.push(index);
                    }
                    pag.push('..');
                    pag.push(this.countPage);
                } else {
                    pag.push(1);
                    pag.push('..');
                    for (let index = (this.countPage - 5); index <= this.countPage; index++) {
                        pag.push(index);
                    }
                }
                return pag;
            } else {
                return []
            }
            
        }
    },
    methods: {
        changePage: function(event){
            this.$emit('change-page',{
                pageNumber: event
            });
        }
    }
}
</script>

<style lang="scss" scoped>
    section{
        text-align: center;
        margin-top: 4em;
        cursor: pointer;
    }
    li {
        display: inline;
        margin-right: 5px;
        margin-left: 5px; 
        font-weight: 600;
    }
    .curentPage{
        font-weight: 600;
        color: #0029FF;
        cursor: default;
    }
</style>