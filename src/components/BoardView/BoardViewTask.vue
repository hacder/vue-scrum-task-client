<template>
  <div class="task task-card task-item" @click="openTask">
    <!--优先级-->
    <div class="task-priority-wrapper">
      <div class="task-priority-view">
        <div class="task-priority bg-priority-2"></div>
      </div>
    </div>
    <!-- task content -->
    <div class="task-checkbox" @click="changeTaskStatus(task)">
      <i v-if="task.status===1" class="ion ion-checkmark"></i>
    </div>
    <div class="task-content-wrapper" :data-task-id="task._id">
      <div class="task-content" v-html="task.title"></div>
      <div class="avatar img-circle"
           style="background-image:url('/static/images/head.jpg')"
           data-title="Godtoy"></div>
    </div>

  </div>
</template>

<script>

  import Api from '@/utils/api'

  export default {
    name: "board-view-task",
    data() {
      return {};
    },
    props: {
      task: {}
    },
    methods: {
      async openTask() {
        this.$router.replace({
          name: 'task-normal-detail',
          params: {
            _taskId: this.task._id
          }
        })
      },
      async changeTaskStatus(task) {
        task.status = task.status === 1 ? 0 : 1;
        let res = await this.$api.instance().put(`tasks/${task._id}/status`, task);
        console.log(task);
      },
      moveTask() {

      }
    }
  }
</script>

<style lang="scss">

</style>
