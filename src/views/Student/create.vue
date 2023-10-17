<template lang="">
    <div class="container mt-3">
        <div class="card">
            <div class="card-header">
                <h4>Add Students</h4>
            </div>
            <ul class="alert alert-warning" v-if="Object.keys(errorlist).length > 0">
                <li class="mb-0 ms-3" v-for="(error, key) in errorlist" :key="key">
                    {{ error[0] }}
                </li>
            </ul>
            <div class="card-body">
                <div class="mb-3">
                    <label for="">Name</label>
                    <input type="text"  class="form-control" v-model="model.student.name">
                </div>
                <div class="mb-3">
                    <label for="">course</label>
                    <input type="text"  class="form-control" v-model="model.student.course">
                </div>
                <div class="mb-3">
                    <label for="">email</label>
                    <input type="email"  class="form-control" v-model="model.student.email">
                </div>
                <div class="mb-3">
                    <label for="">Phone number</label>
                    <input type="number"  class="form-control" v-model="model.student.phone">
                </div>
                <div class="mb-3">
                    <button type="button" @click="saveStudent()" class="btn btn-primary">Save</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios';
export default {
    name: 'createStudent',
    data(){
        return{ 
            errorlist: '',
             model:{
                student:{
                    name:"",
                    course:"",
                    email:"",
                    phone:""
                }
             }
        }
    },
    mounted() {
        
    },
    methods:{
        saveStudent(){
            var mythis = this;
            console.log(this.model.student); 
            axios.post('https://niteen.standardtouch.com/restApi/public/api/students',this.model.student).then(res =>{
                    //  console.log(res.data.errors);
                    //  console.log(res.data.status);
                     this.model.student = {
                        name:"",
                        course:"",
                        email:"",
                        phone:""
                     };
                     alert('Student saved successfully!');
                   
           })
           .catch(error => {
                    console.error('Error saving student:', res.data.errors);
                    if (error.response) {
                        if (error.response.status == 422)
                        {
                            console.log(error.response.data.errors);
                            mythis.errorlist = error.response.data.errors;
                            } else if (error.request) {
                                // The request was made but no response was received
                                // `error.request` is an instance of XMLHttpRequest in the browser and an instance of
                                // http.ClientRequest in node.js
                                console.log(error.request);
                                } else {
                                // Something happened in setting up the request that triggered an Error
                                console.log('Error', error.message);
                                }
                    }
                });
        }
    }
}
</script>
<style lang="">
    
</style>