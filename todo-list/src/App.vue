<template>
<input placeholder="请输入添加的内容" type="text" v-model="newtitle" />
<button @click="add">添加</button> <br />
<p v-for="(thing,index) in things" >
  <input type="checkbox"  @click="final($event,thing.id)" />
<span :ref="thing.id" :class="idvalue==thing.id?'deleteline':''">{{ thing.title }}</span>
<button @click="edit(index)">编辑</button>
<button @click="things.splice(index,1)">删除</button>
</p>
<form v-if="editing" @submit.prevent="change" >
  <input type="text" v-model="changedtitle" />
  <button type="submit">提交</button>
  <button @click="cancel">取消</button>
</form>

</template>
<script>
export default {
  data(){
    return{
      idvalue:0,
      newtitle:'',
      changedtitle: '',
      indexvalue:'',
      editing:false,
      things:[
        {id:1,title:'第一件事'},
        {id:2,title:'第二件事'},
        {id:3,title:'第三件事'},
      ]
    }
  },methods:{
    add(){
      this.things.push({
        id:this.things.id++,
        title:this.newtitle

      })
      this.newtitle = ''
    },
    edit(index){
      this.editing = true
      this.changedtitle = this.things[index].title
      this.indexvalue = index
      console.log(this.indexvalue)

    },
    change(){
      if(this.changedtitle.trim()){
        this.things[this.indexvalue].title = this.changedtitle
        this.editing = false,
        this.changedtitle= ''

      }

    },
    final(e,idstr){
      console.log(e.target.checked)
      
      if(e.target.checked){
        this.idvalue = idstr

      }else{
        this.value = 0

      }

    },
    cancel(){
              this.editing = false,
        this.changedtitle= ''

    }

  }
}

</script>


<style>
.deleteline{
  text-decoration: line-through;
}
</style>
