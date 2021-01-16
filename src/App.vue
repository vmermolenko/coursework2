<template>
  <div class="container column">
    <app-add-block @actionaddblock="createComponentList"></app-add-block>
    <app-cv-block :componentList="componentList"></app-cv-block>
  </div>
  
  <div class="container">
    <app-comment></app-comment>       
  </div>
  
</template>

<script>
import AppAddBlock from './components/AppAddBlock'
import AppCvBlock from './components/AppCvBlock'
import AppComment from './components/AppComment'
import axios from 'axios'
export default {
  data(){
    return {
      loading : false,
      comments : [],
      componentList : []
      // componentList : [
      //   {
      //     type : 'app-title' , 
      //     text : 'Резюме Nickname'
      //   }, 
      //   {
      //     type : 'app-sub-title' , 
      //     text : 'Опыт работы'
      //   }, 
      //   {
      //     type : 'app-avatar' , 
      //     text : 'https://cdn.dribbble.com/users/5592443/screenshots/14279501/drbl_pop_r_m_rick_4x.png'
      //   }, 
      //   {
      //     type : 'app-text' , 
      //     text : 'Lorem ipsum dolor sit amet'
      //   }]
    }
  },
  mounted(){      
    this.loadComponentList()
  },
  methods : {
    async createComponentList(data){
      const url = 'https://vue-coursework2-366f4-default-rtdb.firebaseio.com/componentcv.json'
      
      const response = await fetch(url,{ 
        method : 'POST', 
        headers : {
          'Content-Type' : 'application/json'
        },
        body : JSON.stringify({
          type : data.type,
          text : data.text
        })
      })

      const firebaseData = await response.json()
      console.log(firebaseData)
      this.componentList.push({
        type : data.type,
        text : data.text
      })
    },
    async loadComponentList(){ 
      this.loading = true
      try {
        
        const url = 'https://vue-coursework2-366f4-default-rtdb.firebaseio.com/componentcv.json'
      
        const {data} = await axios.get(url)
        if (!data) {
          throw new Error('Список компонентов пуст') 
        }

        this.componentList = Object.keys(data).map( key => {
          return {
            id: key,
            ...data[key]
          }
        })
      } catch (e) {
        console.log(e.message)
      }
    }

  },
  components : {AppAddBlock, AppCvBlock, AppComment}
}
</script>
