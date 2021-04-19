<template>
<div>
   <!--<h1 style="text-align:center;">New Customer Form </h1> -->

       <div class="row justify-content-center">
        <div class="col-md-6">
            <h2 class="text-center">New Subcontractor Form</h2>
            <form @submit.prevent="handleSubmitForm">
               <div class = "row">

                 <div class = "form-group col-sm-3 my-1">
                     <label>Company</label>
                     <input type="text"  class = "form-control" v-model= "sub.companyName" required>
                  </div>

                  <div class = "form-group col-sm-3 my-1">
                     <label>Phone</label>
                     <input type="tel"  class = "form-control" v-model= "sub.phone" required>
                  </div>

                  <div class = "form-group col-sm-3 my-1">
                     <label>Email</label>
                     <input type="email"  class = "form-control" v-model= "sub.email" required>
                  </div>
               </div>

                <div class = "row">
                  <div class = "form-group col-sm-2 my-1">
                     <label>Street #</label>
                     <input type="number"  class = "form-control" v-model= "sub.streetNum" required>
                  </div>

                  <div class="form-group col-sm-2 my-1">
                    <label>Unit</label>
                    <input type="text" class="form-control" v-model= "sub.unit">
                  </div>

                  <div class="form-group col-sm-2 my-1">
                    <label>Prefix</label>
                    <input type="text" class="form-control" v-model= "sub.pre_fix">
                  </div>

                  <div class="form-group col-sm-3 my-1">
                    <label>Street Name</label>
                    <input type="text" class="form-control" v-model= "sub.streetName" required>
                  </div>

                  <div class="form-group col-sm-2 my-1">
                    <label>Suffix</label>
                    <input type="text" class="form-control" v-model= "sub.suffix">
                  </div>
                </div>
              
              

                <div class = "row">
                  <div class = "form-group col-sm-3 my-1">
                     <label>City</label>
                     <input type="text"  class = "form-control" v-model= "sub.city" required>
                  </div>

                  <div class="form-group col-sm-2 my-1">
                    <label >State</label>
                    <select class="form-control" v-model= "sub.stateID" required>
                    <option v-for = "state in states" v-bind:key = "state.id" v-bind:value = "state.stateID"> {{state.stateName}}</option>

                    </select>
                  </div>

                  <div class="form-group col-sm-2 my-1">
                    <label>Zip Code</label>
                    <input type="number" class="form-control" v-model= "sub.zip" required>
                  </div>

                  <div class="form-group col-sm-2 my-1">
                    <label>Zip Code +4</label>
                    <input type="number" class="form-control" v-model= "sub.zip4">
                  </div>

                </div>
                  <br>
                <div class = "row">
                <div class = "form-group col-sm-3 my-1">
                  <label>Contractor Type</label>
                     <select class="form-control" v-model = "sub.subContractorTypeID" @click="subTypes">
                     <option v-for = "subtype in subtypes" v-bind:key = "subtype.id" v-bind:value = "subtype.subContractorTypeID">{{subtype.subContractorType}}</option>
                     </select>
                  </div>
                
                </div>
                <br>
                <div class="form-group">
                    <button class="btn btn-success btn-block col-sm-3 my-1">Create</button>
                </div>
            </form>
        </div>
    </div>

   
   

   

</div>
</template>


<script>
import axios from "axios";

export default {
  data(){
    return{
      sub:{
        subContractorTypeID: '',
        companyName: '',
        phone: '',
        email: '',
        streetNum: '',
        unit: '',
        pre_fix: '',
        streetName: '',
        suffix: '',
        unitNum: '',
        city:'',
        stateID:'',
        zip: '',
        zip4:''
        

      },
      states: [],
      subtypes: []

     

    

    }


  },

      created() {
           let apiURL = 'http://localhost:8000/api/stateNames';
            axios.get(apiURL).then(res => {
                this.states = res.data;
            }).catch(error => {
                console.log(error)
            });
      },
  methods:{

    subTypes(){
       let apiURL = 'http://localhost:8000/api/subtype';
            axios.get(apiURL).then(res => {
                this.subtypes = res.data;
            }).catch(error => {
                console.log(error)
            });

    },
    handleSubmitForm() {
                let apiURL = 'http://localhost:8000/api/addSubcontractor';
                
                axios.post(apiURL, this.sub).then(() => {
                  this.$router.push('/viewSubcontractors')
                  this.sub = {
                         subContractorTypeID: '',
                         companyName: '',
                         phone: '',
                         email: '',
                         streetNum: '',
                         unit: '',
                         pre_fix: '',
                         streetName: '',
                         suffix: '',
                         unitNum: '',
                         city:'',
                         stateID:'',
                         zip: '',
                         zip4:''
                  }
                }).catch(error => {
                    console.log(error)
                });
            }

  }
}
</script>