<template>
  <q-page class="bg-grey-4 column">
    <div class="row q-pa-sm bg-primary">
      <q-input 
      v-model="newTasks" 
      @keyup.enter="addTask"
      bottom-slots 
      label="Add Task"
      dense 
      bg-color="white" 
      class="col q-pa-none" 
       >
        <template v-slot:append>
          <q-btn
          @click="addTask" 
          round dense flat icon="add" />
        </template>
      </q-input>
    </div>
    <q-list class="bg-white" separator bordered>
      <q-item
        v-for="(task,index) in tasks"
        :key="task.title"
        @click="task.done = !task.done"
        clickable
        v-ripple
      >
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            class="no-pointer-events"
            color="blue"
          />
        </q-item-section>
        <q-item-section :class="{'done': task.done }">
          <q-item-label>{{ task.title }} </q-item-label>
        </q-item-section>
        <q-item-section>
          <q-item-label >
            {{task.time}}
          </q-item-label>
        </q-item-section>
        <q-item-section
        side
        v-if="task.done">
           <q-btn
           @click.stop="deleteTask(index)"
           flat round color="primary" icon="delete" />
        </q-item-section>
      </q-item>
    </q-list>
    <div class="no-tasks absolute-center" v-if="!tasks.length">
      <q-icon
      name="check"
      size="100px"
      color="primary"
      />
      <div class="text-h5 text-primary text-center">No Tasks</div>
      </div>     
  </q-page>
</template>

<script>
import {date} from 'quasar'
export default {
  data() {
    return {
      newTasks: '',
      tasks: [
        // {
        //   title: "Get Bananas",
        //   done: false
        // },
        // {
        //   title: "Eat Bananas",
        //   done: false
        // },
        // {
        //   title: "Poo Bananas",
        //   done: false
        // }
      ]
    };
  },
  methods: {
    deleteTask(index){
      this.$q.dialog({
        title: 'Confirm',
        message: 'Really Delete?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index,1)
        this.$q.notify({
        message: 'Item Deleted.',
        color: 'purple'
      })
      })
  },
    addTask(){
      if (this.newTasks!=="") {
         this.tasks.push({
        title: this.newTasks,
        done:false,
        time:date.formatDate (Date.now(),'dddd D MMMM')

      })
      console.log(this.tasks)
      this.newTasks=''
      } else {
        this.$q.notify({
        message: 'Task Should Not be Null.',
        color: 'red'
      })
      }
     
    }
  },
};
</script>
<style>
.done
  {
    text-decoration: line-through;
    color: #000;
  }

</style>
