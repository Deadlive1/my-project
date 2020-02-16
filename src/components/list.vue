<template>
    <div>
        <p>
            {{listName}}
        </p>
        <button @click="add">+</button>
        <div>
            <div :key="index"  v-for="(item,index) in tasks">
                <p v-if="!item.isEditing">{{item.content}}</p>
                <button v-if="!item.isEditing" @click="edit(index)"> Edit </button>
                <button v-if="!item.isEditing" @click="delet(index)"> Delet </button>
                <button v-if="item.isEditing" @click="save(index)">Save</button>
                <button v-if="item.isEditing" @click="cancel(index)">Cancel</button>
                <input v-if="item.isEditing" type="text" v-model="item.tempEdit">
            </div>
        </div>
    </div>
</template>




<script>
export default {
    name: "list",
    props:["listName"],
    data(){
        return{
            tasks:JSON.parse(localStorage.getItem(this.listName) || "[]"),
        }
    },
   methods:{
       cancel(index){
           this.tasks[index].isEditing=false

       },
       save(index){
           this.tasks[index].content=this.tasks[index].tempEdit
           this.tasks[index].isEditing=false
           this.saveList()

       },
       delet(index){
           this.tasks.splice(index,1)
           this.saveList()
           
       },
       edit(index){
            this.tasks[index].tempEdit=this.tasks[index].content
            this.tasks[index].isEditing=true

       },
       add(){

           this.tasks.push({content:"",isEditing:true,tempEdit:""})

       },
       saveList(){
           localStorage.setItem(this.listName,JSON.stringify(this.tasks))
       }
       
   }
}
</script>