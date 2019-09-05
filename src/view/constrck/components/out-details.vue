<template>
  <div class="pb120 pl18 pt18 pr18">
    这是他的ID：{{ this.id }}
    <!-- <Row :gutter="16">
      <Col span="4">
        <Card :padding="0">
          <Menu theme="light" :active-name="active">
            <MenuItem name="one">test1</MenuItem>
            <MenuItem name="two">test2</MenuItem>
          </Menu>
        </Card>
      </Col>
    </Row> -->
    <Tree :data="data5" :render="renderContent" ></Tree>
    <Collapse v-model="value" accordion>
      <Panel name="1">
        one
        <p slot="content">jdsklaghfdjlhuafhjskehugsdduui</p>
      </Panel>
      <Panel name="2">
        two
        <p slot="content">jdsklaghfdjlhuafhjskehugsdduui</p>
      </Panel>
    </Collapse>
  </div>
</template>

<script>
export default {
  data () {
    return {
      id: '',
      active: '1',
      data5: [
        {
          title: 'parent 1',
          expand: true,
          children: [
            {
              title: 'parent 1-1',
              expand: true,
              children: [
                {
                  title: 'leaf 1-1-1'
                },
                {
                  title: 'leaf 1-1-2'
                }
              ]
            },
            {
              title: 'parent 1-2',
              expand: true,
              children: [
                {
                  title: 'leaf 1-2-1'
                },
                {
                  title: 'leaf 1-2-1'
                }
              ]
            }
          ]
        }
      ],
      buttonProps: {
        type: 'default',
        size: 'small'
      },
      dragstartNode: '',
      dragstartData: ''
    }
  },
  created () {
    this.id = this.$route.query.id
    console.log('id', this.id)
  },
  methods: {
    renderContent (h, { root, node, data }) {
      return h('span', {
        style: {
          display: 'inline-block',
          width: '100%'
        },
        attrs: {
          draggable: 'true'
        },
        on: {
          dragstart: () => this.handleDragStart(root, node, data),
          dragover: () => this.handleDragOver(root, node, data),
          dragend: () => this.handleDragEnd(root, node, data),
          drop: () => this.handleDrop(root, node, data)
        }
      }, [
        h('span', [
          h('Icon', {
            props: {
              type: 'ios-paper-outline'
            },
            style: {
              marginRight: '8px'
            }
          }),
          h('span', data.title)
        ]),
        h('span', {
          style: {
            display: 'inline-block',
            marginRight: '32px',
            marginLeft: '10px'
          }
        }, [
          h('Button', {
            props: Object.assign({}, this.buttonProps, {
              icon: 'ios-create',
              shape: 'circle'
            }),
            style: {
              marginRight: '8px'
            },
            on: {
              click: () => { this.append(data) }
            }
          }),
          h('Button', {
            props: Object.assign({}, this.buttonProps, {
              icon: 'ios-remove',
              shape: 'circle'
            }),
            on: {
              click: () => { this.remove(root, node, data) }
            }
          })
        ])
      ])
    },
    append (data) {
      const children = data.children || []
      children.push({
        title: 'appended node',
        expand: true
      })
      this.$set(data, 'children', children)
    },
    remove (root, node, data) {
      const parentKey = root.find(el => el === node).parent
      const parent = root.find(el => el.nodeKey === parentKey).node
      const index = parent.children.indexOf(data)
      parent.children.splice(index, 1)
    },
    handleDragStart (root, node, data) {
      const event = window.event || arguments[0]
      this.dragstartNode = node
      this.dragstartData = data
    },
    handleDragOver (root, node, data) {
      const event = window.event || arguments[0]
      event.preventDefault()
    },
    handleDragEnd (root, node, data) {
      const event = window.event || arguments[0]
      event.preventDefault()
    },
    handleDrop (root, node, data) {
      event.preventDefault()
      if (node === this.dragstartNode) return
      const target_parentKey = root.find(el => el === node).parent
      const target_parent = root.find(el => el.nodeKey === target_parentKey).node
      const target_index = target_parent.children.indexOf(data)
      const target_children = data.children || []
      target_children.push(this.dragstartData)
      this.$set(data, 'children', target_children)
      const source_parentKey = root.find(el => el === this.dragstartNode).parent
      const source_parent = root.find(el => el.nodeKey === source_parentKey).node
      const source_index = source_parent.children.indexOf(this.dragstartData)
      source_parent.children.splice(source_index, 1)
    }
  }
}
</script>
