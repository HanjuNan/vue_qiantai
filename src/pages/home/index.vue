<template>
  <div>
    <!-- 首页 -->
    <!-- 首页路由组件 -->
    <!-- 商品分类子组件 -->
    <typeNav></typeNav>
    <!-- 中间轮博和右侧部分 -->
    <ListContainer></ListContainer>
    <!-- 今日推荐模块 -->
    <Recommend></Recommend>
    <!-- 排行榜模块 -->
    <Rank></Rank>
    <!-- 猜你喜欢模块 -->
    <Like ref="like"></Like>
    <!-- 
       Floor标签,通过v-for动态生成
       父子组件通信:props

       问题:VC[Home]身上的floorList这个属性的属性值有几种情况?

       仓库floorList:起始值 空数组
       仓库floorList:不是空数组,代表服务器数据回来了。v-for渲染子组件完毕。给组件的props,就是两个对象
    
    -->
    <Floor v-for="(floor,index) in floorList" :key="floor.id" :floor="floor"></Floor>
    <!-- 商标模块 -->
    <Brand></Brand>
  </div>
</template>

<script>
//局部组件:引入、注册、使用
//全局组件：只需要在入口文件定义一次,直接使用
import ListContainer from "./listContainer";
import Recommend from "./recommend";
import Rank from "./rank";
import Like from "./like";
import Floor from "./floor";
import Brand from "./brand";
import { mapState } from "vuex";
export default {
  name: "Home",
  components: {
    ListContainer,
    Recommend,
    Rank,
    Like,
    Floor,
    Brand,
  },
  //组件挂载完毕钩子
  mounted() {
    this.$store.dispatch("getFloorList");

  },
  computed: {
    ...mapState({
      floorList: (state) => state.home.floorList,
    }),
  },
};
</script>

<style scoped>
</style>
