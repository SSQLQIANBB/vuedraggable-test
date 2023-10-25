<template>
  {{ name }}

  <n-form
    ref="formRef"
    :model="state.model"
    :rules="rules"
    :size="size"
    label-placement="top"
  >
    <n-grid :cols="24" :x-gap="24">
      <n-form-item-gi :span="24" label="Input" path="inputValue">
        <n-input v-model:value="state.model.inputValue" placeholder="Input" />
      </n-form-item-gi>
      <n-form-item-gi :span="24" label="Textarea" path="textareaValue">
        <n-input
          v-model:value="state.model.textareaValue"
          placeholder="Textarea"
          type="textarea"
          :autosize="{
            minRows: 3,
            maxRows: 5
          }"
        />
      </n-form-item-gi>
    </n-grid>
  </n-form>
</template>

<script lang="ts" setup>
import { reactive } from 'vue';

const name = 'form';

const state = reactive({
  model: {
    inputValue: '',
    textareaValue: '',
  },
  rules: {},
})

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
