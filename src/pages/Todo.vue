<template>
  <q-page class="bg-grey-3 column">
    <div class="q-pa-md bg-secondary row" style="color:white">
      <q-input 
        filled 
        bottom-slots 
        v-model="tasks" 
        placeholder="Add Task" 
        dense
        bg-color="white"
        >
        <template v-slot:before>
          <q-icon name="list"></q-icon>
        </template>

        <template v-slot:append>
          <q-btn round dense flat icon="add"></q-btn>
        </template>
      </q-input>
    </div>
    <h5 class="q-mt-none">TO DO </h5>
    <q-list 
      class="bg-white"
      separator
      bordered>
      <q-item 
        tag="label" 
        v-ripple 
        v-for="(task,index) in tasks"
        :key="task.title"
        @click="task.done = !task.done"
        :class="{ 'done bg-blue-1' : task.done}"
        
        >
        <q-item-section avatar>
          <q-checkbox 
            v-model="task.done"
            color="primary"
            >
            </q-checkbox>
        </q-item-section>
        <q-item-section>
          <q-item-label>{{task.title}}</q-item-label>
        </q-item-section>
        <q-item-section
          v-if="task.done"
          side>
          <q-btn 
            @click.stop="deleteTask(index)"
            push
            color="primary"
            round 
            icon="delete" 
            dense
            ></q-btn>
        </q-item-section>
      </q-item>

    </q-list>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  data () {
    return {
      tasks: [
        {
        title: 'Banana 1 ',
        done: false
        },
        {
        title: 'Banana 2',
        done: false
        },
        {
        title: 'Banana 3',
        done: false
        }
      ]

    }
  },
  methods: {
    deleteTask(index){
        this.$q.dialog({
        title: 'Confirm',
        message: 'Delete?',
        cancel: true,
        persistent: true
      }).onOk(() => {
    this.tasks.splice(index,1)
    this.$q.notify("Task Deleted")
      })

  }  
  }


})
</script>
<style lang="scss">
.done{
  .q-item__label{
    text-decoration: line-through;
    color: #bbb;
  }
}

</style>
