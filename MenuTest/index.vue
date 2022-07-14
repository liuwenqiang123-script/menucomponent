<template>
  <div>
    <el-menu
      :default-active="activeIndex"
      class="el-menu-demo"
      mode="horizontal"
      @select="handleSelect"
      background-color="rgba(255,255,255,1)"
      text-color="#fff"
      active-text-color="#1890ff"
      router
    >
      <template v-for="(menu, index) in menudata">
        <el-submenu
          :key="index"
          :index="index.toString()"
          v-if="menu.MenuItem.length != 0"
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

        <el-menu-item
          class="el-menu-item-custom"
          v-if="menu.MenuItem.length == 0"
          :key="index"
          :index="menu.url.toString()"
          :route="{ path: menu.url }"
          ><span class="menufontcustom">{{ menu.name }}</span></el-menu-item>
      </template>
    </el-menu>
  </div>
</template>
<script>
import loginVue from "../homepage/components/login.vue";
export default {
  name: "MenuTest",
  //   model:{
  //     prop: "activeIndex",
  //     event: "changeActiveIndex",
  //   },
  //监视如果页面离开
  created() {},
  mounted() {
    if (this.$route.path.slice(12).indexOf("/") != -1) {
      this.activeIndex =
        this.$route.path.slice(0, 12) +
        this.$route.path
          .slice(12)
          .substring(0, this.$route.path.slice(12).indexOf("/"));
    } else {
      this.activeIndex = this.$route.path;
    }
  },
  data() {
    return {
      //   current: '',
      activeIndex: "",
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
  watch: {
    activeIndex: function (newvalue, oldvalue) {
      console.log(newvalue, oldvalue, "watch");
    },
    $route(to, from) {
      console.log(to.path, from.path);
    //   this.activeIndex = to.path;
      if (to.path.slice(12).indexOf("/") != -1) {
        this.activeIndex =
          to.path.slice(0, 12) +
          to.path.slice(12).substring(0, to.path.slice(12).indexOf("/"));
      } else {
        this.activeIndex = to.path;
      }
    },
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
  color: rgb(71, 65, 65);
}
.menufontcustom {
  position: absolute;
  transform: translateX(-50%);
  left: 50%;
  color: rgb(255,255,255);
}

.menufont:active {
  color: rgb(4, 21, 38);
}

/deep/ .el-menu--horizontal > .el-submenu .el-submenu__title {
  height: 30px;
  line-height: 30px;
  background-color: rgba(0, 0, 0, 0) !important;
  border-bottom-color: rgba(0, 0, 0, 0) !important;
}
/deep/ .el-menu--horizontal > .el-submenu .el-submenu__title:hover {
  //   background-color: rgba(0, 0, 0, 0) !important;
  // color:rgb(24, 144, 255) !important;
}
/deep/ .el-submenu.is-active .el-submenu__title {
  border-bottom: none;
}
/deep/ .el-submenu.is-active {
  border-bottom: 2px rgb(24, 144, 255) solid;
}
/deep/ .el-menu-item-custom.is-active{
  border-bottom: 2px rgb(24, 144, 255) solid;
  background-color: rgb(255,255,255) !important;
  .menufontcustom{
    color:rgb(24, 144, 255);
  }
  
}
/deep/ .el-menu-item.is-active:hover{
  background-color: rgb(255,255,255) !important;
}
/deep/ .el-menu-demo {
  background-color: rgba(0, 0, 0, 0) !important;
}
/deep/ .el-menu-item:hover {
  background-color: rgba(152, 201, 247, 0.5) !important;
  .menufont {
    color: rgb(24, 144, 255);
  }
}
/deep/ .el-menu-item-group__title {
  padding: 0 !important;
}
/deep/ .el-menu-item-custom {
  padding: 0 100px;
  height: 30px;
  line-height: 35px;
  background-color: rgba(0, 0, 0, 0) !important;
  border-left: 2px solid white;
  
}
/deep/ .el-menu-item-custom:active{
//   background-color: rgb(255,255,255) !important;
  
}
/deep/ .el-menu-item-custom:hover{
  background-color: rgba(152, 201, 247, 0) !important;
}
/deep/ .el-menu-item:last-child {
  border-right: 2px solid white;
}
</style>
