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
        <Modal v-model="modal1" title="请输入需要填写的信息" @on-ok="ok">
          <!-- 对话框表单信息 -->
          <Form
            ref="formValidate"
            :model="formValidate"
            :rules="ruleValidate"
            :label-width="80"
          >
            <!-- 姓名 -->
            <FormItem label="姓名：" prop="name">
              <Input
                v-model="formValidate.name"
                placeholder="请输入姓名"
                autofocus
              />
            </FormItem>
            <!-- 班级 -->
            <FormItem label="姓名：" prop="grade">
              <Input v-model="formValidate.grade" placeholder="请输入班级" />
            </FormItem>
            <!-- 学号 -->
            <FormItem label="学号：" prop="num">
              <Input v-model="formValidate.num" placeholder="请输入学号" />
            </FormItem>
          </Form>
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
          <!-- 修改信息对话框 -->
          <Modal v-model="modal2" title="请输入需要修改的信息">
            <Form ref="editMsg" :model2="editMsg" :label-width="80">
              <!-- 姓名 -->
              <FormItem label="姓名：" prop="name">
                <Input
                  v-model="editMsg.name"
                  placeholder="请输入姓名"
                  autofocus
                />
              </FormItem>
              <!-- 班级 -->
              <FormItem label="姓名：" prop="grade">
                <Input v-model="editMsg.grade" placeholder="请输入班级" />
              </FormItem>
              <!-- 学号 -->
              <FormItem label="学号：" prop="num">
                <Input v-model="editMsg.num" placeholder="请输入学号" />
              </FormItem>
            </Form>
          </Modal>
          <Button type="error" size="small" @click="remove(index)">删除</Button>
        </template>
      </Table>
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
      modal2: false,
      // ruleValidate:"",
      formValidate: {
        name: "",
        grade:"",
        num: "",
      },
      editMsg:{
        name: "",
        grade:"",
        num: "",
      },
      ruleValidate: {
        name: [{ required: true, message: "请填写姓名", trigger: "blur" }],
        grade: [{ required: true, message: "请填写班级", trigger: "blur" }],
        num: [
          {
            required: true,
            message: "请填写学号",
            trigger: "blur",
            type: "number",
          },
        ],
      },
      columns12: [
        {
          type: "index",
          width: 60,
          align: "center",
        },
        {
          title: "姓名",
          slot: "name",
        },
        {
          title: "班级",
          key: "grade",
        },
        {
          title: "学号",
          key: "num",
        },
        {
          title: "Action",
          slot: "action",
          width: 150,
          align: "center",
        },
      ],
      data6: [
        { name: "张三", grade: "1班", num: "B18033125" },
        { name: "李磊", grade: "1班",  num: "B18033115" },
        { name: "王麻子",grade: "1班", num: "B1803321" },
        { name: "王建国", grade: "1班", num: "B18033113" },
        { name: "赵钱",grade: "1班",  num: "B18033126" },
        { name: "孙李",grade: "1班",  num: "B18033127" },
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
      // this.$Message.info("点击了确定");
      let obj = JSON.parse(JSON.stringify(this.formValidate));
      this.data6.push(obj);
    },

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
