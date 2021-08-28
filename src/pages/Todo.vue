<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
        <q-input 
          v-model="newTask"
          @keyup.enter="addTask"
          class="col"
          square
          bg-color="white"  
          placeholder="Add task" 
          dense>
        
        <template v-slot:append>
          <q-btn 
            @click="addTask"
            round 
            dense 
            flat 
            icon="add" />
        </template>
      </q-input>

    </div>

    <q-list 
      class="bg-white"
      separator  
      bordered>
      <q-item  
        v-for="(tasks, index) in tasks"
        :key="tasks.title"
        @click="tasks.done = !tasks.done"
        :class="{ 'done bg-blue-1' : tasks.done }"
        clickable
        v-ripple>
        <q-item-section avatar>
          <q-checkbox
           v-model="tasks.done" 
           class="no-pointer-events"
           color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ tasks.title }}</q-item-label>
        </q-item-section>
        <q-item-section
          v-if="tasks.done"
          side>
          <q-btn 
            @click.stop="deleteTaks(index)"
            flat
            round 
            dense
            color="primary"
            icon="delete" />
        </q-item-section>
      </q-item>
    </q-list>
     <div
      v-if="!tasks.length" 
      class="no-tasks.absolute-center">
      <q-icon
        name="check"
        size="100px"
        color="primary"
      />
      <div class="text-h5 text-primary text-center">
        No Task
      </div>
     </div>
  </q-page>
</template>

<script>
import { defineComponent,ref } from 'vue';

export default {
  setup(){
    return{
      newTask: '',
      tasks: [
        {
          title: 'Get Cat',
          done: false
        },
        {
          title: 'Cat Eat',
          done: true
        },
        {
          title: 'Poo Cat',
          done: false
        }
      ]
    }
  },
  methods: {
    deleteTaks(index){
      this.$q.dialog({
        title: 'Confirm',
        message: 'Really delete?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index,1)
        this.$q.notify('Task deleted')
      })
    },
    addTask() {
      this.tasks.push({
        title: this.newTask,
        done: false
      })
      this.newTask = ''
    }
  }
  
}
</script>

<style lang="scss">
  .done {
    .q-item_label{
      text-decoration: line-through;
      color: #bbb;
    }
  }
  .no-tasks{
    opacity: 0.5;
  }


</style>