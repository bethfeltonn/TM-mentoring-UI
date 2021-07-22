
<template>
  <div>
    <div class="top-container">
    <h1 class="">Report a Bug</h1> <br>
    <p class="">Please give a detailed description of the bug, so that we know where to make the change. All responses are anonymous.</p>
    <br>
    </div>
   <div class="contact-bug-container">
    <div class="middle-container">
    <cv-select
        label="Where did the bug occur?"
        class="contact-bug-input"
        v-model="where"
        invalid-message
        placeholder="Choose an option">
        <template v-if="where_invalid" slot="invalid-message">This is a required field.</template>
        <cv-select-option value="Login page">Login page</cv-select-option>
        <cv-select-option value="Creating a PenPic">Creating a PenPic</cv-select-option>
        <cv-select-option value="Downloading my PenPic">Downloading my PenPic</cv-select-option>
        <cv-select-option value="Other">Other</cv-select-option>
    </cv-select> <br>

    <cv-text-input
        label="If &quot;other&quot;"
        class="contact-other-input"
        id=""
        v-model="other"
        placeholder="Placeholder text">
      </cv-text-input> <br>
        </div>
      </div>
      <div class="bottom-container">
      <cv-text-area
        label="Please include a description of the bug"
        class=""
        id=""
        v-model="bug_description"
        invalid-message
        placeholder="Placeholder text">
        <template v-if="bug_description_invalid" slot="invalid-message">This is a required field.</template>
     </cv-text-area> <br>

     <cv-file-uploader
        class="upload-file"
        :kind="kind"
        label="Upload any relevant screenshots."
        helperText="Max file size is 500kb. Supported file types are .jpg, .png and .pdf."
        drop-target-label="Add file"
        accept=".jpg,.png,.pdf"
        v-model="screenshot"
        invalid-message
        :remove-aria-label="removeAriaLabel" ref="fileUploader">
        <template v-if="use_dropTargetSlot" slot="drop-target"><AddFilled16 /><strong>File Drop</strong><AddFilled16 /></template>
    </cv-file-uploader> <br>

    

    </div>
    
    <div class="buttons">
    <cv-button-set 
    :stacked="stacked"
    class="">
        <cv-button @click="back" kind="secondary">Back</cv-button>
        <cv-button @click="submit" kind="primary">Submit</cv-button>
    </cv-button-set>
    </div>
    

</div>  
      
</template>

<script>
// @ is an alias to /src

//import axios from "axios";

export default {
  name: "Home",
  created(){
    this.getBug();
  },
  data(){return{
    where: "",
    other: "",
    bug_description: "",
    screenshot: "",
    where_invalid: false,
    other_invalid: false,
    bug_description_invalid: false,
    screenshot_invalid: false,
    

  }},
  components: {
    
  },
  methods: {
     submit(){
        if (this.validate()) {
          var axios = require('axios');
          const d = new Date();
          const date = d.getTime();  
          let form = [this.where, this.other, this.bug_description, this.screenshot]
          console.log(form) 
          var data = {
            "description": this.bug_description,
            "location": this.where,
            "otherlocation": this.other,
            "imageref": date+".png",
            "datereceived": `${d.getFullYear()}-${d.getMonth()+1}-${d.getDate()}`
          };

          var config = {
            method: 'post',
            url: 'https://talentmatchtestenv.tk/api/bug',
            data : data
          };

          axios(config)
          .then(function (response) { location.reload()
            console.log(JSON.stringify(response.data));
          })
          .catch(function (error) {
            console.log(error);
          });

        
        }
  
        },
        
        back(){
        location.href = "http://localhost:8080";
      },

        validate(){
        this.where_invalid = false
        this.bug_description_invalid = false
       let valid_form = true
        if(!this.where){valid_form = false;this.where_invalid = true}  
        if(!this.bug_description){valid_form = false;this.bug_description_invalid = true}
        
        
        return valid_form
  },
   /*  async getBug(){
        const path = "http://localhost:8082/api/bug/1";
        let bug = await axios ({
          url: path, 
          method: "get"
        })
        .then (
          (data)=>{
            console.log(data);
          }
        )
      } */
    
      
  },
  
   
  

};
</script>



<style scoped>
 .label{
    min-width: 80px !important;
    display: inline-block;
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

  .middle-container{
    display: inline-flex;
    }

  .bottom-container{
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-content: flex-start;
    width: 100%;
    min-width: 500px;
    max-width: 500px;
    text-align: left;
  }


  .contact-bug-container{
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-content: flex-start;
    width: 100%;
    min-width: 500px;
    max-width: 500px;
    text-align: left;
    }

  .contact-bug-buttons{
    min-width: 500px;
    max-width: 500px;
    padding: 20px;
    }

  

  .contact-bug-input{
    padding-right: 10px;
    max-width: 230px;
    min-width: 230px;
    }

  .contact-other-input{
    padding-left: 10px;
    max-width: 230px;
    min-width: 230px;
  }

  .buttons{
      padding-left: 20px;
  }
  

  
  
 
 

</style>