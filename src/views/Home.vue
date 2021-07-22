<template>
  <div>
    <div class="top-container">
    <h1>
      Comments
    </h1>

    <p>
      Thank you for helping us to improve IBM TalentMatch! <br> All bug reports and feedback are anonymous.
    </p>
    <br>
    <br>
    <p>I am...</p>
      <br>
    <cv-radio-group 
      :vertical="true">
    <cv-radio-button name="report-a-bug" label="Reporting a Bug" value="report-a-bug" 
      id="reportABugButton"
      :checked="false"
      :disabled="false"
      :hide-label="false"
      :label-left="labelLeft" 
      v-model="radioVal" />
    <cv-radio-button name="feedback" label="Giving feedback" value="feedback" 
      id="feedbackButton"
      :checked="false"
      :disabled="false"
      :hide-label="hideLabel"
      :label-left="false" v-model="radioVal" /> 
    </cv-radio-group>
      <br>
      <br>
  <cv-button @click="directUser" id="next-button">
         Next
       </cv-button> 

       <br>
  

    </div>

    
  
</div> 
</template>

<script>
// @ is an alias to /src


export default {
  name: "Home",
  data(){return{
    first_name: "",
    last_name: "",
    email: "",
    location: "",
    type: "",
    message: "",
    first_name_invalid: false,
    last_name_invalid: false,
    email_invalid: false,
    location_invalid: false,
    type_invalid: false,
    message_invalid: false,

  }},
  components: {
    
  },
  methods: {
     submit(){
        if (this.validate()) {
          let form = [this.first_name, this.last_name, this.email, this.location, this.message, this.type]
        console.log(form) 
        }
  
        },

      directUser() {
        if (this.radioVal) {
        if (this.radioVal === "report-a-bug") location.href="http://localhost:8080/bug";
        else location.href="http://localhost:8080/feedback";
      
        }
        },
        validate(){
        this.first_name_invalid = false
        this.last_name_invalid = false
        this.email_invalid = false
        this.location_invalid = false
        this.message_invalid = false
        this.type_invalid = false
       let valid_form = true
        if(!this.first_name){valid_form = false;this.first_name_invalid = true}  
        if(!this.last_name){valid_form = false;this.last_name_invalid = true}
        if(!this.email){valid_form = false;this.email_invalid = true}
        if(!this.location){valid_form = false;this.location_invalid = true}
        if(!this.message){valid_form = false;this.message_invalid = true}
        if(!this.type){valid_form = false;this.type_invalid = true}
        
        return valid_form
  },

      
    
      
  },
  
   
  

};
</script>

<style scoped>
 .label{
    min-width: 80px !important;
    display: inline-block;
    }

  .name-container{
    display: inline-flex;
    }

  .first-name-input{
    min-width: 250px;
    max-width: 250px; 
    padding-right: 10px;
    }

  .last-name-input{
    min-width: 250px;
    max-width: 250px;
    padding-left: 10px;
    }

  .contact-container{
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
    }

  .contact-input{
    min-width: 500px;
    max-width: 500px;
    }

  .top-container{
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-content: flex-start;
    width: 100%;
    min-width: 500px;
    max-width: 500px;
    text-align: left;
  }

</style>