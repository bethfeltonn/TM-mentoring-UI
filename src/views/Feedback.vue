<template>
<div>
    <h1 class="feedback-container">Feedback</h1> 
    <p class="feedback-container">Please provide any feedback that you feel will help improve TalentMatch. All responses are anonymous.</p> <br>

    <p class="feedback-container">How would you rate your experience with TalentMatch?</p>
    <cv-radio-group 
      :vertical="false"
      class="feedback-container"
      >
    <cv-radio-button name=1 label=1 value=1
      id=""
      :checked="false"
      :disabled="false"
      :hide-label="false"
      :label-left="labelLeft" 
      v-model="radioVal" />
    <cv-radio-button name=2 label=2 value=2 
      id=""
      :checked="false"
      :disabled="false"
      :hide-label="hideLabel"
      :label-left="false" v-model="radioVal" /> 
    <cv-radio-button name=3 label=3 value=3 
      id=""
      :checked="false"
      :disabled="false"
      :hide-label="false"
      :label-left="labelLeft" 
      v-model="radioVal" />
    <cv-radio-button name=4 label=4 value=4 
      id=""
      :checked="false"
      :disabled="false"
      :hide-label="false"
      :label-left="labelLeft" 
      v-model="radioVal" />
      <cv-radio-button name=5 label=5 value=5 
      id=""
      :checked="false"
      :disabled="false"
      :hide-label="false"
      :label-left="labelLeft" 
      v-model="radioVal" />
    </cv-radio-group>   <br>

    <cv-text-area
        label="What does TalentMatch do well?"
        class="feedback-container"
        id="message"
        v-model="do_well"
        invalid-message
        placeholder="Placeholder text">
        <template v-if="do_well_invalid" slot="invalid-message">This is a required field.</template>
     </cv-text-area> <br>

     <cv-text-area
        label="Where can TalentMatch be improved?"
        class="feedback-container"
        id=""
        v-model="improve"
        invalid-message
        placeholder="Placeholder text">
        <template v-if="improve_invalid" slot="invalid-message">This is a required field.</template>
     </cv-text-area> <br>

     <cv-button-set 
     :stacked="stacked"
     class="feedback-buttons" 
     >
        <cv-button @click="back" kind="secondary">Back</cv-button>
        <cv-button @click="submit" kind="primary">Submit</cv-button>
    </cv-button-set>
  <cv-toast-notification v-if="visible" 
 kind="success"
  id="successNotification"
  :title="title"
  :sub-title="subTitle"
  :caption="caption"
  @close="doClose"
  :close-aria-label="closeAriaLabel"
  :low-contrast="lowContrast"></cv-toast-notification>
</div> 
</template>

<script>
// @ is an alias to /src


export default {
  name: "Home",
  data(){return{
    do_well: "",
    improve: "",
    do_well_invalid: false,
    improve_invalid: false,
    

  }},
  components: {
    
  },
  methods: {
   
     
     submit(){
        if (this.validate()) {
        var axios = require('axios');
        const d = new Date();
        var rating = parseInt(this.radioVal)
        var data = {
          "rating": rating,
          "positives": this.do_well,
          "improvements": this.improve,
          "datereceived": `${d.getFullYear()}-${d.getMonth()+1}-${d.getDate()}`
        
        };

        var config = {
          method: 'post',
          url: 'https://talentmatchtestenv.tk/api/feedback',
          data : data
        };

        axios(config)
        .then(function (response) { location.reload()
          console.log(JSON.stringify(response.data));
        })
        .catch(function (error) {
          console.log(error);
        });

          let form = [this.radioVal, this.do_well, this.improve]
        console.log(form) 
        }
        
        },

        back(){
        location.href = "http://localhost:8080";
      },

        validate(){
        this.do_well_invalid = false
        this.improve_invalid = false
       let valid_form = true
        if(!this.do_well){valid_form = false;this.do_well_invalid = true}  
        if(!this.improve){valid_form = false;this.improve_invalid = true}
        
        
        
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

  .feedback-container{
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-content: flex-start;
    width: 100%;
    min-width: 500px;
    max-width: 500px;
    text-align: left;
    }

  .feedback-buttons{
    min-width: 500px;
    max-width: 500px;
    padding: 20px;
    }

 
 

</style>