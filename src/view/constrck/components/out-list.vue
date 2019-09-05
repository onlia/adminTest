<template>
  <div>
    <Row class="mt20">
      <Col span="8">
        <Input v-model="keyword" @keyup.enter.native="query" placeholder="请输入要搜索的分组（支持模糊搜索）"></Input>
      </Col>
      <Col span="8">
        <Button type="primary" class="ml20">查 询</Button>
        <Button type="default" class="ml20">重 置</Button>
      </Col>
      <Col span="8" class="tr">
        <Button type="primary" icon="md-add" @click="add">新建分组</Button>
        <Button type="default" icon="md-refresh" class="ml20">刷新</Button>
      </Col>
    </Row>
    <Table :columns="columns" :data="data" class="mt20"></Table>
    <out-add ref="outAdd"></out-add>
  </div>
</template>

<script>
import outAdd from './out-add'
export default {
  data () {
    return {
      keyword: '',
      modal: false,
      model: {
        name: ''
      },
      columns: [
        {
          title: '名称',
          key: 'name',
          render: (h, params) => {
            console.log(params)
            return h('div', [
              h('a', {
                on: {
                  click: () => {
                    this.$router.push('/constrck/out_details?id=' + params.row.id)
                  }
                }
              }, params.row.name)
            ])
          }
        },
        {
          title: '描述',
          key: 'description'
        },
        {
          title: '状态',
          key: 'status'
        },
        {
          title: '操作',
          key: 'action',
          render: (h, params) => {
            return h('div', [
              h('Button', {
                props: {
                  type: 'text',
                  size: 'small'
                },
                on: {
                  click: () => {
                    this.edit()
                  }
                }
              }, '编辑'),
              h('Button', {
                props: {
                  type: 'text',
                  size: 'small'
                },
                on: {
                  click: () => {
                    this.del(params.$index, params.row)
                  }
                }
              }, '删除')
            ])
          }
        }
      ],
      data: [
        {
          id: 1,
          name: '大讲堂',
          description: 'hguwphrskagfdihui',
          status: '开放'
        },
        {
          id: 2,
          name: '致远楼',
          description: 'fdahioapfdi',
          status: '关闭'
        }
      ]
    }
  },
  methods: {
    edit () {
    },
    del (index, row) {
      this.data.splice(index, 1)
    },
    add () {
      // this.$refs['outAdd'].init(this.id)
      this.$router.push('/constrck/rules_add')
    }
  },
  components: {
    outAdd
  }
}
</script>
