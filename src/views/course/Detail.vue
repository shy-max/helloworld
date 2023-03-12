<template>
  <div class="detail-container">
    <el-container class="flex flex-col">
      <Header></Header>
      <el-container>
        <el-menu :default-active="this.$route.path" class="course-menu" router>
          <div class="course-introduce">
            <img
              class="course-img"
              :src="courseInfo.img"
              :alt="courseInfo.couresName"
            />
            <div class="course-name">{{ courseInfo.couresName }}</div>
          </div>
          <MenuItem
            v-for="(item, index) in menus"
            :key="index"
            :item="item"
          ></MenuItem>
        </el-menu>
        <div class="course-main">
          <!-- 右侧内容 -->
          <router-view></router-view>
        </div>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import Header from "@/components/common/Header.vue";
import MenuItem from "@/components/common/MenuItem.vue";
import { mapGetters } from "vuex";

export default {
  name: "Detail",

  data() {
    return {
      courseInfo: null,
      menus: [
        {
          id: 1,
          title: "消息",
          path: "/course/detail/message",
          icon: "el-icon-message-solid",
          children: [],
        },
        {
          id: 2,
          title: "实验",
          path: "/course/detail/experiment",
          icon: "el-icon-s-opportunity",
          children: [
            {
              id: 4,
              title: "我的实验",
              path: "/course/detail/experiment/my-experiment",
              icon: "el-icon-s-platform",
              children: [],
            },
            {
              id: 5,
              title: "新增实验",
              path: "/course/detail/experiment/add-experiment",
              icon: "el-icon-circle-plus",
              children: [],
            },
            {
              id: 6,
              title: "实验题库",
              path: "/course/detail/experiment/question-manage",
              icon: "el-icon-s-management",
              children: [],
            },
          ],
        },
        {
          id: 3,
          title: "考试",
          path: "/course/detail/examination",
          icon: "el-icon-s-flag",
          children: [],
        },
      ],
    };
  },

  components: {
    Header,
    MenuItem,
  },

  created() {
    this.init();
  },

  methods: {
    ...mapGetters("COURSE", ["getCourse"]),
    init() {
      this.courseInfo = this.getCourse();
      // 开发过程用，后续需删除
      if (!this.courseInfo || this.courseInfo == "") {
        this.courseInfo = {
          img: "https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png",
          couresName: "软件工程课程设计",
          major: "软件工程",
          startingClass: "软件工程课程设计-0004",
          teacher: "叶娇娇",
          time: "2022-10-13~2024-10-13",
        };
      }
    },
  },
};
</script>

<style lang="less" scoped>
.detail-container {
  /deep/.course-menu {
    width: 250px;
    height: calc(100vh - 60px);
    padding: 10px 0;
    .course-introduce {
      margin: 0 auto;
      padding: 10% 0;
      width: 60%;
      height: 20%;
      .course-img {
        width: 100%;
        height: 100%;
      }
      .course-name {
        text-align: center;
      }
    }
    .menu-user {
      padding: 20px;
      text-align: center;
      font-size: 18px;
      overflow: hidden;
      white-space: nowrap;
      text-overflow: ellipsis;
    }
    .el-menu-item.is-active {
      background-color: rgba(87, 178, 251, 0.2);
      border-right: 4px solid #409eff;
    }
  }
  .course-main {
    padding: 10px;
    width: 100%;
    height: calc(100vh - 60px);
    overflow: auto;
    background-color: #f2f4f7;
  }
}
.user-popover {
  padding: 0 !important;
  .fun-item {
    .el-menu {
      border-right: 0;
    }
  }
}
</style>