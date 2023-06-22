<template>

<template/>
<script>
    import feather from 'feather-icons'
    export default{
        name: ListItem,
        props: {
            item: Object,
            index:Number
        },
        computed: {
            deleteIcon(){
                return feather.icons.trash.toSvg({ 'width': 19})
            }
        },
        methods: {
            deleteitem(index){
                this.$emit('deleteFromList', index)
                this.updatedLocalStorage()
            },
            updatedLocalStorage() {
                localStorage.setItem('list', JSON.stringify(this.list))
            },
        },
        
    }
</script>
<style>

</style>