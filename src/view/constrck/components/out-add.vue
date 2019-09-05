<template>
  <div>
    <Modal v-model="modal" :title="title">
      <Form ref="form" :model="model">
        <FormItem label="名称" prop="name">
          <Input type="text" v-model="model.name"></Input>
        </FormItem>
      </Form>
    </Modal>
  </div>
</template>

<script>
export default {
  data () {
    return {
      title: 'new',
      modal: false,
      model: {
        name: ''
      }
    }
  },
  created () {
  },
  methods: {
    init (id) {
      console.log('id1', id)
      this.modal = true
    }
  }
}
</script>
