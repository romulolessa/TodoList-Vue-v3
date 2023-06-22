<template>
    <div class="todo-list">
        <h1>Todo-List</h1>
            <input class="text-field" type="text" @change="addToList" v-model="text">
            <ul>
                <li v-for="(item, index) in  list" :key="index">
                    <!---->
                    <span @click="toggleCheckbox(item)">
                        <input type="checkbox" :checked="item.done">
                        <span :class="{'done' : item.done}">{{ item.label }}</span>
                    </span>
                    <span class="pointer" @click="updateFromList(index)">update</span>
                    <span class="pointer" v-html="deleteIcon"  @click="deleteFromList(index)"></span>
                </li>
            </ul>
    </div>
</template>
<script>
import feather from 'feather-icons'

    export default{
        data() {
            return {
                list: [

                ]
            }
        },
        created() {
            this.list = JSON.parse(localStorage.getItem('list')) || []
        },
        computed: {
            deleteIcon(){
                return feather.icons.trash.toSvg({ 'width': 19})
            }
        },
        methods: {
            addToList(){
                this.list.push({label: this.text, done: false})
                this.updatedLocalStorage()
                this.text=''
            },
            toggleCheckbox(item){
                item.done = !item.done
                this.updatedLocalStorage()
            },
            deleteFromList(index){
                this.list.splice(index, 1)
                this.updatedLocalStorage()
            },
            updatedLocalStorage() {
                localStorage.setItem('list', JSON.stringify(this.list))
            },
        },
    }
</script>

<style scoped>

    .todo-list{
        max-width: 1200px;
        margin: auto;
    }
    .text-field{
        width: 100%;
        height: 35px;
        margin-bottom: 15px;
    }
    ul{
        list-style: none;
        padding: 0;
    }
    li{
        display: flex;
        justify-content: space-between;
    }
    li span.pointer{
        cursor: pointer;
    }
    .done{
        text-decoration: line-through;
    }
</style>