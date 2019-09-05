<template>
  <div class="pb120 pl18 pt18 pr18">
    <Card>
      <p slot="title"></p>
      <Steps :current="current" class="pt20 pb20" style="width:800px;margin: 0 auto">
        <Step title="设置规则"></Step>
        <Step title="完成"></Step>
      </Steps>
      <Form v-if="current === 0" ref="form" :model="model" :rules="rules" :label-width="100" class="pt20" style="width: 800px; margin: 0 auto;">
        <FormItem label="规则名称" prop="rulesName">
          <Select v-model="model.rulesName" style="width: 300px;">
            <Option v-for="(item, index) in nameList" :value="item.value" :key="index">{{ item.label }}</Option>
          </Select>
        </FormItem>
        <FormItem label="类型" prop="type" v-if="model.rulesName === '1'">
          <Select v-model="model.type" style="width: 300px;">
            <Option v-for="item in typeList" :value="item.value" :key="item.value">{{ item.label }}</Option>
          </Select>
        </FormItem>
      </Form>
    </Card>
  </div>
</template>

<script>
export default {
  data () {
    return {
      current: 0,
      model: {
        id: '',
        rulesName: ''
      },
      rules: {
        rulesName: [
          { required: true, message: '请输入名称', trigger: 'change' }
        ],
        type: [
          { required: true, message: '请输入类型', trigger: 'change' }
        ]
      },
      nameList: [{ label: 'hfdha', name: 'jack', value: '1' }, { label: 'hgjh', value: '2' }],
      typeList: [{ label: 'outside', value: '1' }, { label: 'inside', value: '2' }]
    }
  }
}
</script>
