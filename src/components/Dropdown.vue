<template>
  <div class="form-group">
    <select class="form-control"
     v-model="selectedOption"
     
      @input="sendata"
      >
      <option v-for="option in options" :value="option.value" :key="option.value">{{ option.text }}</option>
    </select>
  </div>
</template>

<script>
export default {
   props: {
    value: null,
    options: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      selectedOption: null
    }
  },
  methods:{
    sendata(event){
      this.$emit('input',  event.target.value )
    }
  },
//   mounted () {
//   this.selectedOption = this.value
// },
watch: {
  value: {
    immediate: true,
    handler: function (newValue) {
      this.selectedOption = newValue;
    }
  }
}
// watch: {
//   value: function (newValue) {
//     this.selectedOption = newValue
//   }
// }
}

</script>