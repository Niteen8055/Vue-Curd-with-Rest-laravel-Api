<template lang="">
    <div class="container">
        <div class="card mt-5 mb-2 ">
            <div class="card-header">
                <h4>Students
                    <router-link to="/student/create" class="btn btn-primary float-end">
                        Add Student
                    </router-link>
                </h4>
            </div>
            <div class="card-body ">
                <table class="table table-bordered">
                   <thead>
                      <tr>
                        <th>Id</th>
                        <th>Name</th>
                        <th>Course</th>
                        <th>Email</th>
                        <th>Phone</th>
                        <th>Created At</th>
                        <th>Action</th>
                      </tr>
                   </thead>
                   <tbody v-if="this.studentsData.length > 0">
                      <tr v-for="(data,index) in this.studentsData" :key="index">
                            <td>{{data.id}}</td>
                            <td>{{data.name}}</td>
                            <td>{{data.course}}</td>
                            <td>{{data.email}}</td>
                            <td>{{data.phone}}</td>
                            <td>{{data.created_at}}</td>
                            <td>
                                <router-link :to="{ path: '/student/'+data.id+'/edit'}" class="btn btn-success">
                                    Edit
                                </router-link>
                                <button type="button" @click="studentDelete(data.id)" class="btn btn-danger float-end">
                                    Delete
                                </button>
                            </td>
                      </tr>
                   </tbody>
                   <tbody  v-else>
                     <tr>
                        <td colspan="7">Data Loading</td>
                     </tr>
                   </tbody>
                </table>
            </div>
        </div>    
    </div>
    
</template>
<script>
import axios from 'axios';
export default {
    name: 'students',
  
    data(){
        
         return{
            AllData : "its our data",
            studentsData:[

            ]
         }
    },
    mounted()
    {

        this.getStudents();
    },
    methods:{
       getStudents(){
           axios.get('https://niteen.standardtouch.com/restApi/public/api/students').then(res =>{
                     console.log(res.data.data);
                     this.studentsData = res.data.data;
           });
       } ,
       studentDelete(id)
       {
            if(confirm('Are You sure?,You want to delete this Data'))
            {
                axios.delete(`https://niteen.standardtouch.com/restApi/public/api/students/${id}/delete`).then(res =>{
                        // console.log(res.data);
                        // alert(res.data.status);
                        this.getStudents();
                 });
            }
       } 
    }

}
</script>
<style lang="">
    
</style>