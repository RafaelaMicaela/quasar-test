<template>
  <q-layout view="lHh Lpr lFf">
    <q-header >
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="drawer = !drawer"
        />

      </q-toolbar>
      <div class="q-px-lg q-pt-xl q-mb-md">
        <div class="text-h3">Todo</div>
        <div class="text-subtitle1">{{ todaysDate }}</div>
      </div>
      <q-img 
        src="../statics/cat.jpg"
        class="header-image absolute-top"/>
    </q-header>

   <q-drawer
        v-model="drawer"
        show-if-above
        :width="250"
        :breakpoint="600"
      >
        <q-scroll-area style="height: calc(100% - 192px); margin-top: 192px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item 
              to="/"
              exact
              clickable 
              v-ripple>
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>

              <q-item-section>
                Todo
              </q-item-section>
            </q-item>

            <q-item
              to="/edit"
              exact
              clickable 
              v-ripple>
              <q-item-section avatar>
                <q-icon name="account_box" />
              </q-item-section>

              <q-item-section>
                Profile
              </q-item-section>
            </q-item>

          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top" src="../statics/cat.jpg" style="height: 192px">
          <div class="absolute-bottom bg-transparent">
            <q-avatar
             v-if="user.name"
             size="56px" 
             class="q-mb-sm">
              <img :src="`https://ui-avatars.com/api/?rounded=true&name=${user.name}`">
            </q-avatar>
            <div class="text-weight-bold">{{user.name}}</div>
            <div>{{user.username}}</div>
          </div>
        </q-img>
      </q-drawer>

    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'
import { date } from 'quasar'
import { useStore } from 'vuex'


export default {


  setup () {
    const $store = useStore()
    return {
      drawer: ref(false)
    }

  },
  
  computed:{
    todaysDate(){
      const timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd D MMMM')
    },
    user(){
  
      return (this.$store.getters["geral/getUser"])
      
      
    }
  }
  
  
}
</script>

<style lang="scss">
  .header-image{
    height: 100%;
    z-index: -1;
    opacity: 0.6;
    filter: grayscale(50%)
  }
</style>
