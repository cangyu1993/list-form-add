<template>
  <div class="home">
    <ul class="list_area">
      <li
        v-for="(item, index) in list"
        :key="index"
        @click="editForm(index)"
        class="li_list"
      >
        <p class="art_title">标题：{{ item.name }}</p>
        <p class="art_title">内容：{{ item.content }}</p>
      </li>
      <li class="add_act" @click="addForm">+</li>
    </ul>
    <div class="form_area">
      <input type="text" v-model="form.name" placeholder="name" />
      <input type="text" v-model="form.content" placeholder="content" />
    </div>
  </div>
</template>

<script>
export default {
  name: "HomeView",
  data() {
    return {
      list: [],
      form: {
        name: "",
        content: "",
        image: "",
      },
      index: 0,
    };
  },
  watch: {
    form: {
      handler: function (newVal, oldVal) {
        this.updataForm(newVal);
      },
      deep: true,
    },
  },
  methods: {
    addForm() {
      let addData = { name: "", content: "", image: "" };
      this.list.push(addData);
      this.form = addData;
      if (this.list.length === 1) {
        this.index = 0;
      } else {
        this.index = this.list.length - 1;
      }
    },
    editForm(index) {
      this.index = index;
      let addData = this.list[index];
      this.form = addData;
    },
    updataForm(data) {
      this.list.splice(this.index, 1, data);
    },
  },
};
</script>
<style lang="scss" scoped>
.home {
  box-sizing: border-box;
  display: flex;
  justify-content: space-around;
  .list_area {
    list-style: none;
    height: 100vh;
    width: 40%;
    padding: 50px 0;
    background-color: #ededed;
    .li_list {
      height: 50px;
      background-color: #fff;
    }
    .li_list:nth-of-type(n + 2) {
      margin-top: 20px;
    }
    .add_act {
      width: 80%;
      margin-left: 10%;
      border: 1px dashed #ddd;
      cursor: pointer;
    }
  }
  .form_area {
    height: 100vh;
    width: 40%;
    padding: 50px 0;
    background-color: skyblue;
    display: flex;
    flex-direction: column;
  }
}
</style>
