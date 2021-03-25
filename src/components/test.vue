/**
computed 没有双向绑定
computed 里面的 return 相当于 get()，是只读的
如果要改变 computed 里面的值要用 set()
通过 set() 改变值之后，页面上并不会渲染
如果一定要渲染到页面上，可以使用 Vue.$forceUpdata() 进行强制渲染
*/

<template>
  <div class="test">
    <div class="lis" v-for="(item, index) in list" :key="item.id">
      <span>{{ item.name }}</span>
      <input type="button" @click="btnClick(index)" />
    </div>
  </div>
</template>

<script>
export default {
  name: "Test",
  data() {
    return {};
  },
  computed: {
    list: {
      get() {
        return [
          {
            name: "zhangsan",
            id: 1,
          },
          {
            name: "lisi",
            id: 2,
          },
          {
            name: "wangwu",
            id: 3,
          },
        ];
      },
      set(i){
          this.list[i].name += "1";
      }
    },
  },
  methods: {
    btnClick(i) {
    //   this.$set(this.list[i], "name", this.list[i].name + "1");
    this.list = i;
    this.$forceUpdate();
    },
  },
  watch: {
    list: {
      handler(val) {
        console.log(val);
      },
      deep: true,
    },
  },
};
</script>