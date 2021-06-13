<template>
    <div class="container">
      <h2 class="text-center mt-5"> Vue Todo App  </h2>


        <!-- Input -->
        <div class="d-flex"> 
            <input v-model="task" type="text" placeholder="Enter text" class="form-control ">
            <button @click="submitTask" class="btn btn-warning text-white "> Submit </button>
            
        </div>


        <!-- Table -->
        <table class="table table-bordered mt-5">
            <thead>
                <tr>
                  <th scope="col">Task  </th>
                  <th scope="col">Satus </th>
                  <th scope="co" class="text-center">Edit</th>
                  <th scope="col" class="text-center"> Delete</th>
                </tr>
            </thead>
            <tbody>
                  <tr v-for="(task,index) in tasks " :key="index">
                    <td> 
                      <!-- <span :class="{'finished':task.status ==='finished'}">
                           {{task.name}}
                      </span> -->

                      <span :class="{'finished': task.status === 'finished'}"> {{task.name}} </span>
                    </td> 


                    
                    <td style="width:120px">  
                      <span @click="changeStatus(index)" class="pointer"
                      :class="{
                        'text-danger':  task.status === 'to-do',
                        'text-success': task.status === 'finished',
                        'text-warning': task.status === 'in-progress',
                      }"
                      >

                         {{firstCharUpper(task.status)}} 
                      </span>
                    </td>

                    <td>
                        <div class="text-center" @click="EditTask(index)">
                            <span class="fa fa-pen"> </span>
                        </div>
                    </td>
                     <td>
                        <div class="text-center" @click="deleteTask(index)">
                            <span class="fa fa-trash"> </span>
                        </div>
                    </td>
                  </tr>

            </tbody>
        </table>



    </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return{
      //property
      task: '',
      editedTask: null,
      availableStatuses: ['to-do', 'in-progress' , 'finished' ],
      tasks: [ 
        {
          name:  'Stole the banna From the store',
          status: 'todo-do'
        },

        {
          name:  'Eat 1Kg Choclate in 1 hour',
          status: 'in-progress'
        },

        {
          name:  'Pay What i have bought',
          status: 'finished'
        },

      ]
    }
  },

  methods: {
    submitTask(){
      if(this.tasks.length ===0) return;
      if(this.editedTask === null) 
      {
          this.tasks.push({
            name:this.task,
            status: 'to-do'
          });
        }else{
          this.tasks[this.editedTask].name = this.task;
          this.editedTask = null;
        }

        //Empty the input after typed the task

        this.task = '';
      },

      //Delete Task Method
      deleteTask(index){
        this.tasks.splice(index,1)
      },

      //EditTask Method

      EditTask(index){
        this.task = this.tasks[index].name;
        this.editedTask = index;
      },

      //Change Method (To-do , in-progress , finished)
    changeStatus(index){
       let newIndex =  this.availableStatuses.indexOf(this.tasks[index].status);
       if(++newIndex > 2 ) newIndex = 0;
       this.tasks[index].status = this.availableStatuses[newIndex];
    }, 

    //Upercas 
    firstCharUpper(str){
      return str.charAt(0).toUpperCase() + str.slice(1);
    }

  }
};
</script>

<style scoped>

.pointer {
  cursor: pointer;

}

.finished {
  text-decoration: line-through;
}
 </style> 
