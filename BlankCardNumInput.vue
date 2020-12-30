<template>
  <div
      class="money el-input"
      :class="{'is-disabled':disabled,'el-input-group el-input-group--append':!!$slots.append}">
    <div class="el-input el-input--suffix">
      <input
          :maxLength="maxlength"
          :placeholder="placeholder"
          ref="ipt"
          autocomplete="off"
          type="text"
          rows="2"
          :disabled="disabled"
          validateevent="true"
          class="el-input__inner"
          v-model="formatValue">
      <span class="el-input__suffix" v-show="showClose">
      <span class="el-input__suffix-inner">
      <i class="el-input__icon el-icon-circle-close el-input__clear" @click="clear"></i>
      </span>
    </span>
    </div>
    <div
        v-if="!!$slots.append"
        class="el-input-group__append">
      <slot name="append"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "BlankCardNumInput",
  data(){
    return {
      showClose:false
    }
  },
  props:{
    value: {
      type: String,
      required: false,
      'default': ''
    },
    disabled: {
      type: Boolean,
      required: false,
      'default': false
    },
    clearable: {
      type: Boolean,
      required: false,
      'default': false
    },
    placeholder:{
      type: String,
      required: false,
      'default': '请输入'
    },
    maxlength:{
      type: String,
      required: false,
      'default': '37'
    }

  },
  methods:{
    clear(){
      const {ipt} = this.$refs;
      ipt.focus();
      ipt.value='';
      this.$emit('input', '');
      this.$emit('change', '');
    },
    changeShowClose(val){
      this.showClose = val
    },
  },
  computed: {
    formatValue:{
      get() {
        this.changeShowClose(this.clearable&&this.value!=='');
        var formattedValue = this.value.replace(/\D/g, '').split(" ").join("");
        this.$emit('input', formattedValue)
        this.$emit('change', formattedValue)
        return this.value.replace(/\D/g, '').replace(/....(?!$)/g, '$& ');
      },

      set(val) {
        var formattedValue = val.split(" ").join("");
        this.$emit('input', formattedValue)
        this.$emit('change', formattedValue)
      }
    }

  }
}
</script>

<style scoped>

</style>