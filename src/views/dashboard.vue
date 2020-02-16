<template>
<div>
    <list listName="Я наблюдатель">
    </list>
    <list listName="Я автор">
    </list>
    <list listName="Я исполнитель">
    </list>
</div>
</template>
<script>
import list from '../components/list.vue'
export default {
    name: "dashboard",
    data(){
        return{
            
        }
    },
    components:{
      list:list
    }
}
</script>