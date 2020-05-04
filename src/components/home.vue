<template>
  <div>
    <div>
      <!-- 标题 -->
      <h1>学生成绩管理系统</h1>
      <!-- 操作区 -->
      <div class="options">
        <!-- 搜索关键词 -->
        <div>
          <Input
            suffix="ios-search"
            placeholder="Enter text"
            style="width: 300px"
            class="search"
            clearable
            v-model="msg"
          />
        </div>
        <!-- 添加信息 -->
        <Button type="primary" @click="modal1 = true">增加信息</Button>
        <Modal
          v-model="modal1"
          title="普通的Modal对话框标题"
          @on-ok="ok"
          @on-cancel="cancel"
        >
          <p>对话框内容</p>
          <p>对话框内容</p>
          <p>对话框内容</p>
        </Modal>
      </div>
      <!-- 信息区 -->
      <Table border :columns="columns12" :data="serach(msg)" class="tab">
        <template slot-scope="{ row }" slot="name">
          <strong>{{ row.name }}</strong>
        </template>
        <template slot-scope="{ row, index }" slot="action">
          <Button
            type="primary"
            size="small"
            style="margin-right: 5px"
            @click="edit(index)"
            >修改</Button
          >
          <Button type="error" size="small" @click="remove(index)">删除</Button>
        </template>
      </Table>
      <!-- 添加信息对话框 -->
      <div>
        <Modal
          :visible.sync="modal1"
          title="请按格式填写信息"
          @on-ok="ok"
          @on-cancel="cancel"
        >
        <!-- 表单信息 -->
        <Form ref="formValidate" :model="formValidate" :rules="ruleValidate" :label-width="80">
            <!-- 姓名 -->
          <FormItem label="Name" prop="name">
            <Input v-model="formValidate.name" placeholder="Enter your name"/>
          </FormItem>
            <!-- 班级 -->
            <FormItem label="Grade" prop="grade">
              <Select v-model="formValidate.city" placeholder="请选择班级">
                  <Option value="beijing">New York</Option>
                  <Option value="shanghai">London</Option>
                  <Option value="shenzhen">Sydney</Option>
              </Select>
          </FormItem>
          <!-- 学号 -->
          <FormItem label="E-mail" prop="mail">
            <Input v-model="formValidate.mail" placeholder="Enter your e-mail"/>
          </FormItem>
        </Form>
        </Modal>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      // 搜索关键词
      msg: "",
      // 开启对话框
      modal1: false,
      model:'',
      ruleValidate:"",
      formValidate:'',
      rules:'',
      columns12: [
        {
          type: "index",
          width: 60,
          align: "center",
        },
        {
          title: "班级",
          slot: "name",
        },
        {
          title: "姓名",
          key: "age",
        },
        {
          title: "学号",
          key: "address",
        },
        {
          title: "Action",
          slot: "action",
          width: 150,
          align: "center",
        },
      ],
      data6: [
        {
          name: "John Brown",
          age: 18,
          address: "New York No. 1 Lake Park",
        },
        {
          name: "Jim Green",
          age: 24,
          address: "London No. 1 Lake Park",
        },
        {
          name: "Joe Black",
          age: 30,
          address: "Sydney No. 1 Lake Park",
        },
        {
          name: "Jon Snow",
          age: 26,
          address: "Ottawa No. 2 Lake Park",
        },
      ],
    };
  },
  methods: {
    serach(keyword) {
      let newUsers = [];
      this.data6.forEach((value) => {
        if (value.name.indexOf(keyword) != -1) {
          newUsers.push(value);
        }
      });
      return newUsers;
    },
    
    ok() {
      this.$Message.info("点击了确定");
    },
    cancel() {
      this.$Message.info("点击了取消");
    },
    // edit(index){
    // },
    // remove(index){
    // }
  },
};
</script>
<style>
h1 {
  width: 100%;
  height: 100px;
  line-height: 100px;
  text-align: center;
  background: #0c7d9d;
  opacity: 0.7;
}

.options {
  width: 500px;
  height: 100px;
  margin: 0 auto;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  text-align: center;
}
/* .ivu-input{
  width: 300px !important;
} */
.tab {
  width: 800px;
  margin: 0 auto;
  text-align: center;
  /* height: 500px; */
}
</style>
