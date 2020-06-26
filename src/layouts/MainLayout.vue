<template>
  <div class="">
    <q-layout view="lHh Lpr lff"  style="height: 700px" class="shadow-2 rounded-borders">
      <q-header class="bg-cyan-8">
        <q-img src="~assets/pixbay.jpg" class="header-image absolute-top "/>
        <q-toolbar>
          <q-btn flat @click="drawer = !drawer" round dense icon="menu" />
        </q-toolbar>
       <div class="q-px-lg q-pt-xl q-mb-md">
         <div class="text-h3">To-Do</div>
         <div class="text-subtitles">{{todaysDate}}</div>
       </div>
       
      </q-header>

      <q-drawer
        v-model="drawer"
        show-if-above
        :width="180"
        :breakpoint="600"
      >
        <q-scroll-area style="height: calc(100% - 186px); margin-top: 186px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item clickable v-ripple to="/todo">
              <q-item-section avatar>
                <q-icon name="menu" />
              </q-item-section>

              <q-item-section>
                TO-DO
              </q-item-section>
            </q-item>

            <q-item clickable v-ripple to="/home">
              <q-item-section avatar>
                <q-icon name="home" />
              </q-item-section>
              <q-item-section>
                Home
              </q-item-section>
              </q-item>
              
              <q-item clickable v-ripple >
              <q-item-section avatar>
                <q-icon name="help" />
              </q-item-section>
              <q-item-section>
                Help
              </q-item-section>
            </q-item>
          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top" src="https://cdn.quasar.dev/img/material.png" style="height: 186px">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="56px" class="q-mb-sm">
              <img src="https://cdn.quasar.dev/img/boy-avatar.png">
            </q-avatar>
            <div class="text-weight-bold">Sharmin Akter</div>
            <div>@SharminDishari</div>
          </div>
        </q-img>
      </q-drawer>

      <q-page-container>
        <keep-alive>
          <router-view/>
        </keep-alive>
      </q-page-container>
    </q-layout>
  </div>

</template>

<script>
import { date } from 'quasar'
export default {
  name: 'MainLayout',
  components: {
    
  },  
  data() {
    return {
      drawer:false
    }
  },
  computed: {
    todaysDate(){
      let timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd D MMMM')
    }
  },
}
</script>
<style lang="scss">
  .header-image{
 height:100%;
 z-index:-1;
 opacity:0.2;
 filter:grayscale(100%);
  }
</style>