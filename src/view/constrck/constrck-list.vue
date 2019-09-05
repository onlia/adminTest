<template>
  <div>
    <!-- <Card>
      <p slot="search"></p>
      <Input v-model="key" placeholder="请输入要查询的名称" style="width: 300px;"></Input>
      <Button type="primary" class="ml20">查询</Button>
      <Button type="default" class="ml20">重置</Button>
    </Card> -->
    <Card :padding="20">
      <Tabs :value="value" :animated="false" @on-click="tabClick">
        <TabPane label="方式" name="out"></TabPane>
        <TabPane label="规则enheng" name="inner"></TabPane>
      </Tabs>
      <outList v-if="value === 'out'"></outList>
      <innerList v-if="value === 'inner'"></innerList>
    </Card>
  </div>
</template>

<script>
import outList from './components/out-list'
import innerList from './components/inner-list'
export default {
  components: {
    outList,
    innerList
  },
  data () {
    return {
      value: 'out'
    }
  },
  methods: {
    tabClick (name) {
      this.value = name
    }
  }
}
</script>
