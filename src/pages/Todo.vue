<template>
  <q-page class="bg-grey-3 column">
    <q-list class="bg-white" separator bordered>
      <q-item
          v-for="(task, index) in tasks"
          :key="task.title"
          @click="task.done = !task.done"
          :class="{ 'done bg-blue-1' : task.done }"
          clickable
          v-riple>
        <q-item-section avatar>
          <q-checkbox
          v-model="task.done"
          class="no-pointer-events"
          color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section
          v-if="task.done"
          side>
          <q-btn
          @click.stop="deleteTask(index)"
          flat
          round
          dense
          color="primary"
          icon="delete" />
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      alert: false,
      confirm: false,
      prompt: false,
      address: '',

      tasks: [
        {
          title: 'Get Bananas',
          done: false
        },
        {
          title: 'Eat Bananas',
          done: false
        },
        {
          title: 'Poo Bananas',
          done: false
        }
      ]
    }
  },

  methods: {
    deleteTask (index) {
      this.$q.dialog({
        title: 'Confirm',
        message: 'Really Delete?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify('Task deleted')
      })
    }
  }
}
</script>

<style lang="scss">
  .done {
    .q-item__label {
      text-decoration: line-through;
      color: #bbb;
    }
  }
</style>
