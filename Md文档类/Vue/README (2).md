### vant
  官网: https://youzan.github.io/vant/#/zh-CN/
  安装: npm i vant -S
  使用方式:
    1.使用前要安装babel的插件 npm i babel-plugin-import -D
    2.配置babel ; 在.babelrc 中添加配置
      {
        "plugins": [
          ["import", {
            "libraryName": "vant",
            "libraryDirectory": "es",
            "style": true
          }]
        ]
      }
    3.引入方式一
      import Vue from 'vue';
      import { Button } from 'vant';
      Vue.use(Button);
    4.引入方式二
        import { Button } from 'vant';
        export default {
          components:{
            [Button.name]:Button
          }
        }

### van-contact-card
  type="add"
  add-text="添加联系人信息"
    添加联系人;以及添加联系人面板的文案
  type="edit"
  name="damu"
  tel="15851802777"
  :editable="false" 代表当前卡片是否可以被编辑(click事件能不能被触发)
    编辑联系人;以及联系人的信息

  @click : 点击card触发当前这个事件

### van-contact-list
  v-model : 当前选中者的id
  list    : 当前的联系人列表
  add-text : 新增按钮的文案
  default-tag-text : 默认联系人气泡文案

  @add : 点击新增按钮触发事件
  @edit: 点击编辑按钮触发事件
  @select: 点击选中按钮触发事件

### van-contact-edit
  tel: 最好还是使用字符串 在未来的版本中应该会支持number

  :contact-info="info"  : 联系人信息
  :is-edit="true"       : 出不出现删除按钮
  :is-saving="false"    : 保存按钮的动画
  :is-deleting="false"  : 删除按钮的动画
  :tel-validator="validator" : 手机号的验证函数
  :show-set-default="true"   : 代表是否出现默认联系人的选项
  set-default-label="xxx"    : 默认联系人区域的文案
  @save="saveFn"             : 保存事件 参数是contact-info中的内容  而不仅仅是表单的内容
  @delete="deleteFn"         : 删除事件

