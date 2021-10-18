<template>
    <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
    <template #default>
        <p>Unfortunately, at least one input value is Invalid.</p>
        <p>Plesce check all input and enter some characters</p>
    </template>
    <template #actions>
        <base-button @click="confirmError">Okay</base-button>
    </template>
    </base-dialog>
  <base-card>
  <form @submit.prevent="submitData">
      <div class="from-control">
          <label for="title">Title</label>
          <input id="title" ref="titleInput" name="title" type="text">
      </div>
      <div class="from-control">
          <label for="description">Description</label>
          <textarea ref="descInput" name="description" id="description" cols="30" rows="10"></textarea>
      </div>
      <div class="from-control">
          <label for="link">Link</label>
          <input id="link" ref="linkInput" name="link" type="url">
      </div>
      <div>
          <base-button type="submit">Add Resource</base-button>
      </div>
  </form>
  </base-card>
</template>

<script>
import BaseButton from '../ui/BaseButton.vue';
import BaseDialog from '../ui/BaseDialog.vue';
export default {
  components: { BaseDialog, BaseButton },
    inject:['addresource'],
    data(){
        return {
            inputIsInvalid: false,
        }
    },
    methods:{
        submitData(){
            const entertitle = this.$refs.titleInput.value;
            const enterdesc = this.$refs.descInput.value;
            const enterlink = this.$refs.linkInput.value;

            if(entertitle.trim()===''|| enterdesc.trim()===''|| enterlink.trim()===''){
                this.inputIsInvalid = true;
                return;
            }

            this.addresource(entertitle, enterdesc,enterlink)

            this.$refs.titleInput.value=''
            this.$refs.descInput.value=''
            this.$refs.linkInput.value=''
        },
        confirmError(){
            this.inputIsInvalid = false;
        }
    }

}
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
  margin-bottom: 13px;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>