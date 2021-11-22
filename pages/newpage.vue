<template>
  <div>

    <div>
      <el-form :model="formdata"
               :rules="rulesdata"
               label-width="120px">
        <el-form-item label="数据名"
                      prop="name">
          <el-input v-model="formdata.name"
                    placeholder="请输入名称"
                    clearable></el-input>
        </el-form-item>
        <el-form-item label="地址"
                      prop="area">
          <el-select v-model="formdata.area"
                     placeholder="请选择地址">
            <el-option v-for="item in areaoptions"
                       :key="item.value"
                       :label="item.label"
                       :value="item.value"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="联系电话"
                      prop="phone">
          <el-input v-model="formdata.phone"
                    placeholder="请输入电话号码"
                    clearable></el-input>
        </el-form-item>
        <el-form-item label="数值"
                      prop="number">
          <el-input-number v-model="formdata.number"
                           placeholder="请输入任意数字"
                           clearable></el-input-number>
        </el-form-item>
      </el-form>
      <li v-for="con in Content"
          :key="con.name">
        <nuxt-link :to="{name:getContentTestRouterName($i18n.locale), params:{content:con}}">
          <b>{{con.name}}</b><br>
        </nuxt-link>
      </li>
    </div>
    <p>Please click the button</p>
    <button id="Newbtn"
            @click="$fetch">重置 data </button>
    <div id="NewForm"
         v-html="newhtml"></div>
    <nuxt-link to='/'>回到首页</nuxt-link>
  </div>
</template>
<script>

import { Form, FormItem, Select, Input, Option, InputNumber } from 'element-ui';
import datajson from '../static/jsons/index'

export default ({
  // layout:'Demotest',
  async asyncData () {
    console.log("first run!");
  },
  components: {
    [Form.name]: Form,
    [FormItem.name]: FormItem,
    [Select.name]: Select,
    [Input.name]: Input,
    [Option.name]: Option,
    [InputNumber.name]: InputNumber
  },
  data () {
    return {
      newhtml: `<p> Hello "Benny"</p>`,
      areaoptions: [{
        value: '选项1',
        label: '北京'
      }, {
        value: '选项2',
        label: '上海'
      }, {
        value: '选项3',
        label: '广州'
      }],
      formdata: {
        name: '',
        area: '',
        phone: '',
        number: 0
      },
      rulesdata: {
        name: [{ required: true, message: '请输入名称', trigger: 'blur' }, { min: 3, max: 10, message: '长度在3到10个字符', trigger: 'blur' }],
        area: [{ required: true, message: '请选择地域', trigger: 'change' }],
        phone: [{ required: true, message: '请输入联系电话', trigger: 'blur' }, { pattern: /^1[3|4|5|8][0-9]\d{4,8}$/, message: '请输入电话号码', trigger: 'blur' }],


      },
      data1: {},
      input1: '',
      Content: []
    }
  },
  async fetch () {
    const packages = datajson;
    /* this.Content = await this.$http.$get('https://github.com/guibowdgf/RoomChen/blob/master/test.json'); */
    console.log(packages);
    this.Content = packages;
  },
  methods: {
    getContentTestRouterName (locale) {
      if (locale === 'en')
        return "ContentTest-ContentTest___en";
      else if (locale === 'ar')
        return "ContentTest-ContentTest___ar"
    },

  }
})
</script>
<style scoped>
#Newbtn {
  position: relative;
  color: blue;
}
.el-input {
  width: 500px;
}
</style>
