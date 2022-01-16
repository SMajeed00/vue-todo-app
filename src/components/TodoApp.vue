<template>
  <div class="container">
    <div class="col-lg-6 mx-auto">
      <div class="row">
        <h2 class="text-center mt-5">My Vue Todo-App</h2> 

        <!-- input -->
        <div class="d-flex mb-5">
          <input v-model="task" type="text" class="form-control" placeholder="Enter Task">
          <button class="btn btn-warning rounded-0" @click="submitTask">Submit</button>
        </div> 

        <!-- table -->
        <table class="table table-bordered">
          <thead>
            <tr>
              <th scope="col">Task</th>
              <th scope="col">Status</th>
              <th scope="col" class="text-center">#</th>
              <th scope="col" class="text-center">#</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(task, index) in tasks" :key="index">
              <td>
                <span :class="{'finished': task.status === 'finished'}">
                  {{ task.name}}
                  </span></td>
              <td style="width: 120px;">
                <span 
                class="status" 
                :class="{'text-danger' : task.status === 'to-do',
                'text-warning' : task.status === 'in-progress',
                'text-success': task.status === 'finished'}" @click="changeStatus(index)">
                {{firstCharUpper(task.status)}}
                </span>
                </td>
              <td>
                <div class="text-center" @click="editTask(index)">
                  <span class="fa fa-pen"></span>
                </div>
              </td>
              <td>
                <div class="text-center" @click="deleteTask(index)">
                  <span class="fa fa-trash color-red"></span>
                </div>
              </td>
            </tr>
          </tbody>
        </table>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      task: '',
      editedTask: null,
      availableStatus: ['to-do', 'in-progress', 'finished'],
      tasks: [
        {
          name: 'Clean the house',
          status: 'to-do'
        },
        {
          name: 'Buy eye Drop',
          status: 'in-progress'
        },
      ]
    }
  },
  methods: {
    submitTask(){
      if (this.task.length === 0) return

      if (this.editedTask === null) {
        this.tasks.push({
        name: this.task,
        status: 'to-do',
        })
      }
      else{
        this.tasks[this.editedTask].name = this.task
        this.editedTask = null
      }
      this.task = '' 
    },
    deleteTask(index){
      this.tasks.splice(index, 1)
    },
    editTask(index){
      this.task = this.tasks[index].name
      this.editedTask = index
    },
    changeStatus(index){
      let newIndex = this.availableStatus.indexOf(this.tasks[index].status)
      if (++newIndex > 2) newIndex = 0
      this.tasks[index].status = this.availableStatus[newIndex]
    },
    firstCharUpper(str){
      return `${str.charAt(0).toUpperCase()}${str.slice(1)}`
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .status{
    cursor: pointer;
  }
  .finished{
    text-decoration: line-through;
  }
</style>
