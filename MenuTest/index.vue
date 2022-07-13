<template>
  <div>
    <!-- <a-menu v-model="current" mode="horizontal"  >
      <a-sub-menu v-for="(menu, index) in menudata" :key="index" >
        <span slot="title" class="submenu-title-wrapper"
          ><a-icon type="read" />{{ menu.name }}<a-icon type="caret-down"
        /></span>
        <a-menu-item-group title="">
          <a-menu-item v-for="menuitem of menu.MenuItem" :key="menuitem.id" 
            ><span class="menufont">{{ menuitem.name }}</span></a-menu-item
          >
        </a-menu-item-group>
      </a-sub-menu>
    </a-menu> -->

    <el-menu
      :default-active="activeIndex"
      class="el-menu-demo"
      mode="horizontal"
      @select="handleSelect"
      background-color="rgba(17,36,81,1)"
      text-color="#fff"
      active-text-color="#1890ff"
      router
    >
      <!-- <el-menu-item index="1">处理中心</el-menu-item> -->
      <el-submenu
        v-for="(menu, index) in menudata"
        :key="index"
        :index="index.toString()"
      >
        <template slot="title"
          ><span>{{ menu.name }}</span></template
        >
        <el-menu-item-group>
          <el-menu-item
            v-for="menuitem of menu.MenuItem"
            :key="menuitem.id"
            :index="menuitem.url"
            :route="{ path: menuitem.url }"
            ><span class="menufont">{{ menuitem.name }}</span></el-menu-item
          >
        </el-menu-item-group>
      </el-submenu>
    </el-menu>
  </div>
</template>
<script>
import loginVue from '../homepage/components/login.vue';
export default {
  name: "MenuTest",
//   model:{
//     prop: "activeIndex",
//     event: "changeActiveIndex",
//   },
          //监视如果页面离开
        created() {
        },
        mounted() {
             this.activeIndex = this.$route.path
            console.log(this.activeIndex);
        },
  data() {
    return {
    //   current: '',
      activeIndex: '',
    };
  },
  props: {
    menudata: {
      type: Array,
      default: [],
    },
  },
  methods: {
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
      this.activeIndex = keyPath[1];
    //   this.$emit("changeActiveIndex", this.activeIndex);
    //   console.log(this.activeIndex);
    },
  },
  watch:{
    activeIndex:function(newvalue,oldvalue){
        console.log(newvalue,oldvalue,"watch");
    },
    $route( to , from ){   
       console.log( to.path , from.path );
       this.activeIndex = to.path;
    //    console.log(to.path.slice(12));
    //    console.log(to.path.slice(12).indexOf("/"));
    if(to.path.slice(12).indexOf("/") != -1){
        // console.log(to.path.slice(0,12) + to.path.slice(12).substring(0,to.path.slice(12).indexOf("/")));
        this.activeIndex = to.path.slice(0,12) + to.path.slice(12).substring(0,to.path.slice(12).indexOf("/"))
    }else{
        // console.log(to.path.slice(0,12) + to.path.slice(12));
        // console.log(to.path);
        this.activeIndex = to.path;
    }
    // console.log(to.path.slice(0,12) + to.path.slice(12).substring(0,to.path.slice(12).indexOf("/")));

        // to , from 分别表示从哪跳转到哪，都是一个对象
        // to.path  ( 表示的是要跳转到的路由的地址 eg: /home );
     }
  },
 
};
</script>
<style lang="scss" scoped>
/deep/ .ant-menu-submenu {
  // background-color: rgb(87, 65, 65) !important;
  padding: 0 40px;
}
/deep/ .el-submenu {
  // background-color: rgb(87, 65, 65) !important;
  padding: 0 40px;
  border-left: 2px solid white;
}
/deep/ .el-submenu.is-active {
  background-color: rgb(255, 255, 255);
}
/deep/ .el-submenu:last-child {
  border-right: 2px solid white;
}
/deep/ .el-submenu:first-child {
  border-left: 2px solid white;
}
.menufont {
  position: absolute;
  transform: translateX(-70%);
  left: 50%;
}
/deep/ .el-menu--horizontal > .el-submenu .el-submenu__title {
  height: 30px;
  line-height: 30px;
  background-color: rgba(0, 0, 0, 0) !important;
  border-bottom-color:rgba(0,0,0,0) !important;

}
/deep/ .el-menu--horizontal > .el-submenu .el-submenu__title:hover {
  background-color: rgba(0, 0, 0, 0) !important;
  // color:rgb(24, 144, 255) !important;
}
/deep/ .el-submenu.is-active .el-submenu__title {
  border-bottom: none;
}
/deep/ .el-submenu.is-active {
  border-bottom: 2px rgb(24, 144, 255) solid;
}
/deep/ .el-menu-demo {
  background-color: rgba(0, 0, 0, 0) !important;
}
/deep/ .el-menu-item:hover{
    background-color: rgb(6, 26, 72) !important;
} 
</style>
