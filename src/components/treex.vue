<script>
  import TreeRender from '@/components/tree_render'
  import {Tree} from 'element-ui'

  export default {
    extends: Tree,
//    mixins: [Tree],
    props: {

      renderContent: {
        type: Function,
        default(h, {node, data, store}) {
//          let that = this;
          return h(TreeRender, {
            props: {
              DATA: data,
              NODE: node,
              STORE: store,
//              maxexpandId: that.non_maxexpandId
            },
            on: {
              nodeAdd: ((s, d, n) => this.tree.handleAdd(s, d, n)),
              nodeEdit: ((s, d, n) => this.tree.handleEdit(s, d, n)),
              nodeDel: ((s, d, n) => this.tree.handleDelete(s, d, n))
            }
          });
        }
      }
    },
    name: 'tree2',
    data() {
      return {}
    },
    mounted() {

    },
    methods: {
      handleAdd(s, d, n) {//增加节点
        this.$emit('onNodeAdd', s, d, n)
      },
      handleEdit(s, d, n) {//增加节点
        this.$emit('onNodeEdit', s, d, n)
      },
      handleDelete(s, d, n) {//增加节点
        this.$emit('onNodeDelete', s, d, n)
      },

    }

  }
</script>

<style>
  .expand {
    width: 100%;
    height: 100%;
    overflow: hidden;
  }

  .expand > div {
    height: 85%;
    padding-top: 20px;
    width: 50%;
    margin: 20px auto;
    max-width: 400px;
    overflow-y: auto;
  }

  .expand > div::-webkit-scrollbar-track {
    box-shadow: inset 0 0 6px rgba(0, 0, 0, .3);
    border-radius: 5px;
  }

  .expand > div::-webkit-scrollbar-thumb {
    background-color: rgba(50, 65, 87, 0.5);
    outline: 1px solid slategrey;
    border-radius: 5px;
  }

  .expand > div::-webkit-scrollbar {
    width: 10px;
  }

  .expand-tree {
    border: none;
    margin-top: 10px;
  }

  .expand-tree .el-tree-node.is-current,
  .expand-tree .el-tree-node:hover {
    overflow: hidden;
  }

  .expand-tree .is-current > .el-tree-node__content .tree-btn,
  .expand-tree .el-tree-node__content:hover .tree-btn {
    display: inline-block;
  }

  .expand-tree .is-current > .el-tree-node__content .tree-label {
    font-weight: 600;
    white-space: normal;
  }
</style>
