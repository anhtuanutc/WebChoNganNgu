<template>
  <TrangChu @ShowChiTiet="showdialog"/>
  <Chitiet v-if="isShow" @CloseChiTiet="showdialog"
  :ID="itemSelected"
  />
</template>

<script>
import Chitiet from './components/Chitiet.vue'
import TrangChu from './components/TrangChu.vue'

export default {
  name: 'App',
  components: {
    Chitiet,TrangChu
  },
  data(){
    return{
      isShow:false,
      itemSelected:""
    }
  },
  methods:{
    showdialog(isShow,id){
      try {
        this.isShow=isShow
        this.itemSelected=id
        console.log(this.itemSelected);
      } catch (error) {
        console.log(error);
      }
    }
  }
}
</script>
<style>
@import url(./assets/style.css);
</style>
